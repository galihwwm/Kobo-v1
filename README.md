# KOBO — Belajar Koperasi Bareng Bao di Kerbau

Aplikasi gamifikasi literasi koperasi yang dikembangkan untuk
**Hackathon Digital Cooperatives Expo 2026 — Pilar 4: Literasi Gen-Z & Gen-Alpha dalam Berkoperasi**.

KOBO mengajarkan materi dasar-dasar koperasi (definisi, simpanan, SHU, hingga koperasi digital)
dengan format yang akrab bagi generasi muda: pelajaran singkat, kuis interaktif, XP, streak,
nyawa (hearts), dan lencana.

> **Status: Minimum Viable Product (MVP) / prototipe demo.**

🔗 **Coba langsung:** https://galihwwm.github.io/Kobo-v1/

---

## 👥 Tim

| Peran | Nama |
|-------|------|
| Nama Tim | _CIA-14_ |
| Ketua | _Galih Wening Werdi Mukti_ |
| Anggota 1 | _Asriza Yolanda_ |
| Anggota 2 | _Monike Febrianti_ |

---

## 🎯 Relevansi dengan Tema Pilar 4

Pilar 4 menyoroti **literasi Gen-Z & Gen-Alpha dalam berkoperasi**. KOBO menjawabnya dengan dua cara:
pertama, **gamifikasi** mengubah materi koperasi yang sering dianggap kuno menjadi pengalaman belajar
yang ringan dan menyenangkan, sesuai kebiasaan digital generasi muda. Kedua, **jembatan ke aksi nyata** —
usai belajar, pengguna langsung diarahkan ke daftar koperasi yang bisa diikuti. Dengan begitu KOBO tidak
berhenti pada literasi, tetapi mendorong partisipasi nyata: dari *belajar -> paham -> bergabung*.

---

## ✨ Fitur

- **Pembelajaran bertingkat** — 4 unit pembelajaran dengan mode terkunci/terbuka antar tingkat.
- **3 tipe soal interaktif**: pilihan ganda, benar/salah, dan mencocokkan pasangan.
- **Gamifikasi**: XP, streak harian, sistem nyawa (❤️), dan lencana yang bisa di-unlock.
- **🌉 Jembatan ke aksi nyata**: setiap selesai pelajaran, muncul ajakan + mini-katalog koperasi
  *(saat ini berupa data contoh/simulasi — lihat Keterbatasan)*. Ini mengubah "belajar" menjadi
  dorongan untuk "ikut bergabung".
- **🎓 Sertifikat kelulusan**: setelah semua unit selesai, pengguna membuat sertifikat ber-nama dengan
  gelar "Sahabat Koperasi" yang bisa diunduh (.png) dan dibagikan ke media sosial.
- **Maskot "Bao"** — Bao si kerbau memandu dan memberi umpan balik tiap soal. Kerbau dipilih sebagai
  simbol kerja keras dan gotong royong yang identik dengan pertanian Indonesia — sekaligus pembeda dari
  aplikasi belajar lain.
- **Progres tersimpan otomatis** di perangkat (localStorage) — lanjut kapan saja.
- **100% offline & tanpa backend** — cukup file statis.
- **Responsif** (mobile-first) dan mendukung `prefers-reduced-motion`.

## 🆚 Yang Membedakan KOBO

Aplikasi belajar gamifikasi pada umumnya berhenti pada penyampaian teori. KOBO melangkah lebih jauh
dengan **menghubungkan edukasi ke aksi nyata**: di akhir tiap pelajaran, pengguna disuguhi daftar koperasi
beserta jenis, lokasi, layanan, dan syarat keanggotaan yang bisa dicari dan disaring. Inilah inti
diferensiasi KOBO — pengetahuan baru langsung dikaitkan dengan peluang konkret untuk menjadi anggota koperasi.

## 🚀 Cara Menjalankan

**Paling cepat:** buka file `index.html` di browser (double-click).
> Catatan: lewat double-click, aplikasi memakai **data bawaan** dan perubahan pada file JSON tidak
> akan terlihat. Untuk memuat JSON, jalankan via server (lihat **Catatan Teknis** di bawah).

**Via server lokal (disarankan):**
```bash
python3 -m http.server 8000
# lalu buka http://localhost:8000
```

## 🌐 Deploy ke GitHub Pages

1. Push repo ini ke GitHub.
2. Buka **Settings -> Pages**.
3. Bagian *Source* pilih branch `main`, folder `/ (root)`, lalu **Save**.
4. Tunggu ±1 menit, aplikasi tersedia di `https://<username>.github.io/<nama-repo>/`.

## 🧱 Teknologi

HTML, CSS, dan JavaScript murni (vanilla). **Tanpa** framework, **tanpa** build step, **tanpa** dependensi.
Font dimuat dari Google Fonts (butuh internet untuk tampilan font terbaik).

