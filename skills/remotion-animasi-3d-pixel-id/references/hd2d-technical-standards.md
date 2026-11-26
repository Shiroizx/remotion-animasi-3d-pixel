# Standar Teknis HD-2D, Koreografi Karakter & Anti-Error Remotion

## 1. Acuan Wajib `.lemo-opuscar/` (Read-Only) & Override Resmi Skill
Sebelum menulis kode komponen 3D atau shader, agen wajib membaca dan mematuhi dokumen asli di dalam folder proyek `.lemo-opuscar/`:
- `.lemo-opuscar/DIRECTOR.md` — Gramatika penyutradaraan, *native moves*, dan ritme visual.
- `.lemo-opuscar/styles/hd-2d/STYLE.md` — Invarian teknis HD-2D (`24 px/m`, *Signed CoC*, *Bayer dithering*, *UI JRPG*, dan mastering `-14 LUFS`).
- `.lemo-opuscar/TECHNIQUE.md` & `.lemo-opuscar/styles/hd-2d/DEMO.md` — Pola implementasi shader, sprite billboard, lampu praktis, dan pipeline audio.
- **Dilarang keras** memodifikasi file apa pun di dalam `.lemo-opuscar/`. Seluruh kode kustom proyek ditulis di dalam `src/`.

**Aturan *Override* Resmi Skill Ini (Menang atas `DEMO.md` / `STYLE.md` bila berbeda):**
1. **Skala Sprite `24 px/m`:** Gunakan `48x72 px` (`2.0x3.0 m`) untuk karakter standar dan `64x96 px` (`2.67x4.0 m`) untuk sosok besar (menggantikan `34x50 px` pada `1/30 m/px` di `DEMO.md`).
2. **Kotak Dialog `NARATOR`:** Narasi POV orang ketiga tetap ditampilkan dalam kotak dialog berbingkai emas berlabel **`NARATOR`** lengkap dengan potret `96x96 px` (menggantikan *subtitle italic* tanpa bingkai di `STYLE.md` §4).
3. **Font Pilihan GATE 4:** `JrpgOverlay.tsx` wajib memakai pasangan font yang dipilih pengguna pada GATE 4 (`Cinzel + Cormorant Garamond` sebagai *default*, `Press Start 2P + Silkscreen`, atau `Playfair Display + Plus Jakarta Sans`).

---

## 2. Invarian Piksel, Pencahayaan, Shader & Anti-Error Remotion (`PostProcessEffects.tsx`)

1. **Kepadatan Tekstur Konstan `24 px/m` & Dither Band Sempit:**
   - Seluruh tekstur permukaan tanah, batu, kayu, dan bangunan wajib menggunakan `THREE.NearestFilter` murni (nol blur tekstur), *4x4 Bayer dithering*, palet bertingkat (*color ramps*), dan proyeksi `worldUV`.
   - **Lebar pita dither (`dz`):** Kunci `dz ≈ 0.22` untuk sprite karakter dan `dz ≈ 0.45` untuk tekstur lingkungan. Pita dither yang terlalu lebar akan memunculkan pola papan catur kasar di seluruh gambar.

2. **Integrasi Wajib `EffectComposer` + R3F `<ThreeCanvas>` (`PostProcessEffects.tsx`):**
   - Pada `<ThreeCanvas>`, set properti `gl={{ antialias: false, preserveDrawingBuffer: true, toneMapping: THREE.ACESFilmicToneMapping, toneMappingExposure: 1.15 }}`.
   - Ambil alih siklus render R3F secara eksklusif menggunakan `useFrame(({ gl, scene, camera }) => { composer.render(); }, 1)` (*priority = 1*) agar Three.js tidak merender dua kali ke layar. Akhiri rantai `EffectComposer` dengan satu `OutputPass` (hindari *double tone-mapping*).
   - **Signed Circle of Confusion (`CoC`) & Tilt-Shift Permanen:** Jangan menunggu parameter `?tilt=1` (milik HTML demo lama). Efek *Signed CoC* (menggabungkan *physical Depth of Field* + pita fokus *tilt-shift* dari `post_ts.js`) wajib selalu aktif di `PostProcessEffects.tsx` agar latar jauh/depan terblur lembut **tanpa** kebocoran halo ke subjek tajam di tengah.
   - **2x MSAA / SSAA & Guardrail Memori Portrait:** Gunakan target render `HalfFloatType` dengan `samples: 4` dan supersampling `2x` pada `16:9` / `1:1`. Untuk Portrait `1080x1920`, `2x` internal berarti `2160x3840`: jika VRAM/RAM terbatas saat `--concurrency=3`, turunkan `ssaa` ke `1.5` (atau `1.0`) agar Chromium tidak OOM.
   - **`UnrealBloom` & Zero Grain:** Kalibrasi `UnrealBloomPass` (mis. `strength: 0.55`, `radius: 0.75`, `threshold: 0.85`) khusus untuk layer emisif agar teks `JrpgOverlay.tsx` tidak silau. **0 film grain** (dilarang menambah noise/grain).

