# 🗺️ MapReaper — GeoGuessr & RussiaGuesser Helper Tool

<p align="center">
  <img src="https://readme-typing-svg.demolab.com?font=Inter&weight=700&size=28&pause=1000&color=ff3b3b&center=true&vCenter=true&width=700&lines=MapReaper+Extension;GeoGuessr+Location+Analyzer;Coordinate+Extraction+Tool;Built+for+Map+Verification" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Version-1.0.5-ff3b3b?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Status-Active-00ff88?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Platform-Chrome%20%7C%20Edge-1f6feb?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/License-All%20Rights%20Reserved-black?style=for-the-badge"/>
</p>

---

<p align="center">
  <img src="https://s10.iimage.su/s/24/gKnfZp8xXR2ILQGzUX5m184U1kzzELvIRtp2uqwaW.png" width="360"/>
</p>

<p align="center">
  <a href="https://github.com/psybladerrr/MapReaper-Geoguessr/tree/main#-installation">
    <img src="https://img.shields.io/badge/⬇%20DOWNLOAD-LATEST%20VERSION-0ff?style=for-the-badge&logo=github&logoColor=0ff&labelColor=000000" alt="Download"/>
  </a>
</p>

---

## 📖 What is MapReaper?

**MapReaper** is a powerful browser extension that intercepts and displays exact coordinates from GeoGuessr and RussiaGuessr games. Originally designed as an administrative tool for map verification, it provides:

- 📍 **Real-time coordinate extraction** from Google Street View API
- 🗺️ **Interactive map display** with precise location markers
- 🌐 **Detailed location information** (country, city, street, etc.)
- 🎨 **Modern dark interface** with smooth animations
- 💾 **Persistent settings** across sessions

> **Note**: This tool is intended for educational purposes, map verification, and administrative use. Users are responsible for compliance with platform terms of service.

---

## 🎬 Preview

### 🌍 GeoGuessr Mode

<p align="center">
  <img src="https://s10.iimage.su/s/24/gZSDswcx9tP5eDRXoCRqccw8ojf2MfcNt8HArqPzw.png" width="600"/>
  <br><i>Main interface with "Where?" button</i>
</p>

<p align="center">
  <img src="https://s10.iimage.su/s/25/gVrdQvkx6YzzMmDvA1MhbSKHRrc8VDong80mU2cI0.png" width="600"/>
  <br><i>Modal window with interactive map and location details</i>
</p>

<p align="center">
  <img src="https://s10.iimage.su/s/25/gIJiVe8xuAvjoolnUOkzGhKYBUMZAk7CAKTnlCrUa.png" width="600"/>
  <br><i>Mini-map feature with auto-update</i>
</p>

### 🇷🇺 RussiaGuessr Mode

<p align="center">
  <img src="https://s10.iimage.su/s/24/g67iY3HxJ6o7gfYCzsYIGaK8mTIbgErsJN89vHDy9.png" width="600"/>
  <br><i>RussiaGuessr interface</i>
</p>

<p align="center">
  <img src="https://s10.iimage.su/s/24/gfrJ36mx5zZ6ftDl635cyfZO9wJDkgUoDNaUFbPq4.png" width="600"/>
  <br><i>Detailed location information panel</i>
</p>

---

## ⚡ Key Features

### 🎯 Core Functionality
- ✅ **Automatic coordinate interception** from Google Maps API requests
- ✅ **Real-time updates** when moving to next round
- ✅ **Visual feedback** - button glows green when coordinates update
- ✅ **Works on all game modes** - regular games, challenges, custom maps

### 🗺️ Interactive Mapping
- 🗺️ **Full-screen modal map** with Leaflet.js
- 📍 **Precise markers** with coordinate display
- 🔍 **Zoom and pan controls**
- 🎨 **Beautiful CartoDB Voyager tiles**

### 📱 Mini-Map Feature
- 📐 **Compact 320x240px map** under "Where?" button
- 🔄 **Auto-updates** with each new location
- 🎚️ **Toggle on/off** with one click
- 💾 **Setting persists** across sessions

### 🌐 Multi-Language Support
- 🇷🇺 **Russian** interface and location data
- 🇬🇧 **English** interface and location data
- 🔄 **Easy switching** in modal window
- 💾 **Language preference saved**

### 📊 Location Information
- 🌍 Country, state/region, county
- 🏙️ City, town, village, suburb
- 🛣️ Road name and house number
- 📮 Postal code
- 📡 Data from OpenStreetMap Nominatim API

