# UntitledRhythmGame

A Project SEKAI–inspired rhythm game built for the [Adafruit Fruit Jam](https://www.adafruit.com/product/6200), running on the RP2350B.

> **Status:** early development — chart parsing and rendering pipeline in progress.

## What this is

A standalone rhythm-chart player: point it at a chart file and a backing track, and it renders falling notes on the Fruit Jam's DVI output, synced to the audio, with input read from a connected controller/keyboard.

This project is based off of community charts, **not** Project SEKAI itself. See [Chart sources](#chart-sources) below.

## Hardware target

| Component | Fruit Jam feature used |
|---|---|
| MCU | RP2350B @ 150MHz |
| Video | DVI output via HSTX |
| Audio | I2S DAC (TLV320DAC3100) |
| Storage | microSD (charts + audio) |
| Memory | 8MB PSRAM for chart/asset buffering |
| Updater | ESP32-C6 WiFi coprocessor (SPI) |

Built with the Arduino framework (arduino-pico core).

## Supported chart formats

- **`.sus`** (Sliding Universal Score) — plain-text, measure/tick-based grid format. Parsed by `sus_parser`.
- **`.usc`** (Universal Sekai Chart) — JSON-based format with native support for PJSK-style note types (critical, flick, trace, hold ticks). Parsed by `usc_parser`.

Both parsers normalize into a shared internal note-list representation so the renderer and judgment logic don't need to know which format a chart came from.

## Note types

| Note | Color |
|---|---|
| Tap | Teal |
| Critical Tap | Amber |
| Flick | Red |
| Critical Flick | Gold |
| Hold | Blue |
| Trace | Gray |

Notes fall top-to-bottom through vertical lanes toward a horizontal judgment line near the bottom of the screen.

## Project layout

```
UntitledRhythmGame/
├── src/
│   ├── sus_parser/     # .sus chart parsing
│   ├── usc_parser/     # .usc chart parsing
│   ├── updater/        # fetches new charts/content over WiFi or SD
│   └── chart_types.h   # shared note/chart data structures
├── UntitledRhythmGame.ino
├── LICENSE
└── README.md
```

## Chart sources

This project plays **custom/fan-made charts** (e.g. from community chart editors like MikuMikuWorld for Chart Cyanvas) paired with audio you have the rights to use — your own compositions, licensed tracks, or original charts over cleared audio.

It does not read, extract, or play official Project SEKAI in-game assets, which are encrypted and DRM-protected.

## Building

_Build instructions coming soon — Arduino IDE / arduino-cli with the Fruit Jam board package._

## License

MIT — see [LICENSE](LICENSE).
