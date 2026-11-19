# 📚 Jurnal Pustakawan

Aplikasi web sederhana untuk pustakawan sekolah: mencatat pekerjaan harian, to-do bertenggat, agenda, dan register arsip internal. Berjalan sepenuhnya di browser (tanpa server, tanpa akun), dan dapat dipasang gratis lewat GitHub Pages.

## Fitur

| Menu | Kegunaan |
|---|---|
| **Beranda** | Dashboard: ringkasan angka, grafik 7 hari, status dan kategori bulan ini, pengingat tenggat, agenda 7 hari ke depan |
| **Jurnal** | Catat beberapa pekerjaan sekaligus untuk satu tanggal, saran otomatis dari pekerjaan sebelumnya, filter, cari, edit, hapus |
| **To-do** | Pekerjaan bertenggat dengan penanda terlambat / segera; tombol "Ke jurnal" |
| **Kalender** | Tampilan bulanan: jurnal, tenggat to-do, arsip, dan **agenda** (bisa beberapa hari) |
| **Rekap** | Rekap per bulan, tahun, atau rentang tanggal; pilih tanggal yang dicetak; kop dan tanda tangan; cetak / simpan PDF; unduh CSV |
| **Arsip** | Register arsip fisik dan digital: nomor otomatis, jenis, lokasi, status, peminjaman, status unggah ke Drive, tautan Drive |
| **Kategori** | Kelola kategori pekerjaan, jenis arsip (beserta kodenya), dan kode lokasi |
| **Cadangan** | Unduh / pulihkan data (JSON), unduh tabel (CSV) |

## Struktur repositori

```
jurnal-pustakawan/
├── index.html            ← seluruh aplikasi (HTML + CSS + JavaScript dalam satu file)
├── manifest.webmanifest  ← identitas aplikasi untuk dipasang di layar utama (PWA)
├── sw.js                 ← service worker: membuat aplikasi bisa dibuka tanpa internet
├── icon.svg              ← ikon aplikasi
├── README.md             ← dokumen ini
└── .gitignore            ← mencegah file cadangan data ikut ter-commit (opsional)
```

Logika aplikasi sengaja dibuat dalam satu file (`index.html`) agar mudah diunggah dan diperbarui. Tiga file lainnya hanya untuk mode PWA.

## Memasang di GitHub Pages

1. Buat repositori baru di GitHub (misalnya `jurnal-pustakawan`).
2. Klik **Add file → Upload files**, lalu unggah `index.html`, `manifest.webmanifest`, `sw.js`, `icon.svg`, dan `README.md` (serta `.gitignore` bila ada). Klik **Commit changes**.
3. Buka **Settings → Pages**.
4. Pada **Source**, pilih **Deploy from a branch**. Pilih branch `main` dan folder `/ (root)`, lalu **Save**.
5. Tunggu 1–3 menit. Alamat aplikasi akan tampil di halaman yang sama, berbentuk `https://NAMA-AKUN.github.io/jurnal-pustakawan/`.

> Pada akun GitHub gratis, repositori perlu berstatus **Public** agar bisa memakai Pages. Lihat bagian Privasi di bawah.

## Memperbarui aplikasi

Unggah ulang `index.html` dengan nama yang sama (**Add file → Upload files**, GitHub akan menimpa file lama). Aplikasi mengambil versi terbaru saat perangkat online. Bila Anda mengubah `manifest.webmanifest`, `icon.svg`, atau `sw.js`, naikkan nomor versi `CACHE` di dalam `sw.js` (misalnya `jurnal-pustakawan-v2`). Data Anda tidak terpengaruh karena tersimpan di browser, bukan di repositori. Bila tampilan belum berubah, muat ulang halaman dengan menekan Ctrl+F5 (di HP: tutup dan buka kembali tab).

## Mode PWA (dipasang dan offline)

- Setelah dibuka lewat alamat `https://...github.io/...`, aplikasi dapat dipasang: **Android (Chrome)** menu ⋮ → *Instal aplikasi*; **komputer (Chrome/Edge)** ikon pasang di kolom alamat; **iPhone (Safari)** Bagikan → *Tambah ke Layar Utama*. Menu **Cadangan** juga memuat tombol pasang bila browser mendukung.
- Setelah dibuka sekali saat online, aplikasi tetap bisa dibuka tanpa internet.
- Di Android, aplikasi yang dipasang memakai data yang sama dengan browser untuk alamat yang sama. Di iPhone, data aplikasi di layar utama **terpisah** dari Safari, jadi pindahkan lewat menu **Cadangan**.
- Service worker hanya aktif di alamat `https` (GitHub Pages sudah https) atau `localhost`, bukan saat file dibuka langsung dari folder.

## Data dan cadangan (penting)

- Semua data tersimpan di **penyimpanan browser** (localStorage) pada perangkat yang dipakai.
- Data **terikat pada alamat web** aplikasi. Bila nama repositori atau akun GitHub diganti, alamatnya berubah dan data lama tidak terlihat. Pulihkan lewat menu **Cadangan**.
- Data tidak otomatis sinkron antar perangkat. Untuk berpindah perangkat: **Cadangan → Unduh cadangan (JSON)**, lalu **Pulihkan dari file** di perangkat baru.
- Membersihkan data situs / cache browser akan menghapus data. **Unduh cadangan secara berkala**, misalnya seminggu sekali, dan simpan di Google Drive atau flashdisk.

## Privasi dan keamanan

- Kode aplikasi di repositori publik dapat dilihat siapa saja, tetapi **data Anda tidak ikut terunggah** ke GitHub.
- **Jangan mengunggah file cadangan (`.json` / `.csv`) ke repositori publik.** Berkas `.gitignore` membantu bila Anda memakai Git, tetapi unggahan lewat web tidak tersaring otomatis.
- Halaman diberi tanda `noindex` agar tidak ditampilkan mesin pencari. Alamatnya tetap dapat dibuka siapa pun yang mengetahuinya, jadi jangan menaruh data rahasia di aplikasi ini.
- Bila perangkat dipakai bersama, setiap pengguna browser yang sama dapat melihat datanya.

## Catatan teknis

- Teknologi: HTML, CSS, dan JavaScript murni (tanpa framework dan tanpa proses build).
- Font Nunito dimuat dari Google Fonts. Tanpa internet, tampilan memakai font bawaan perangkat.
- Mencetak rekap: menu **Rekap → Cetak / simpan PDF**, lalu pilih "Simpan sebagai PDF" di dialog cetak (ukuran A4).
- Telah dirancang untuk browser modern (Chrome, Edge, Firefox, Safari versi terbaru) di komputer maupun HP.

## Riwayat versi

| Versi | Isi |
|---|---|
| 1.0 | Jurnal, To-do, Kalender dan agenda, Rekap dengan template cetak, Arsip (nomor otomatis, status unggah Drive, peminjaman), Kategori, Cadangan |
| 1.1 | Mode PWA: dapat dipasang di layar utama dan dibuka tanpa internet |

## Rencana pengembangan

- Pengingat cadangan di Beranda
- To-do dan agenda berulang