3. **Determinisme Mutlak untuk Render Paralel (`--concurrency=3`):**
   - Di Remotion, worker merender frame secara acak dan paralel. **Dilarang keras** menggunakan `delta` pada `useFrame`, `clock.getElapsedTime()`, `Date.now()`, `Math.random()`, atau komponen `@react-three/drei` yang non-deterministik.
   - Seluruh animasi kamera, partikel, ayunan angin, kilat, dan kedipan api wajib dihitung murni dari `useCurrentFrame()` dan `useVideoConfig()` menggunakan fungsi deterministik (`interpolate`, `spring`, *summed sines*, dan *seeded hash*).

4. **Pencahayaan Kontras Tinggi & Guardrail `STYLE.md` §9:**
   - Kontraskan langit/kabut malam indigo (`#0b0e1e`–`#141936`) melawan sumber cahaya hangat praktis (*summed sines* `±20%`).
   - **Wajib Front Fill Light (~2 m di depan tokoh):** Billboard datar hanya memiliki normal ke depan; tanpa *front fill* dingin (`intensity 1.2–1.8`), sprite yang membelakangi matahari atau lampu akan menjadi siluet hitam pekat.
   - **Wajib Rim Light & Hemisphere Fill:** Pada adegan malam/badai, nyalakan *Rim Light* dingin (`#60A5FA` / `#818CF8`, minimal `0.7`) + `hemisphereLight` minimal `0.4` (0 *dead black*).
   - **Pencegahan Sprite Burn-out:** Lampu praktis yang dibawa karakter wajib digeser **`0.42–0.45 m` ke arah kamera** dan material sprite di-cap melalui `onBeforeCompile` (`outgoingLight = min(outgoingLight, diffuseColor.rgb * 1.35 + emissive)`).
   - **Anti-NaN Beam & Kabut:** Dilarang memakai silinder untuk sorot cahaya volumetrik (menghasilkan `NaN` blok hitam saat menghadap kamera); gunakan *billboard beam cards* yang memudar terhadap sudut kamera. Untuk pendar cahaya jauh menembus kabut, pasang `depthTest = false` dan `renderOrder` lebih tinggi.

---

## 3. Sistem Sprite Karakter 2D dalam Ruang 3D (`PixelSprite.tsx` & `sprites.ts`)
1. **Resolusi & Proporsi `24 px/m`:**
   - `48x72 px` (`2.0 m x 3.0 m`) untuk karakter manusia/dewa utama; `64x96 px` (`2.67 m x 4.0 m`) untuk sosok raksasa/monster.
   - Menggunakan garis tepi *selout* `1 px` warna tinta hangat (`#140e21`).
2. **Bayangan Siluet Presisi (Bukan Kotak Persegi):**
   - Billboard wajib memakai `alphaTest={0.5}` dan `castShadow` + `receiveShadow`. Jika material dimodifikasi dengan `onBeforeCompile`, wajib menyertakan `customDepthMaterial` dengan `alphaTest: 0.5` dan peta tekstur utama agar bayangan di tanah membentuk siluet piksel asli.
3. **Layer Emisif Terpisah:**
   - Setiap karakter dengan elemen menyala (senjata energi, mahkota cahaya, mata, segel tangan, lentera) wajib memiliki kanvas/tekstur emisif terpisah agar hanya elemen tersebut yang memicu `UnrealBloom`.
4. **10 State Animasi Multi-Frame (`6–10 fps` stepped, pre-baked di `useMemo`):**
   - `idle` (bernapas & ayunan rambut/jubah 1.5–2 Hz)
   - `walk` (siklus langkah kaki & perpindahan koordinat 3D)
   - `stance` (kuda-kuda tempur/siaga)
   - `channel` (penyaluran energi/segel/aura)
   - `strike` (ayunan tebasan atau hantaman aksi ber-blur piksel 1 frame)
   - `stagger` (terdorong mundur terkena gelombang kejut)
   - `kneel` (berlutut menunduk di bawah hujan/hukuman)
   - `react` (tersentak/menoleh sinkron dengan *emote bubble*)
   - `action` (gestur membuka gulungan/menunjuk/ritual)
   - `emote` (pose ekspresif saat *emote bubble* muncul)

---

## 4. Arsitektur Set 3D Vertikal & Koreografi Kamera (`CameraRig.tsx`)
1. **Zero Asset & Layout Recycling (`90x90 m` Stage):**
   - Setiap produksi baru wajib membangun **2–3 zona set 3D vertikal yang kontras** (misalnya pelataran kuil berundak 3 tingkat, jembatan awan di atas jurang badai, dan tebing pantai dengan shader air piksel terkuantisasi) lengkap dengan 4 lapis kedalaman (*Sky Dome*, *Far Horizon*, *Midground*, *Foreground*) dan `<fogExp2>`.
