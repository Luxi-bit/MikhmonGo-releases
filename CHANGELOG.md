# Changelog

🇬🇧 English · 🇮🇩 [Bahasa Indonesia](CHANGELOG.id.md)

## v1.0.0 — Initial Release

Flutter app for managing MikroTik routers (Hotspot & PPP) directly from Android — no intermediary web server required.

### Key features

- **Multi-router** — save multiple router profiles, switch without re-entering credentials. "Check Login URL" button auto-fetches from the router's hotspot profile.
- **Dashboard** — live stats: resource usage (CPU/RAM/HDD), hotspot active/total, PPP active/total, uptime, real-time traffic monitor.
- **Hotspot & PPP** — manage users, generate vouchers, active sessions, hosts, profiles, secrets.
- **Voucher printing**
  - Multi-design A4 PDF (Default, Modern Card, Elegant) via the Template Editor — per-profile colors, logo, pricing, auto-login QR code.
  - **Quick Print** — print a 58mm thermal receipt straight to a Bluetooth printer (ESC/POS), including a scan-to-login QR code.
- **Sales Report** — transaction summary, daily trend chart, per-profile breakdown, PDF export.
- **Telegram notifications** — router reports/alerts to a Telegram bot.
- **App-level security** — optional app login lock, separate from router credentials.

### Notable fixes (Bluetooth thermal printing)

- Fixed an instant crash on Test Print/Quick Print — the `BLUETOOTH_SCAN` runtime permission was never requested (required internally by the printer plugin on Android 12+).
- Fixed a false "printer not connected" error when tried right after opening the app — the Bluetooth connection is now polled instead of waited-on-once.
- Fixed a false "success" message — printing now waits for the printer to actually finish detecting its command set (ESC/TSC/CPCL) before sending data.
- The thermal receipt's QR code now follows the "Show QR Code" toggle in the Template Editor, same as the PDF path.

### About screen & Sales Report CSV export

- New "About App" menu (Settings) — app version, "Check for Updates"
  (queries this repo's latest GitHub release), "What's New" (shows this
  changelog), and a link to this repo.
- Sales Report's History tab now has a CSV export button next to the
  existing PDF export.

### Build hardening & size

- Native Java/Kotlin code (including the printer plugin) is minified & obfuscated (R8/ProGuard).
- Dart code is obfuscated (`--obfuscate --split-debug-info`) — original class/function names are no longer readable straight from the APK.
- Verified on physical hardware: dashboard, router connection, and Bluetooth thermal printing all still work correctly after hardening.
- Oversized image assets shrunk (a 1.5MB image displayed at a max of
  104dp, and a duplicate unused splash image) — saved ~2.4MB.
- APKs are now published split per CPU architecture — the recommended
  `arm64` download is ~25MB vs. a `universal` build's ~64MB.

### Requirements

Android 8.0 (API 26) or newer · a MikroTik router with RouterOS API enabled (default port `8728`).
