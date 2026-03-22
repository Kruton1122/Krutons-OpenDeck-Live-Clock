# Krutons Clock

A crisp, pixel-perfect digital clock for [OpenDeck](https://github.com/nekename/OpenDeck). Shows the time, day of week, date, and year on a single keypad button — with a live sky-gradient background that shifts naturally through the day.

---

## Preview

| Auto (day) | Auto (night) | Custom colour |
|:----------:|:------------:|:-------------:|
| ![Day](preview/clock_auto.png) | ![Night](preview/clock_black.png) | ![Custom](preview/clock_purple.png) |

---

## Features

- **Live time** — updates every second
- **Full date display** — day of week, month, date, and year all on one button
- **12h or 24h** — with AM/PM indicator in 12h mode, positioned cleanly below the time
- **Optional seconds** — toggle on for a full `HH:MM:SS` display
- **Auto sky background** — the background colour shifts gradually through the day:

| Time | Colours |
|------|---------|
| Midnight | Deep navy |
| Pre-dawn | Dark purple |
| Sunrise | Warm orange/gold |
| Morning | Soft blue sky |
| Midday | Clear bright blue |
| Golden hour | Orange/amber |
| Sunset | Purple/orange fade |
| Night | Dark navy |

- **Full black mode** — classic, minimal, always sharp
- **Custom colour mode** — pick any background colour; text automatically inverts for legibility
- **Pure JS rendering** — no native binaries, no canvas module, no compilation needed

---

## Installation

1. Download `krutons-clock.sdPlugin.zip` from the [Releases](../../releases) page
2. Extract — you should have a folder called `clock.sdPlugin`
3. Copy it to your OpenDeck plugins directory:
   ```
   %APPDATA%\OpenDeck\plugins\
   ```
4. Restart OpenDeck
5. **Digital Clock** will appear in the actions list under **Krutons Clock**

> **Note:** OpenDeck bundles its own Node.js runtime — you do not need to install Node separately.

---

## Customisation

Click a placed clock button to open its settings panel:

### Time Format
| Setting | Description |
|---------|-------------|
| **Hour Format** | 24-hour (`14:30`) or 12-hour (`2:30 PM`) |
| **Show Seconds** | Display full `HH:MM:SS`. Scales text down to fit. |

### Background
| Setting | Description |
|---------|-------------|
| **Auto** | Sky gradient that shifts from midnight through sunrise, day, sunset, and back to night. Text colour adapts automatically. |
| **Full black** | Solid black background, white text. |
| **Custom colour** | Colour picker — text inverts automatically based on brightness. |

---

## How it works

The plugin is a lightweight Node.js process that:
1. Connects to OpenDeck over a local WebSocket
2. Reads the current system time every second via `new Date()`
3. Renders a 144×144 PNG frame entirely in pure JavaScript — pixel-level drawing with a 5×7 bitmap font, vertical gradient background, and a subtle vignette — using only Node's built-in `zlib` for PNG encoding
4. Sends the frame via `setImage` to OpenDeck

No native modules. No dependencies beyond `ws`.

---

## Requirements

- **OpenDeck** (Windows 10+)
- Node.js 20+ (bundled with OpenDeck)

---

## Project structure

```
clock.sdPlugin/
├── index.js                   # Plugin backend — rendering, WebSocket, time loop
├── manifest.json              # OpenDeck plugin manifest
├── images/
│   ├── plugin-icon.png        # Plugin icon
│   └── action-icon.png        # Action icon
├── propertyinspector/
│   └── index.html             # Settings panel UI
└── node_modules/
    └── ws/                    # WebSocket client
```

---

## Building from source

```bash
git clone https://github.com/kruton/krutons-clock
cd krutons-clock/clock.sdPlugin
npm install
```

Then zip the `clock.sdPlugin` folder and install as above.

---

## Credits

- WebSocket via [ws](https://github.com/websockets/ws)
- Built for [OpenDeck](https://github.com/nekename/OpenDeck) by nekename

---

## License

MIT
