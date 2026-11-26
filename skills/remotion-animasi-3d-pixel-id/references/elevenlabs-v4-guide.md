# Panduan Naskah & Voice ElevenLabs v4

## Expressive Audio Tags Resmi Eleven v4
Sisipkan tag berikut di dalam kurung siku `[...]` tepat sebelum kalimat/frasa yang membutuhkan perubahan emosi:
- `[curious]` — nada bertanya, memancing rasa penasaran (cocok untuk Hook).
- `[serious]` / `[dramatic]` — nada bercerita epik dan berwibawa.
- `[tense]` / `[ominous]` — suasana mencekam, misterius, atau terancam.
- `[angry]` — emosi meledak, murka, atau bentakan dramatis.
- `[sighs]` / `[somber]` — helaan napas berat, kecewa, atau sedih mendalam.
- `[whispers]` — bisikan tegang untuk bagian rahasia atau horor.
- `[confident]` — nada tegas untuk kalimat penutup / *cliffhanger*.

## Aturan Penulisan Naskah
1. **Panjang Ideal:** 95–125 kata (menghasilkan durasi VO ~45–55 detik pada kecepatan normal, sehingga menyisakan ruang untuk *Chapter Card*, 2 *Hard Silence Beats*, dan *Title Card* penutup 4 detik agar total durasi video berada di kisaran 50–65 detik).
2. **Jeda Dramatis & Paragraf (Wajib Dilongkap 1 Baris):** Pada bagian *Naskah Siap Salin*, wajib pisahkan setiap segmen adegan dengan **1 baris kosong (`Enter` 2x)** agar ElevenLabs v4 memberi jeda napas alami antar-adegan dan memudahkan pemetaan *timeline* Remotion.
3. **Pelafalan Bahasa Asing / Istilah Khusus:** Pecah suku kata nama atau istilah non-Indonesia dengan tanda hubung (misalnya `Val-ha-lla`, `Ex-ca-li-bur`, `A-ra-shi`, `Hi-ka-ri`) agar `Language: Auto` di Eleven v4 tidak salah membaca vokal.
4. **Anti AI-Slop Copywriting (Wajib):**
   - Tulis dengan gaya tutur *storyteller* manusia yang lugas, konkret, dan langsung menggambarkan aksi adegan.
   - **DILARANG** memakai frasa klise AI seperti *"menebar teror tanpa henti"*, *"tak ingin alam semesta binasa"*, *"bayangkan jika..."*, pertanyaan retoris (*"bagaimana cara..."* / *"kira-kira apa yang terjadi..."*), maupun kata sifat berlebih (*"sangat dramatis"*, *"begitu luar biasa"*).

## Rekomendasi Karakter Suara (Voice) Eleven v4
Selalu sarankan pilihan suara berikut sesuai karakter cerita:
1. **Narator Pria Epik & Berwibawa:** `Callum`, `George`, atau `Raunak M` (vokal dalam, artikulasi bahasa Indonesia jernih, sangat responsif terhadap transisi `[dramatic]` ke `[angry]`).
2. **Narator Pria Dokumenter Hangat:** `Brian` atau `Daniel` (cocok untuk cerita sejarah, filosofi, atau mitologi yang tenang).
3. **Narator Wanita Misterius & Ekspresif:** `Aria` atau `Charlotte` (cocok untuk dongeng gelap atau sudut pandang tokoh utama wanita).
4. **Custom Voice Design v4:** Jika pengguna ingin suara unik, berikan *prompt* deskripsi karakter suara dalam bahasa Inggris untuk fitur **Try Voice Design for v4**.
