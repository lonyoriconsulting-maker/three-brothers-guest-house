# Three Brothers Guest House — Tracker

A single-page, installable PWA (Progressive Web App) for running the day-to-day
operations of Three Brothers Guest House in Morogoro, Tanzania: rooms, bookings,
restaurant, income/expenses, inventory, and staff payroll — fully offline.

Built by **LERO Systems / Consulting**.

---

## Features

- **Rooms** — 11 guest rooms (numbers 2–9, 21–23) plus a dedicated staff room, with status (vacant / occupied / cleaning)
- **Bookings** — check-in/out, guest name, phone, nights, amount, paid status
- **Restaurant** — menu management, orders, daily sales. Alcohol-free by design (menu form and UI both flag "No Alcohol")
- **Money** — expenses (with optional receipt photo), other income, and a rolling Today / This Week / This Month summary
- **Scan Receipt** — camera capture + on-device OCR (Tesseract.js) to pull amounts off printed receipts; falls back to manual entry if offline on first use or handwriting isn't recognized
- **Inventory** — stock levels by category (Rooms / Kitchen / General), low-stock warnings, optional photo
- **Staff & Payroll** — base salary, allowances, advances/emergency payouts (food, transport, family emergency, other), running "owed this month" balance per staff member
- **Reports** — Today / Week / Month breakdown by income source and expense category, with CSV export
- **Calculator** — floating quick-access calculator from any screen
- **Backup/Restore** — one-tap JSON export/import, since all data lives on-device only

## Tech

- Vanilla JS, no build step, no framework — a single `index.html`
- **IndexedDB** for storage (all data stays on the phone; nothing is sent online)
- **Service Worker** (`sw.js`) caches the app shell for full offline use after first load
- **Tesseract.js** (loaded from CDN, cached after first successful use) for receipt OCR
- Installable as a home-screen app via the browser's "Add to Home Screen" / "Install app" prompt

## File structure

```
three-brothers/
├── index.html          All UI, styles, and app logic
├── manifest.json        PWA manifest (name, icons, theme)
├── sw.js                 Service worker (offline caching)
├── icon.svg              Source logo (three roof peaks over a doorway)
└── icons/
    ├── icon-32.png        Favicon
    ├── icon-180.png        Apple touch icon
    ├── icon-192.png        Android home screen icon
    └── icon-512.png        Splash / maskable icon
```

## Deploy (GitHub Pages)

1. Create a new repo, e.g. `three-brothers-guest-house`, under `lonyoriconsulting-maker`
2. Upload all files above, **keeping the folder structure** (the `icons/` folder must stay a folder)
3. In repo Settings → Pages, set the source to the `main` branch, root folder
4. Share the resulting `https://lonyoriconsulting-maker.github.io/three-brothers-guest-house/` URL

On first visit, Chrome will offer "Install app" (Android) or "Add to Home Screen" (iOS Safari).

## Notes on room numbers

Guest rooms are seeded as **2, 3, 4, 5, 6, 7, 8, 9, 21, 22, 23** plus one **Staff Room**
(excluded from guest booking options and from the occupancy stat on the dashboard).
This seeding only runs once, the first time the app opens with an empty database —
editing `GUEST_ROOM_NUMBERS` in `index.html` after that won't retroactively change
existing installs; use the Rooms tab's Edit button instead.

## Known limitations

- **OCR needs one internet connection the first time** a receipt is scanned (to download
  the ~2MB Tesseract engine). After that, scanning works fully offline. The app shows a
  manual-entry fallback if that first download hasn't happened yet.
- OCR is unreliable on **handwritten** receipts — it's built and tested against printed
  text. For handwritten tallies, use manual entry (the photo is still attached as proof).
- Data lives only on the device it was entered on. Use **Settings → Download Backup**
  weekly and send the file off-device (e.g. via WhatsApp) as a safety net.

## Support

Maintained remotely from Arusha. For issues or feature requests, contact LERO Systems / Consulting.
