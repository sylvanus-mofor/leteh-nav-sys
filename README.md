# 🗺️ Leteh Navigation System

> A free, offline-capable community map for **Mmuock Leteh**, a mostly farming village in the Western Highlands of Cameroon. Built to work on low-end smartphones with intermittent internet, and designed around the way villagers actually navigate: by landmarks, not street names.

---

## 🌍 Why This Exists

Mmuock Leteh has no formal street names, no postal codes, and no presence on commercial navigation apps. Giving directions means describing what you can see — *"pass the Catholic church, continue to Agric Post, turn at the red house tree."*

This project puts the village on the map on its own terms. It is built by and for the community, works offline once loaded, and gives every resident and visitor the ability to find health facilities, schools, markets, and more without depending on a data connection.

It is entirely contained in a **single HTML file**. No server required, no app store, no install. It can be saved to a phone's home screen and used like a native app.

---

## ✨ Features

### 🗺️ Interactive Map
- OpenStreetMap tiles with offline caching via Service Worker. Tiles are viewed once then saved for future offline use
- All village places shown as colour-coded map markers by category
- Tap any marker for details, directions, and sharing options
- You can share places and directions on WhatsApp, SMS, Email, social media etc.

### 🔍 Search & Filter
- Full-text search across place names, landmark descriptions, tags and notes
- Category filter chips: Health, Market, Church, School, Home/Residence, Farmland, Palace, Financial Institution, Touristic Site, Notices, and more

### 🏘️ Quarter/Zone Labels
- Subtle area labels on the map (Ntemndzem I, Ntemndzem II, Mve, Kongho, Maleta, S'hê-Ntsi'hi) to help orient users with no street references

### 🧭 Navigation with Landmark Directions
- GPS-based routing via OpenStreetMap / OSRM
- **Local Landmark Guide** alongside every route — plain-language steps using the village's own reference points (*"Head north from Nkongle Market towards 3 Corners, then continue west about 400m. Look for: large white church building."*)

### 📅 8-Day Market Calendar
- Mmuock Leteh's traditional rotating 8-day calendar cycle: **Mboegnwa** (big market day), **Mbeugleu**, **Njungong**, **Mbeunkeu**, **Njulekhea**, **Fa'a** (small market day), **Telang**, and **Nganga'a** (no farming day)
- Today's day shown at a glance on the map; full calendar with countdown to each day
- Colour-coded: green for big market, amber for small market, purple for no-farming day

### 🌾 Farming Calendar
- Seasonal crop status and farming tips aligned to the Cameroon Western Highlands agricultural calendar (Planting / Growing & Weeding / Harvest / Dry Season)
- Per-crop status (maize, beans, groundnuts, cocoyam, plantain, vegetables) updated each month
- Practical tips and a prompt to visit the Agric Post for seeds and extension advice

### 📢 Community Notice Board
- Admin-postable announcements (Urgent / Info / Event) with optional expiry dates
- Notices auto-expire and disappear — no stale information
- Badge dot on the notice button when active notices exist

### 📍 Location & Sharing
- GPS "locate me" with accuracy circle
- Share any place via WhatsApp, SMS, or copied link
- Share your own location via link or live-share banner
- Add new places from your current GPS position

### 🌤️ Weather Forecast
- 7-day forecast from Open-Meteo (free, no API key) with farming-relevant tips
- Graceful offline fallback with typical local weather

### ✏️ Community Editing
- Any user can suggest a new place or suggest an edit to an existing one
- All suggestions go to admins for review before going live
- Admins approve or reject via a password-protected panel

### 🔒 Admin Panel
- Password-protected (SHA-256 hashed) with session memory
- Approve/reject community submissions, delete live places, post notices, view statistics
- Reset to seed data if needed

### 📡 Offline-First
- Service Worker caches all map tiles as they are viewed
- All core functionality (map, search, calendar, notices, weather fallback) works without internet after first load
- Single-file architecture — the entire app is one `.html` file, shareable via WhatsApp

---

## 🏗️ Architecture

