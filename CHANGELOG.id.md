# Changelog

🇬🇧 [English](CHANGELOG.md) · 🇮🇩 Bahasa Indonesia

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

### Keamanan build

- Kode Java/Kotlin native (termasuk plugin printer) di-minify & di-obfuscate (R8/ProGuard).
- Kode Dart di-obfuscate (`--obfuscate --split-debug-info`) — nama class/fungsi asli tidak lagi terbaca langsung dari APK.
- Sudah diverifikasi di device fisik: dashboard, koneksi router, dan cetak thermal Bluetooth tetap berfungsi normal setelah hardening.

### Requirement

Android 8.0 (API 26) ke atas · router MikroTik dengan RouterOS API aktif (port default `8728`).
