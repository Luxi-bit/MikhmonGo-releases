# Changelog

🇬🇧 English · 🇮🇩 [Bahasa Indonesia](CHANGELOG.id.md)

## v1.1.0

### New

- **Settings → Appearance**: choose app theme (System / Light / Dark), app language (System / Indonesian / English — "System" follows your phone's language, falling back to English), and a manual display size slider (90%–110%).
- **Share Voucher as Image**: share a freshly generated voucher, or any existing user (via the ⋮ menu in User List), as a card image — code, price, validity, an auto-login QR code, and your Template Editor logo if you have one — straight to the Android share sheet. Sell vouchers over WhatsApp/Telegram without printing anything.
- Collapsible search bar on list screens (User List, PPP Secret/Profile/Active, Hotspot Hosts, User Profile, Vouchers, Sales Report, Quick Print) — hidden behind a search icon instead of always shown.
- Entrance animation for the router list on the Sessions screen.

### Changed

- Settings redesigned: each item now sits in its own bordered card with breathing room, instead of grouped under plain text section headers.
- In-app notifications (snackbars) redesigned app-wide into a compact floating pill with a colored status icon (green/red/orange).
- The "Press back again to exit" hint redesigned into the same floating pill style.
- App theme now defaults to following your phone's system light/dark setting on a fresh install.
- App bar buttons reordered (search → filter → refresh); the filter button no longer disappears while searching, and only highlights for an actual filter, not just a search query.
- Startup splash screen redesigned to match the app icon/theme, with a consistent hold duration on every device.
- App drawer's navigation list is now scrollable; Disconnect is a separate red button below Settings.
- Dashboard's "Online" badge moved to the top-right corner of the router card.

### Fixed

- Crash on startup on some devices (observed on Huawei EMUI), caused by the native splash screen theme.
- Rare "invalid user name or password" error after a failed login retry, caused by a leaked router connection that was never properly closed.
- Status bar icons/colors now correctly match the app's light/dark theme, including live theme switches.
- Android back button now closes an open search field first, consistently across every list screen.
- Switching tabs mid-search no longer leaves the list silently filtered on the old query.
- "Follow System" language now re-checks your phone's language every time the app is opened.
- Display size slider now saves only once released, instead of on every drag movement.
- Dashboard temperature now shows a proper unit ("45°C") on every router.
- Removed an oversized gap between filters on Sales Report's transaction list.

### Requirements

Android 8.0 (API 26) or newer · a MikroTik router with RouterOS API enabled (default port `8728`).

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