```
leteh_nav_sys.html   ← The entire application (HTML + CSS + JS, ~3000 lines of code)
README.md
```

**Dependencies (all loaded from CDN, cached by Service Worker):**
- [Leaflet.js](https://leafletjs.com/) — map rendering
- [Leaflet Routing Machine](https://www.lrouter.graphhopper.com/) — turn-by-turn routing
- [OpenStreetMap](https://www.openstreetmap.org/) — map tiles
- [Open-Meteo](https://open-meteo.com/) — weather API (no key required)
- [DM Sans / DM Mono](https://fonts.google.com/) — typography

**No backend. No database. No build step. No environment variables.**

Data is stored in the browser's `localStorage`. The seed data (all known places) lives directly in the JS as a `SEED` array and is versioned. Bumping the version string forces all users to reload the latest seed on next visit.

---

## 🚀 Getting Started

### Use it now
Open `leteh_nav_sys.html` in any modern browser. That's it.

To use on a phone:
1. Open the file in Chrome or Safari
2. Tap the browser menu → **"Add to Home Screen"**
3. Use it like an app, with or without internet

### Run locally
```bash
git clone https://github.com/sylvanus-mofor/leteh-nav-sys.git
cd leteh-nav-sys
# Open leteh_nav_sys.html in your browser
# OR serve with any static server:
npx serve .
```

### Admin access
The admin panel is accessible via the ⚙️ button. The default password is set as a SHA-256 hash in the `ADMIN_HASH` constant. New admins are given the password.
---

## 🤝 Community & Contributing

This project was built for Mmuock Leteh but the architecture can serve **any rural community** that lacks formal addressing, has intermittent connectivity, and navigates by landmarks.

I am actively looking for:

- **Village contributors**: residents who can verify, add, and improve place data
- **Developers**: to help extend features, improve offline capability, and adapt the system for other villages
- **UX/design partners**: To make the interface even simpler for low literacy and first-time smartphone users
- **NGOs and development organisations**: Who work in rural digital inclusion and see value in this approach
- **Translators**: To add French (the app is currently English-only; Cameroon is officially bilingual)
- **Other communities**: Who want to fork and adapt this for their own village

### How to contribute

1. **Fork** this repository
2. **Create a branch** for your feature or fix: `git checkout -b feature/my-improvement`
3. **Make your changes** — the entire app is one file, so it's easy to get started
4. **Test** by opening the file in a browser
5. **Submit a Pull Request** with a clear description of what you changed and why

### Good first contributions
- Add missing places to the `SEED` array (coordinates, landmark descriptions, opening hours)
- Translate UI strings to French
- Improve the landmark direction algorithm to use more local reference points
- Add a `name_fr` field to all seed entries for bilingual display
- Improve accessibility (screen reader support, larger tap targets)
- Add a "copy directions as SMS text" button for sharing without internet
- Pre-cache tile loading (pan around village bounds automatically when online)

### Reporting issues
Please open a GitHub Issue with:
- What you expected to happen
- What actually happened
- Your browser and device (e.g. Chrome on Android, Safari on iPhone)

---

## 🌱 Vision

My long term vision is a **network of village maps** across rural Cameroon and beyond with each community owning its own. Each adapted to local language, place names and cultural context, all sharing the same open-source foundation.

I believe that communities who have been left off the map deserve to define their own geography, in their own language, using their own landmarks, on their own terms.

If you share that belief, I'd love to hear from you.

---

## 📄 Licence

This project is open source under the [MIT Licence](LICENSE). You are free to use, copy, modify, and distribute it with atribution. Not for commercial use.

---

## 🙏 Acknowledgements

- The community of **Mmuock Leteh**, Cameroon, for the knowledge, place names, and patience that made this possible
- [OpenStreetMap contributors](https://www.openstreetmap.org/copyright) for the map data
- [Open-Meteo](https://open-meteo.com/) for free weather data
- [Leaflet](https://leafletjs.com/) and the open-source mapping community

---

*Built with love for a village that deserves to be on the map*