2. **Kamera Multi-Axis & Focus-Band Sweep:**
   - Sudut 3/4 tinggi bergaya diorama miniatur (`38°–46°` FOV) menggunakan `interpolate` / `spring` deterministik: *High Crane Dive*, *Lateral Tracking*, *Focus-Band Sweep* (menggeser pita tajam *tilt-shift* antar-subjek), *Half-Orbit 110°* dengan getaran mikro 12 frame saat benturan klimaks, *Vertical Descent Crane*, dan *Rack Focus*.
   - **Kompensasi Framing Portrait (`1080x1920`):** Mundurkan jarak kamera 15%–25% dibanding mode Landscape `16:9` agar karakter pengapit, pilar, dan lentera di sisi kiri-kanan tidak terpotong bingkai vertikal.

---

## 5. UI Kotak Dialog JRPG (`JrpgOverlay.tsx`) & Font Deterministik
1. **Font Loading Anti-Fallback:**
   - Wajib memuat font pilihan GATE 4 melalui `@remotion/google-fonts` (atau `document.fonts.ready` yang dikunci `delayRender()` / `continueRender()`) agar frame awal tidak pernah dirender dengan font sistem standar.
2. **Header Bab Dinamis di Atas:**
   - Label judul/bab (mengikuti pasangan font pilihan GATE 4) yang otomatis diperbarui mengikuti perpindahan zona adegan di `story.ts`.
3. **Kotak Dialog Emas & Akurasi Pembicara:**
   - Bingkai gelap transparan bertepi garis emas (`#d8c28e`) dengan ornamen berlian sudut di zona aman bawah, potret piksel `96x96 px` (*nearest-neighbor*), dan teks dengan sorotan kata aktif warna emas (`#FDE047`) + kursor kedip `▼`.
   - Untuk narasi POV orang ketiga, label pembicara wajib tertulis **`NARATOR`**, dan seluruh teks disalin persis tanpa typo dari naskah final.
   - *Title Card* penutup ditahan minimal **`4.0` detik**.

---

## 6. Audio 3 Lapis, Hard Silence Beats & Mastering `-14 LUFS`
1. **2 Titik Jeda Sunyi Total (*Hard Silence Beats*):**
   - Sisipkan minimal 2 jeda sunyi penuh (`1.3–1.8` detik di mana bus musik dan ambience dimatikan ke `0`) tepat sebelum momen ledakan emosi atau klimaks.
2. **Sintesis Audio Prosedural Node-Native / FFmpeg (Tanpa Python):**
   - Karena proyek berjalan murni di ekosistem Node.js + Remotion, bangkitkan file WAV (`48 kHz` Stereo/Mono ke `public/sfx/`) untuk stem musik tematik (*drone/pad*, petikan senar/harpa/koto, timpani/taiko), *ambience* (angin, hujan, api unggun), dan *foley/micro-SFX* (`emote-pop`, langkah kaki, benturan senjata, petir, lonceng) menggunakan generator PCM/WAV Node.js (harmonik aditif + amplop ADSR + filtered noise) atau `ffmpeg -f lavfi` (`sine`, `anoisesrc`, `aevalsrc`).
3. **Mastering Two-Pass `-14 LUFS` via `scripts/mix-master-audio.mjs`:**
   - Tulis konfigurasi `scripts/audio-mix.json` berisi `narrationPath`, `narrationStartSec`, `targetDurationSec` (sama persis dengan total durasi komposisi Remotion termasuk *Title Card* 4 detik), `musicTracks`, `ambienceTracks`, `sfxTracks`, dan `silenceBeats`.
   - Jalankan `node scripts/mix-master-audio.mjs --config scripts/audio-mix.json` untuk menerapkan auto-ducking `-10 dB` saat vokal aktif, pemotongan *Hard Silence Beats*, transisi *J-Cut/L-Cut*, dan normalisasi two-pass ke **`-14 LUFS`** (`-1.2 dBTP`) menjadi 1 file `-master.wav` (`48 kHz` Stereo).

---

## 7. Detail Mikro Hidup (*Living World Micro-Details*)
Setiap *scene* wajib memiliki minimal **4 detail mikro deterministik** berbasis `useCurrentFrame()` (dengan saturasi warna 20%–30% lebih redup dari tokoh utama):
1. **Cuaca & Partikel Atmosfer:** Hujan miring 3 lapis, kilat petir reaktif menerangi awan, bara api melayang naik, atau debu cahaya emas (*golden dust motes*).
2. **Fauna Latar:** Kawanan burung piksel di cakrawala pada adegan terang, atau kunang-kunang berpendar di dekat semak/air pada adegan malam.
3. **Fisika Angin & Cahaya Praktis:** Goyangan dedaunan/tali sakral/lentera gantung (`Math.sin(frame * 0.05 + x * 0.4) * 0.06`), kedipan api anglo (*summed sines*), dan kilau riak air piksel terkuantisasi.
4. **Tekstur Permukaan:** Kerikil, lumut, batu basah, dan rumput liar instanced di atas medan `90x90 m`.
