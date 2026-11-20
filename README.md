# Pemadat Prompt

Alat web satu file (`index.html`) untuk memadatkan prompt tanpa mengubah maksudnya.

## Deploy lewat GitHub Pages

1. Buat repo baru di GitHub, misalnya `pemadat-prompt` (Public).
2. Upload `index.html` dan `README.md` ke root repo.
3. Buka **Settings → Pages**.
4. Di *Build and deployment*, pilih **Deploy from a branch**, branch `main`, folder `/ (root)`, lalu **Save**.
5. Tunggu 1-2 menit. Alamatnya: `https://USERNAME.github.io/pemadat-prompt/`.

## Cara pakai

- **Mode AI**: masukkan API key Anthropic (dari console.anthropic.com), pilih model dan target hemat, tempel prompt, klik **Kirim**. Opsi *Cek makna otomatis* menjalankan AI kedua yang membandingkan hasil dengan aslinya dan memulihkan instruksi yang hilang.
- **Mode Lokal**: gratis, tanpa API. Hanya membuang basa-basi, pengulangan, dan frasa sopan. Kode dan teks dalam tanda kutip tidak disentuh.
- `Ctrl+Enter` = Kirim.

## Keamanan API key

- Jangan menulis API key di dalam file di repo. Alat ini meminta key lewat kolom input dan hanya menyimpannya di browser Anda (opsional).
- Key tetap terlihat di browser pemakai. Pakai key pribadi dengan batas pengeluaran (spend limit), dan jangan bagikan alamat situsnya jika key tersimpan.
- Jika ingin dipakai orang lain tanpa key mereka, buat proxy (misalnya Cloudflare Worker) yang menyimpan key di server, lalu ganti URL di fungsi `claude()` dalam `index.html`.

## Catatan soal "95%"

Hasil bergantung pada isi prompt. Prompt yang bertele-tele sering bisa turun 70-95%. Prompt yang sudah padat (banyak aturan, angka, contoh) hanya bisa turun sedikit tanpa kehilangan isi. Alat ini mendahulukan makna di atas target.

## Bahasa dan format

- **Mode AI** bekerja untuk bahasa apa pun dan campuran bahasa; AI diminta tidak menerjemahkan.
- **JSON**: jika seluruh input adalah JSON valid, hasilnya hanya di-minify (data identik, tanpa panggilan AI). JSON di tengah teks atau di dalam blok kode ``` dilindungi dan hanya di-minify, tidak pernah dikirim untuk ditulis ulang.
- **Kode, kode inline, XML/YAML/CSV di blok berpagar** dijaga persis seperti aslinya.
- **Mode Lokal** punya aturan basa-basi untuk Indonesia, Inggris, Spanyol, Prancis, Jerman, Portugis, Italia, Mandarin, Jepang, dan Korea. Bahasa lain hanya dirapikan spasinya dan dibuang kalimat gandanya.

## Opsi: padatkan teks di dalam JSON

Centang *Padatkan juga teks panjang di dalam JSON* (mode AI). Hanya nilai teks yang panjang (40 karakter ke atas dan berisi spasi) yang ditulis ulang. Kunci, angka, boolean, null, urutan, dan struktur tidak diubah. Hasil per nilai ditolak dan dikembalikan ke aslinya jika tidak lebih pendek atau jika angka, URL, atau placeholder `{x}` di dalamnya berubah. Sifatnya opsional karena isi data memang berubah; matikan jika JSON dipakai sebagai data yang harus persis.
