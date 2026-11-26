# Remotion Animasi 3D Pixel / 2.5D Pixel Art (HD-2D Director Skills)

> Interactive end-to-end agent skill repository (**English & Bahasa Indonesia**) for creating **2.5D Pixel Art (HD-2D)** animations with **Remotion**, **Three.js**, **lemo-opuscar**, **ElevenLabs v4**, and **-14 LUFS** audio mastering—from an empty folder to a ready-to-upload MP4.

**Jump to / Pilih Bahasa:** [English](#english) · [Bahasa Indonesia](#bahasa-indonesia)

---

## English

### Overview & Available Skill Variants (`skills/`)

| Skill Name | Language | Path | Purpose |
| :--- | :--- | :--- | :--- |
| `remotion-animasi-3d-pixel-en` | **English** | [`skills/remotion-animasi-3d-pixel-en/`](skills/remotion-animasi-3d-pixel-en/SKILL.md) | Full interactive workflow, ElevenLabs v4 scripting, blueprint, and upload copywriting in English. |
| `remotion-animasi-3d-pixel-id` | **Bahasa Indonesia** | [`skills/remotion-animasi-3d-pixel-id/`](skills/remotion-animasi-3d-pixel-id/SKILL.md) | Panduan interaktif, naskah ElevenLabs v4, blueprint, dan caption upload berbahasa Indonesia. |

### System Requirements
- **Node.js** v20 or newer (v20 LTS / v22 LTS recommended)
- **Git** (optional; used only after explicit user confirmation to fetch the pinned `lemo-opuscar` visual reference)
- **ElevenLabs** account (to generate 1 single-pass voiceover MP3)
- Internet access on first run *(initial downloads for Remotion, Chromium Headless Shell, and optional pinned-commit `lemo-opuscar` reference total ~300–500 MB)*

> **FFmpeg Note:** You do not need a global FFmpeg/FFprobe installation; the pipeline automatically uses the FFmpeg & FFprobe binaries bundled with Remotion (`@remotion/compositor-*`) on Windows, macOS, and Linux.

### Installation

```bash
# 1. Interactive language selection (global install)
npx skills add Shiroizx/remotion-animasi-3d-pixel -g

# 2. Install the English skill directly (global)
npx skills add Shiroizx/remotion-animasi-3d-pixel --skill remotion-animasi-3d-pixel-en -g

# 3. Install the Indonesian skill directly (global)
npx skills add Shiroizx/remotion-animasi-3d-pixel --skill remotion-animasi-3d-pixel-id -g

# 4. Install both variants into the current project directory (without -g)
npx skills add Shiroizx/remotion-animasi-3d-pixel --all
```

### How to Use
Open a brand-new empty folder in your AI coding agent (Antigravity, Claude Code, Codex, Cursor, etc.) and trigger the skill:
- **English:** *"Hello, let's build a 3D pixel art animation"* or `/remotion-animasi-3d-pixel-en`
- **Bahasa Indonesia:** *"Halo, ayo buat animasi 3D pixel art"* or `/remotion-animasi-3d-pixel-id`

The agent guides you through **7 Interactive Gates (GATE 1–7)**:
1. **GATE 1:** Story idea check or concept brainstorming.
2. **GATE 2:** Continuity detection (*standalone*, sequel/continuation, or *cliffhanger*).
3. **GATE 3:** Quota-efficient ElevenLabs v4 script (single MP3 generation) + voice recommendations + Remotion/Three.js workspace setup (with explicit user confirmation before fetching external references).
4. **GATE 4:** VO-first duration analysis & questionnaire (aspect ratio `9:16` / `16:9` / `1:1`, FPS, frame format, lighting mood, and RPG font style).
5. **GATE 5:** Pre-production blueprint covering vertical 3D zones, multi-axis camera paths, 10 sprite states, and 3-layer sound design.
6. **GATE 6:** Modular HD-2D coding, procedural audio synthesis & two-pass `-14 LUFS` mastering, plus an 8-point quality audit.
7. **GATE 7:** Final MP4 render, audio-video stream verification, and anti-*AI-slop* upload captions.

### Repository Structure
```text
remotion-animasi-3d-pixel/
├── README.md
├── LICENSE
└── skills/
    ├── remotion-animasi-3d-pixel-id/
    │   ├── SKILL.md
    │   └── references/
    │       ├── elevenlabs-v4-guide.md
    │       ├── hd2d-technical-standards.md
    │       └── mix-master-audio-template.mjs
    └── remotion-animasi-3d-pixel-en/
        ├── SKILL.md
        └── references/
            ├── elevenlabs-v4-guide.md
            ├── hd2d-technical-standards.md
            └── mix-master-audio-template.mjs
```

### Workspace Dependencies & External References
When running **GATE 3** inside an empty workspace, the agent installs the project's npm packages below and only fetches the external visual reference after your explicit confirmation:

| Package / Repository | Source & Original Author Attribution | Role in Project |
| :--- | :--- | :--- |
| `lemomo-ai/lemo-opuscar` *(optional pinned-commit `8ca0dd8` sparse checkout to `.lemo-opuscar/` after user confirmation)* | **Lemomo / lemomoLab** ([lemomo-ai/lemo-opuscar](https://github.com/lemomo-ai/lemo-opuscar)) | Read-only visual architecture, shader, and Three.js/Remotion code-template reference (`DIRECTOR.md`, `TECHNIQUE.md`, `styles/hd-2d/STYLE.md`, `styles/hd-2d/DEMO.md`) — never overrides primary skill rules. |
| `remotion`, `@remotion/cli`, `@remotion/player`, `@remotion/media-utils`, `@remotion/transitions`, `@remotion/three` | **Remotion Team** ([remotion-dev/remotion](https://github.com/remotion-dev/remotion)) | React video composition engine, headless Chromium renderer, and bundled FFmpeg/FFprobe binaries. |
| `three` & `@types/three` | **Mr.doob (Ricardo Cabello) & Three.js Contributors** ([mrdoob/three.js](https://github.com/mrdoob/three.js)) | 3D WebGL renderer, *Signed CoC Tilt-Shift DoF*, `UnrealBloom`, and *ACES Filmic* shader pipeline. |
| `@react-three/fiber` & `@react-three/drei` | **Poimandres (`pmndrs`)** ([pmndrs/react-three-fiber](https://github.com/pmndrs/react-three-fiber)) | Declarative React 18 bindings for Three.js inside `<ThreeCanvas>`. |
| `react`, `react-dom`, `lucide-react`, `typescript` | **Meta / React Team**, **Lucide Contributors**, & **Microsoft** | React UI runtime, interface icons, and TypeScript checking. |

> **Optional Manual Skills:** No external agent skills are installed automatically. If you want optional Remotion SFX pattern guidance, you may manually run `npx skills add remotion-dev/remotion@add-sfx` yourself.

### Copyright, Public Domain & Creative Adaptation Policy
- **100% Safe & Copyright-Free Topics:** Original fiction (*Original IP*), folklore, ancient mythology, historical events & biographies, *Public Domain* classic literature/fables, philosophy/psychology, and science/general education are fully permitted (including for monetization), provided scripts are written originally and diorama visuals follow traditional or general descriptions.
- **Educational Exception (*Nominative Fair Use*):** For tech or programming tutorials and educational videos, users may depict pixel-art representations of framework, language, or tool logos (such as Laravel, Next.js, React, Python, Docker) solely to identify the technology being taught, without using them as a primary brand mark or implying official endorsement.
- **Reference Adaptation with Mandatory Differentiation:** 3D set code structures, script outlines, or logo/emblem inspiration may be adapted from existing references, **as long as nothing is copied verbatim (1:1)** and clear differentiators are introduced across spatial layout, color palettes, ornaments, naming, and narrative arc.
- **Prohibited / Unsafe Content:** Never copy characters, costumes, specific plotlines, or music from modern commercial IP (anime, games, films, modern novels—including modern studio interpretations of folklore such as Marvel, Disney, or Capcom), never copy modern books/transcripts word-for-word, never clone third-party voices in ElevenLabs without consent, and avoid prohibited extremism symbols (e.g., Nazi insignia in historical contexts), gore, or hate speech.

---

## Bahasa Indonesia

### Ringkasan & Varian Skill yang Tersedia (`skills/`)

| Nama Skill | Bahasa | Folder | Kegunaan |
| :--- | :--- | :--- | :--- |
| `remotion-animasi-3d-pixel-id` | **Bahasa Indonesia** | [`skills/remotion-animasi-3d-pixel-id/`](skills/remotion-animasi-3d-pixel-id/SKILL.md) | Panduan interaktif, naskah ElevenLabs v4, blueprint, dan caption upload berbahasa Indonesia. |
| `remotion-animasi-3d-pixel-en` | **English** | [`skills/remotion-animasi-3d-pixel-en/`](skills/remotion-animasi-3d-pixel-en/SKILL.md) | Alur lengkap, penaskahan ElevenLabs v4, blueprint, dan copywriting upload dalam bahasa Inggris. |

### Prasyarat Sistem
- **Node.js** v20 atau lebih baru (disarankan v20 LTS / v22 LTS)
- **Git** (opsional; digunakan hanya setelah konfirmasi eksplisit pengguna untuk mengambil referensi visual `lemo-opuscar` versi terkunci)
- Akun **ElevenLabs** (untuk men-generate 1 file audio narasi v4)
- Koneksi internet pada eksekusi pertama *(unduhan awal paket Remotion, Chromium Headless Shell, serta opsional referensi `lemo-opuscar` versi terkunci sekitar 300–500 MB)*

> **Catatan FFmpeg:** Anda tidak perlu menginstal FFmpeg/FFprobe secara global; pipeline ini menggunakan biner FFmpeg & FFprobe bawaan Remotion (`@remotion/compositor-*`) secara otomatis di Windows, macOS, dan Linux.

### Cara Instalasi

```bash
# 1. Pilih varian bahasa secara interaktif (instalasi global)
npx skills add Shiroizx/remotion-animasi-3d-pixel -g

# 2. Instal langsung varian Bahasa Indonesia (global)
npx skills add Shiroizx/remotion-animasi-3d-pixel --skill remotion-animasi-3d-pixel-id -g

# 3. Instal langsung varian English (global)
npx skills add Shiroizx/remotion-animasi-3d-pixel --skill remotion-animasi-3d-pixel-en -g

# 4. Instal kedua varian sekaligus di folder proyek saat ini (tanpa -g)
npx skills add Shiroizx/remotion-animasi-3d-pixel --all
```

### Cara Memakai
Buka folder kosong baru di agen coding Anda (Antigravity, Claude Code, Codex, Cursor, dll.), lalu panggil skill sesuai bahasa yang diinstal:
- **Bahasa Indonesia:** *"Halo, ayo buat animasi 3D pixel art"* atau `/remotion-animasi-3d-pixel-id`
- **English:** *"Hello, let's build a 3D pixel art animation"* or `/remotion-animasi-3d-pixel-en`

Agen akan memandu Anda melalui **7 Tahap Interaktif (GATE 1–7)**:
1. **GATE 1:** Pengecekan atau brainstorming ide cerita.
2. **GATE 2:** Deteksi kontinuitas cerita (*standalone*, sekuel, atau *cliffhanger*).
3. **GATE 3:** Penulisan naskah ElevenLabs v4 (1x generate utuh) + rekomendasi voice + penyiapan workspace Remotion/Three.js (dengan konfirmasi eksplisit sebelum mengunduh referensi eksternal).
4. **GATE 4:** Analisis durasi VO & kuesioner rasio aspek (`9:16`, `16:9`, `1:1`), FPS, kualitas render, pencahayaan, dan gaya font RPG.
5. **GATE 5:** Blueprint adegan 3D vertikal, kamera multi-axis, 10 state sprite, dan peta suara 3 lapis.
6. **GATE 6:** Coding komponen modular HD-2D, sintesis & mastering audio two-pass `-14 LUFS`, serta audit kualitas 8 poin.
7. **GATE 7:** Final render MP4, verifikasi stream audio-video, dan penyusunan caption upload anti-*AI-slop*.

### Dependensi Workspace & Referensi Eksternal
Saat menjalankan **GATE 3** di folder proyek kosong, agen memasang dependensi npm proyek berikut dan hanya mengunduh referensi eksternal setelah persetujuan eksplisit pengguna:

| Paket / Repositori | Sumber & Atribusi Pembuat Asli | Kegunaan dalam Proyek |
| :--- | :--- | :--- |
| `lemomo-ai/lemo-opuscar` *(opsional, sparse checkout commit terkunci `8ca0dd8` ke `.lemo-opuscar/` setelah izin pengguna)* | **Lemomo / lemomoLab** ([lemomo-ai/lemo-opuscar](https://github.com/lemomo-ai/lemo-opuscar)) | Referensi arsitektur visual, shader, dan template kode Three.js/Remotion (*read-only*, bukan instruksi sistem) dari `DIRECTOR.md`, `TECHNIQUE.md`, `styles/hd-2d/STYLE.md`, dan `styles/hd-2d/DEMO.md`. |
| `remotion`, `@remotion/cli`, `@remotion/player`, `@remotion/media-utils`, `@remotion/transitions`, `@remotion/three` | **Remotion Team** ([remotion-dev/remotion](https://github.com/remotion-dev/remotion)) | Engine komposisi video React, renderer Chromium Headless, dan binary FFmpeg/FFprobe bawaan. |
| `three` & `@types/three` | **Mr.doob (Ricardo Cabello) & Three.js Contributors** ([mrdoob/three.js](https://github.com/mrdoob/three.js)) | Renderer WebGL 3D, *Signed CoC Tilt-Shift DoF*, `UnrealBloom`, dan *ACES Filmic* shader pipeline. |
| `@react-three/fiber` & `@react-three/drei` | **Poimandres (`pmndrs`)** ([pmndrs/react-three-fiber](https://github.com/pmndrs/react-three-fiber)) | Binding deklaratif Three.js untuk React 18 di dalam `<ThreeCanvas>`. |
| `react`, `react-dom`, `lucide-react`, `typescript` | **Meta / React Team**, **Lucide Contributors**, & **Microsoft** | Runtime UI React, ikon antarmuka, dan type checking. |

> **Catatan Skill Opsional:** Tidak ada skill eksternal yang diinstal otomatis. Jika membutuhkan referensi pola SFX Remotion tambahan, pengguna dapat menjalankan `npx skills add remotion-dev/remotion@add-sfx` secara manual.

### Kebijakan Hak Cipta, Public Domain & Adaptasi Kreatif
- **Tema yang 100% Aman & Bebas Hak Cipta:** Cerita fiksi karangan sendiri (*Original IP*), cerita rakyat (*folklore*), mitologi kuno, peristiwa sejarah & biografi tokoh, sastra klasik/fabel *Public Domain*, filosofi/psikologi, serta edukasi sains & pengetahuan umum diperbolehkan sepenuhnya (termasuk untuk monetisasi), dengan syarat naskah ditulis ulang secara orisinal dan visual diorama dirancang berdasarkan deskripsi umum/tradisional.
- **Pengecualian Edukatif (*Nominative Fair Use*):** Untuk video edukasi atau tutorial teknologi/pemrograman, pengguna diperbolehkan menampilkan representasi piksel dari logo *framework*, bahasa pemrograman, atau teknologi (seperti Laravel, Next.js, React, Python, Docker) semata-mata untuk mengidentifikasi materi yang sedang dijelaskan, selama tidak dipakai sebagai logo merek utama maupun mengklaim afiliasi resmi.
- **Adaptasi Referensi dengan Pembeda Wajib:** Struktur kode set 3D, pola naskah, atau inspirasi desain logo/emblem boleh diadaptasi dari referensi yang ada, asalkan tidak disalin mentah (1:1) dan wajib memiliki pembeda yang tegas pada tata letak ruang, palet warna, ornamen, dan alur cerita.
- **Batasan yang Tidak Aman (Dilarang):** Dilarang menjiplak karakter, kostum, alur spesifik, atau musik dari IP komersial modern (anime, game, film, novel modern, termasuk adaptasi modern atas cerita rakyat seperti versi Marvel/Disney/Capcom), menyalin naskah kreator/buku modern kata per kata, melakukan kloning suara di ElevenLabs tanpa izin, serta menampilkan simbol ekstremisme terlarang (seperti lambang Nazi pada topik sejarah) maupun konten *gore*/SARA.

---

## License / Lisensi
Distributed under the [MIT](LICENSE) License. / Didistribusikan di bawah lisensi [MIT](LICENSE).