## 📁 Struktur

```
.
├── index.html     # aplikasi (UI + logika). Berisi data fallback bawaan.
├── lessons.json   # 📚 materi pelajaran — edit di sini untuk menambah/ubah soal
├── coops.json     # 🏪 data katalog koperasi — edit di sini untuk menambah koperasi
├── README.md
└── LICENSE
```

> **Konten terpisah dari kode.** Materi & data koperasi dimuat dari `lessons.json` dan `coops.json`
> saat aplikasi start. Tim non-programmer bisa menambah konten hanya dengan mengedit file JSON —
> tanpa menyentuh `index.html`.

## ✏️ Cara Menambah Materi

### Menambah/mengubah pelajaran — `lessons.json`

Berisi daftar unit. Setiap unit punya `id`, `title`, `icon`, dan daftar `questions`.
Tersedia 3 tipe soal:

```jsonc
// Pilihan ganda
{ "type":"mc", "prompt":"Pertanyaan?", "hint":"opsional",
  "options":["A","B","C","D"], "answer":0,  // index jawaban benar (mulai 0)
  "explain":"Penjelasan setelah dijawab." }

// Benar / salah
{ "type":"tf", "prompt":"Judul soal",
  "statement":"Pernyataan yang dinilai.", "answer":true,
  "explain":"Penjelasan." }

// Mencocokkan pasangan
{ "type":"match", "prompt":"Pasangkan!",
  "pairs":[ {"l":"Kiri","r":"Kanan"}, {"l":"...","r":"..."} ],
  "explain":"Penjelasan." }
```

Field opsional: `bubble` (teks dari maskot Bao 🐃) dan `hint`.

### Menambah koperasi — `coops.json`

```jsonc
{ "name":"Nama Koperasi", "type":"Konsumen",
  "area":"Kecamatan, Kota", "services":["Layanan 1","Layanan 2"],
  "member":"Syarat keanggotaan", "emoji":"🏪" }
```

> ⚠️ Setelah mengedit, pastikan JSON tetap valid (mis. cek di jsonlint.com).
> Jalankan lewat GitHub Pages atau server lokal agar JSON termuat.

## ⚙️ Catatan Teknis: file:// vs server

Browser **memblokir `fetch()` saat file dibuka langsung** (double-click -> `file://`). Artinya:

- **Di GitHub Pages / server lokal:** `lessons.json` & `coops.json` dimuat normal. ✅
- **Saat double-click `index.html`:** aplikasi tetap jalan, tapi memakai **data fallback bawaan**
  di dalam `index.html` (perubahan JSON tidak terlihat). ⚠️

Untuk menguji perubahan JSON di lokal, jalankan server kecil:

```bash
python3 -m http.server 8000   # lalu buka http://localhost:8000
```

## 🗺️ Kurikulum (dummy)

| Unit | Topik |
|------|-------|
| 1 | Kenalan sama Koperasi (definisi, 1 anggota 1 suara) |
| 2 | Simpanan & Modal (pokok, wajib, sukarela) |
| 3 | Rahasia SHU (Sisa Hasil Usaha, RAT) |
| 4 | Koperasi Zaman Now (digitalisasi) |

## ⚠️ Keterbatasan & Catatan

- **Materi & data koperasi bersifat contoh (dummy)** untuk demo. Sebelum digunakan, perlu
  **verifikasi setiap materi** dengan sumber resmi seperti **UU No. 25 Tahun 1992 tentang
  Perkoperasian** dan regulasi terbaru. Daftar koperasi di mini-katalog juga dummy dan perlu
  dihubungkan ke data koperasi resmi & terverifikasi.
- **Belum berbasis lokasi nyata.** Label "koperasi terdekat" masih konsep; MVP belum memakai
  geolokasi (GPS), melainkan menampilkan daftar contoh.
- **Belum ada autentikasi/akun**, multi-pengguna, atau sinkronisasi cloud. Progres hanya tersimpan
  di satu browser/perangkat.
- **Streak dihitung sederhana** berdasarkan tanggal kalender perangkat; bisa "dicurangi" dengan
  mengubah jam sistem. Bukan untuk produksi.
- **Belum ada fitur sosial** (leaderboard, komunitas) — peluang pengembangan lanjutan.

## 🔭 Ide Pengembangan Lanjutan

- **Integrasi data koperasi resmi** — menggantikan data dummy dengan sumber terverifikasi.
- **Leaderboard & tantangan antar-teman** — memperkuat aspek komunitas digital.
- **Mode kontributor** — antarmuka bagi koperasi/dinas untuk menambah materi tanpa menyentuh kode.
- **Akun pengguna + sinkronisasi** — via backend ringan atau layanan BaaS.
- **Audio & aksesibilitas tambahan** untuk jangkauan lebih luas.

## 📄 Lisensi

MIT — lihat berkas [LICENSE](LICENSE).