### 💾 Settings Management
- ⚙️ **Automatic saving** to chrome.storage
- 🌐 Language preference
- 🗺️ Mini-map state (on/off)
- 🔄 Applied on next launch

---

## 🔧 How It Works

### Technical Architecture

```
┌─────────────────────────────────────────────────────────┐
│                    GeoGuessr Website                     │
│  ┌───────────────────────────────────────────────────┐  │
│  │         Google Street View / Maps API             │  │
│  │  (GetMetadata requests with coordinate data)      │  │
│  └───────────────┬───────────────────────────────────┘  │
└──────────────────┼──────────────────────────────────────┘
                   │
                   ▼
         ┌─────────────────────┐
         │    inject.js        │ ◄── Injected into page context
         │  (Page-level hook)  │     Intercepts Fetch/XHR
         └──────────┬──────────┘
                    │ postMessage
                    ▼
         ┌─────────────────────┐
         │    content.js       │ ◄── Content script
         │  (Extension layer)  │     Receives coordinates
         └──────────┬──────────┘
                    │
                    ├──► Creates "Where?" button
                    ├──► Updates mini-map (if enabled)
                    ├──► Stores in latestCandidate
                    └──► Shows modal on click
                           │
                           ▼
                    ┌──────────────────┐
                    │  Modal Window    │
                    │  - Leaflet Map   │
                    │  - Location Info │
                    │  - Settings      │
                    └──────────────────┘
```

### Coordinate Extraction Process

1. **Injection Phase**
   - `inject.js` is injected into page context at `document_start`
   - Hooks into `window.fetch` and `XMLHttpRequest.prototype`

2. **Interception Phase**
   ```javascript
   // When GeoGuessr loads a location, it calls:
   fetch('https://maps.googleapis.com/.../GetMetadata?...')
   
   // Response format:
   [[0],[[[1],[2,"pano_id"],[...],[...],[...],
     [[[1],[[null,null,LAT,LNG],...
   ```

3. **Parsing Phase**
   - Extract coordinates from nested array structure
   - Format: `data[1][0][5][0][1][0]` = `[null, null, LAT, LNG]`
   - Validate that LAT and LNG are numbers

4. **Communication Phase**
   - Send via `window.postMessage()` to content script
   - Include timestamp to track new locations

5. **Display Phase**
   - Update `latestCandidate` variable
   - Trigger button animation (green glow)
   - Update mini-map if enabled
   - Ready for modal display

### Supported API Endpoints

The extension intercepts these Google Maps API calls:
- `GetMetadata` - Primary source of coordinates
- `photometa` - Alternative metadata endpoint
- `maps.googleapis.com` - General Maps API
- `cbk` - Street View callback data

---

## 📦 Installation

### Quick Install (Recommended)

