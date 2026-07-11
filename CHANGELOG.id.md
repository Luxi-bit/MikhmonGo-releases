# Changelog

🇬🇧 [English](CHANGELOG.md) · 🇮🇩 Bahasa Indonesia

## v1.1.0

### Baru

- **Settings → Appearance**: pilih tema aplikasi (System / Light / Dark), bahasa aplikasi (System / Indonesia / English — "System" mengikuti bahasa HP, fallback ke English), dan slider ukuran tampilan manual (90%–110%).
- **Share Voucher as Image**: bagikan voucher yang baru dibuat, atau user yang sudah ada (lewat menu ⋮ di User List), sebagai gambar kartu — kode, harga, masa berlaku, QR code auto-login, dan logo Template Editor kalau ada — langsung ke share sheet Android. Jual voucher lewat WhatsApp/Telegram tanpa perlu cetak.
- Search bar collapsible di layar daftar (User List, PPP Secret/Profile/Active, Hotspot Hosts, User Profile, Vouchers, Sales Report, Quick Print) — disembunyikan di balik ikon search, bukan selalu tampil.
- Animasi entrance untuk daftar router di layar Sessions.

### Diubah

- Settings di-redesign: tiap item sekarang punya card bergaris sendiri dengan sedikit jarak, tidak lagi dikelompokkan dengan header section polos.
- Notifikasi in-app (snackbar) di-redesign di seluruh app jadi pill mengambang dengan ikon status berwarna (hijau/merah/oranye).
- Hint "Tekan sekali lagi untuk keluar" di-redesign ke gaya pill mengambang yang sama.
- Tema aplikasi sekarang default mengikuti setelan light/dark HP saat instal baru.
- Tombol app bar diurutkan ulang (search → filter → refresh); tombol filter tidak lagi hilang saat sedang mencari, dan hanya menyala kalau ada filter asli, bukan sekadar kata kunci pencarian.
- Splash screen awal di-redesign sesuai ikon/tema aplikasi, dengan durasi tampil yang konsisten di semua device.
- Daftar navigasi app drawer sekarang bisa di-scroll; Disconnect jadi tombol merah terpisah di bawah Settings.
- Badge "Online" di Dashboard dipindah ke pojok kanan atas kartu router.

### Diperbaiki

- Crash saat startup di beberapa device (ditemukan di Huawei EMUI), disebabkan oleh tema native splash screen.
- Error "invalid user name or password" yang jarang muncul setelah percobaan login ulang gagal, disebabkan koneksi ke router yang bocor dan tidak pernah tertutup dengan benar.
- Ikon/warna status bar sekarang sesuai dengan tema light/dark aplikasi, termasuk saat ganti tema secara live.
- Tombol back Android sekarang menutup search field yang terbuka terlebih dahulu, konsisten di semua layar daftar.
- Pindah tab di tengah pencarian tidak lagi meninggalkan daftar yang diam-diam masih terfilter kata kunci lama.
- Bahasa "Ikuti Sistem" sekarang benar-benar mengecek ulang bahasa HP setiap kali aplikasi dibuka.
- Slider ukuran tampilan sekarang hanya menyimpan sekali saat dilepas, bukan setiap gerakan kecil saat drag.
- Suhu Dashboard sekarang menampilkan satuan yang benar ("45°C") di semua router.
- Menghapus jarak berlebih antar-filter di daftar transaksi Laporan Penjualan.

### Requirement

Android 8.0 (API 26) ke atas · router MikroTik dengan RouterOS API aktif (port default `8728`).

## v1.0.0 — Rilis Awal

Aplikasi Flutter untuk mengelola router MikroTik (Hotspot & PPP) langsung dari Android, tanpa perlu web server perantara.

### Fitur utama

- **Multi-router** — simpan banyak profil router, pindah antar router tanpa input ulang kredensial. Tombol "Check Login URL" auto-fetch dari hotspot profile router.
- **Dashboard** — statistik live: resource (CPU/RAM/HDD), hotspot active/total, PPP active/total, uptime, traffic monitor real-time.
- **Hotspot & PPP** — kelola user, generate voucher, sesi aktif, host, profil, secret.
- **Cetak voucher**
  - PDF A4 multi-desain (Default, Modern Card, Elegan) lewat Template Editor — warna per profil, logo, harga, QR code login otomatis.
  - **Quick Print** — cetak struk thermal 58mm langsung ke printer Bluetooth (ESC/POS), termasuk QR code scan-to-login.
- **Laporan Penjualan** — rekap transaksi, grafik tren harian, breakdown per profil, export PDF.
- **Notifikasi Telegram** — laporan/alert router ke bot Telegram.
- **Keamanan aplikasi** — opsi kunci login aplikasi terpisah dari kredensial router.

### Perbaikan penting (cetak thermal Bluetooth)

- Fix crash instan saat Test Print/Quick Print — permission `BLUETOOTH_SCAN` yang sebelumnya tidak pernah diminta saat runtime (dibutuhkan plugin printer secara internal di Android 12+).
- Fix "printer belum terhubung" yang salah muncul kalau dicoba tepat setelah app baru dibuka — koneksi Bluetooth sekarang di-poll, bukan tunggu tetap.
- Fix "berhasil" palsu — print sekarang menunggu printer benar-benar selesai deteksi jenis command (ESC/TSC/CPCL) sebelum mengirim data.
- QR code pada struk thermal sekarang mengikuti toggle "Tampilkan QR Code" di Template Editor, sama seperti jalur PDF.

### Menu About & Export CSV Laporan Penjualan

- Menu baru "Tentang Aplikasi" (Settings) — versi aplikasi, "Cek
  Pembaruan" (memeriksa rilis terbaru di repo ini), "Yang Baru"
  (menampilkan changelog ini), dan link ke repo ini.
- Tab History di Laporan Penjualan sekarang punya tombol export CSV di
  sebelah tombol export PDF yang sudah ada.

### Keamanan & ukuran build

- Kode Java/Kotlin native (termasuk plugin printer) di-minify & di-obfuscate (R8/ProGuard).
- Kode Dart di-obfuscate (`--obfuscate --split-debug-info`) — nama class/fungsi asli tidak lagi terbaca langsung dari APK.
- Sudah diverifikasi di device fisik: dashboard, koneksi router, dan cetak thermal Bluetooth tetap berfungsi normal setelah hardening.
- Aset gambar yang kegedean diperkecil (satu gambar 1.5MB yang cuma
  ditampilkan maks 104dp, dan satu gambar splash duplikat yang tidak
  terpakai) — hemat ~2.4MB.
- APK sekarang dipublikasikan terpisah per arsitektur CPU — unduhan
  `arm64` yang direkomendasikan cuma ~25MB dibanding `universal` ~64MB.

### Requirement

Android 8.0 (API 26) ke atas · router MikroTik dengan RouterOS API aktif (port default `8728`).