1. **Download Extension**

   - Go to [Releases](https://github.com/psybladerrr/MapReaper/releases)

   - Download `MapReaper.Geoguessr.crx` file from the latest release

2. **Install Extension**

   - Open `chrome://extensions/` (or `edge://extensions/`)

   - Enable **Developer Mode** (toggle in top-right corner)

   - **Drag and drop** the `.crx` file into the browser window

   - Click **Add Extension** in the popup

3. **Verify Installation**

   - Visit [geoguessr.com](https://www.geoguessr.com)

   - Start a game

   - "Where?" button should appear in top-left corner

---

## 🎮 Usage Guide

### Basic Usage

1. **Start a Game**
   - Go to [geoguessr.com](https://www.geoguessr.com) or [russiaguessr.ru](https://russiaguessr.ru)
   - Start any game mode (regular, challenge, custom map)

2. **Wait for Location Load**
   - Extension automatically intercepts coordinates
   - "Where?" button appears in top-left corner
   - Button glows green when coordinates update

3. **View Location**
   - Click "Where?" button
   - Modal window opens with:
     - Interactive map centered on location
     - Detailed location information
     - Settings panel

4. **Configure Settings**
   - **Language**: Switch between Russian/English
   - **Mini-Map**: Toggle compact map under button
   - Settings save automatically

### Advanced Features

#### Mini-Map
- Enable in modal settings
- Appears below "Where?" button (320x240px)
- Auto-updates with each new round
- Click to interact (zoom, pan)

#### Keyboard Shortcuts
- `ESC` - Close modal window
- Click outside modal - Close modal

#### Console Debugging
Open DevTools (F12) to see:
```
🔧 MapReaper: Инжектирован скрипт перехвата
✅ Fetch/XHR перехват установлен для Geoguessr
📍 MapReaper: Перехвачены координаты из Geoguessr (Fetch)
✅ MapReaper: Координаты обновлены (новая локация)
```

---

## 📁 Project Structure

```
MapReaper/
├── 📄 manifest.json          # Extension configuration (Manifest V3)
├── 📄 content.js             # Main content script (UI, logic)
├── 📄 inject.js              # Page-level injection (API hooks)
├── 📄 styles.css             # UI styles (dark theme)
├── 📄 content_v2.js          # Alternative map implementations
├── 📄 map-fallback.js        # Fallback map options
├── 📄 LICENSE                # License file
├── 📄 README.md              # This file
├── 📄 RELEASE_NOTES.md       # GeoGuessr release notes
├── 📄 RELEASE_NOTES_RUSSIAGUESSR.md  # RussiaGuessr release notes
└── 🖼️ assets/
    ├── avatar.png            # Extension icon (16x16)
    ├── icon16.png            # Toolbar icon (16x16)
    ├── icon48.png            # Extension page icon (48x48)
    ├── icon128.png           # Chrome Web Store icon (128x128)
    └── icon.svg              # Vector icon source
```

### File Descriptions

| File | Purpose | Key Functions |
|------|---------|---------------|
| `manifest.json` | Extension config | Permissions, content scripts, web resources |
| `content.js` | Main logic | UI creation, coordinate handling, settings |
| `inject.js` | API interception | Fetch/XHR hooks, coordinate extraction |
| `styles.css` | Styling | Dark theme, animations, responsive design |
| `content_v2.js` | Alternatives | Google Maps, Yandex Maps fallbacks |

---

## 🔧 Configuration

### Manifest V3 Permissions

```json
{
  "permissions": [
    "activeTab",      // Access current tab
    "storage"         // Save settings
  ],
  "host_permissions": [
    "https://www.geoguessr.com/*",           // GeoGuessr
    "https://nominatim.openstreetmap.org/*"  // Location data
  ]
}
```

### Storage Schema

```javascript
{
  language: "ru" | "en",      // Interface language
  showMiniMap: true | false   // Mini-map visibility
}
```

---

## 🛠️ Development

### Prerequisites
- Chrome/Edge browser
- Basic knowledge of JavaScript
- Text editor (VS Code recommended)

### Local Development

1. **Clone repository**
   ```bash
   git clone https://github.com/psybladerrr/MapReaper.git
   cd MapReaper
   ```

2. **Make changes**
   - Edit `content.js`, `inject.js`, or `styles.css`
   - Test changes locally

3. **Reload extension**
   - Go to `chrome://extensions/`
   - Click reload icon on MapReaper card
   - Refresh GeoGuessr page

4. **Debug**
   - Open DevTools (F12)
   - Check Console for logs
   - Use Sources tab to debug

### Adding New Features

#### Example: Add new language

1. **Update translations in `content.js`**
   ```javascript
   const translations = {
     ru: { /* ... */ },
     en: { /* ... */ },
     es: {  // New language
       title: 'Verificación de ubicación',
       coordinates: 'Coordenadas',
       // ...
     }
   };
   ```

2. **Add language option**
   ```javascript
   <select id="language-select">
     <option value="ru">Русский</option>
     <option value="en">English</option>
     <option value="es">Español</option>
   </select>
   ```

3. **Test and commit**

---

## 🐛 Troubleshooting

### Common Issues

#### "Where?" button doesn't appear
- ✅ Check extension is enabled in `chrome://extensions/`
- ✅ Refresh the GeoGuessr page
- ✅ Check console for errors (F12)
- ✅ Verify you're on a game page (`/game` or `/challenge`)

#### Coordinates not updating
- ✅ Check console for "📍 MapReaper: Перехвачены координаты"
- ✅ Ensure location has fully loaded
- ✅ Try moving to next round
- ✅ Check Network tab for `GetMetadata` requests

#### Map not loading
- ✅ Check internet connection
- ✅ Verify Leaflet.js CDN is accessible
- ✅ Check browser console for errors
- ✅ Try alternative map in `content_v2.js`

#### Settings not saving
- ✅ Check `storage` permission in manifest
- ✅ Open DevTools → Application → Storage → Extension Storage
- ✅ Verify chrome.storage.local is working

### Debug Mode

Enable verbose logging:
```javascript
// In inject.js, uncomment:
console.log('🗺️ MapReaper: Запрос к Maps API:', url);
console.log('📦 MapReaper: GetMetadata ответ:', text.substring(0, 200));
```

---

## 🔐 Privacy & Security

### Data Collection
- ❌ **No data is collected** or sent to external servers
- ❌ **No analytics** or tracking
- ❌ **No user information** is stored

### Data Usage
- ✅ Coordinates are **only displayed locally**
- ✅ Settings stored in **browser's local storage**
- ✅ Location data from **OpenStreetMap API** (public)

### Permissions Explained
- `activeTab` - Access current tab to inject scripts
- `storage` - Save user preferences locally
- `host_permissions` - Access GeoGuessr and OSM APIs

---

## 📊 Compatibility

### Supported Platforms
| Platform | Version | Status |
|----------|---------|--------|
| GeoGuessr | Latest | ✅ Full support |
| RussiaGuessr | Latest | ✅ Full support |

### Supported Browsers
| Browser | Version | Status |
|---------|---------|--------|
| Chrome | 88+ | ✅ Tested |
| Edge | 88+ | ✅ Tested |
| Brave | 88+ | ⚠️ Should work |
| Opera | 74+ | ⚠️ Should work |

### Game Modes
- ✅ Regular games
- ✅ Challenges
- ✅ Custom maps
- ✅ Multiplayer
- ✅ Ranked (RussiaGuessr)

---

## 🤝 Contributing

Contributions are welcome! Here's how:

1. **Fork the repository**
2. **Create feature branch**
   ```bash
   git checkout -b feature/amazing-feature
   ```
3. **Commit changes**
   ```bash
   git commit -m 'Add amazing feature'
   ```
4. **Push to branch**
   ```bash
   git push origin feature/amazing-feature
   ```
5. **Open Pull Request**

### Contribution Guidelines
- Follow existing code style
- Add comments for complex logic
- Test thoroughly before submitting
- Update README if needed

---

## 📝 Changelog

### v1.0.5-geoguessr (2026-01-XX)
- ✨ Full GeoGuessr support
- ✨ Mini-map with auto-update
- ✨ Multi-language (RU/EN)
- ✨ Settings persistence
- 🐛 Fixed coordinate update bug
- 🎨 Improved UI/UX

### v1.0.4-russiaguessr (2026-01-XX)
- ✨ RussiaGuessr support
- ✨ WebSocket for ranked games
- ✨ Version checking system
- 🎨 Dark theme interface

[Full Changelog](RELEASE_NOTES.md)

---

## ⚠️ Disclaimer

This extension is provided **"as is"** for educational and administrative purposes.

- 📚 **Educational use** - Learn about web APIs and coordinate systems
- 🛠️ **Administrative use** - Verify map accuracy and location data
- ⚖️ **User responsibility** - Comply with platform terms of service

The author is not responsible for misuse or violations of platform rules.

---

## 📄 License

**All Rights Reserved © 2026 [psybladerrr](https://github.com/psybladerrr)**

This is proprietary software. Unauthorized copying, modification, distribution, or use is strictly prohibited without explicit permission from the author.

For licensing inquiries, contact the author.

---

## 🔗 Links

- 🐙 **GitHub**: [psybladerrr/MapReaper](https://github.com/psybladerrr/MapReaper)
- 👤 **Author**: [psybladerrr](https://github.com/psybladerrr)
- 💰 **Support**: [DonateX](https://donatex.gg/donate/psyblader)
- 🌍 **GeoGuessr**: [geoguessr.com](https://www.geoguessr.com)
- 🇷🇺 **RussiaGuessr**: [russiaguessr.ru](https://russiaguessr.ru)

---

## ⭐ Support the Project

If you find MapReaper useful:

- ⭐ **Star** this repository
- 🐛 **Report bugs** via Issues
- 💡 **Suggest features** via Discussions
- 🔀 **Contribute** code via Pull Requests
- 💰 **Donate** to support development

---

## 🙏 Acknowledgments

- **Leaflet.js** - Interactive map library
- **OpenStreetMap** - Location data provider
- **CartoDB** - Beautiful map tiles
- **GeoGuessr** - Inspiration for the project
- **Community** - Feedback and support

---

<br>

<p align="center">
  <img src="https://img.shields.io/badge/Made%20with-❤️-ff3b3b?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Built%20by-psybladerrr-0ff?style=for-the-badge"/>
</p>

<p align="center">
  <b>MapReaper</b> — Precise coordinates for map verification
</p>

<p align="center">
  <sub>Not affiliated with GeoGuessr or RussiaGuessr</sub>
</p>
