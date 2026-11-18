# YOCIM Audio Cut

[English](README.md) | [简体中文](README.zh-CN.md)

A browser-based, local-first audio editor. Files are decoded and processed in your browser — nothing is uploaded to a server. Built with Vue 3, TypeScript and the Web Audio API.

**[Live demo](https://audio.yocim.top/)**

## Features

- **Local and private** — import by clicking or dragging files onto the window; all decoding and DSP happens locally.
- **Waveform editor** — precise selection, zoom/pan, zero-crossing snapping, cut/copy/paste, fades, gain and undo/redo.
- **Multitrack timeline** — clips on multiple tracks, drag to move, trim edges non-destructively, split/delete, track gain and pan, plus microphone recording.
- **Non-destructive effect chain** — multi-band EQ, filters, dynamics and more with live A/B preview; effects are rendered once at export time.
- **Pitch-preserving time stretch** — 0.25x–4x WSOLA processing in a Web Worker, optionally limited to the current selection.
- **Analysis and repair** — LUFS / RMS / true peak metering, loudness normalization, spectrogram, noise reduction, declick, limiter and pitch shift.
- **Markers and navigation** — cue list, CSV import/export, adjustable snap grid, keyboard navigation and silence detection.
- **Video audio extraction** — extract audio from video offline with a self-hosted ffmpeg.wasm core.
- **Batch processing** — queue multiple files for serial processing and export them individually or as a ZIP archive.
- **Flexible export** — WAV (16/24/32-bit), MP3, FLAC, M4A/AAC, OGG and WebM; choose sample rate, channels, bitrate, metadata and export range (whole file, selection or timeline mix).
- **Lossless projects** — `.yac.zip` project packages store PCM as 32-bit float WAV, with automatic session recovery in IndexedDB.

## Getting started

Requirements: Node.js 22 is recommended (the same version used by CI).

```bash
npm install
npm run dev
```

Open the URL printed by Vite. To create and preview a production build:

```bash
npm run build
npm run preview
```

The deployable static site is generated in `dist/`.

## Using the editor

1. Click **Import Audio** or drag an audio file onto the window. Browser-decodable formats such as WAV, MP3, FLAC, OGG and M4A are supported, depending on the browser.
2. Switch between **Waveform** and **Multitrack Timeline** at the top of the editor.
3. Use the right sidebar tabs to edit, apply effects, measure, add markers, repair, record or export.
4. Save a portable `.yac.zip` project from the top bar, or reopen one later. Work in progress is also restored automatically on the same browser.
5. Open **Export** to choose a format and download the result. WAV can optionally be streamed directly to a file via the File System Access API where supported.

## Keyboard shortcuts

| Key | Action |
| --- | --- |
| `Space` | Play / pause |
| `B` | Bypass / enable the effect chain |
| `M` | Add a marker at the playhead |
| `[` / `]` | Jump to previous / next marker |
| `←` / `→` | Nudge selection or playhead (`Shift`: right edge, `Ctrl`: left edge, `Alt`: 10x) |
| `Home` / `End` | Jump to start / end |
| `Ctrl+Z` / `Ctrl+Shift+Z` / `Ctrl+Y` | Undo / redo |
| `Ctrl+C` / `Ctrl+X` / `Ctrl+V` | Copy / cut / paste |
| `Delete` | Delete the selected region |

## Project structure

| Path | Purpose |
| --- | --- |
| `src/audio/` | DSP core: effects, loudness, spectral processing, mixdown, multitrack models |
| `src/workers/` | Compute workers for audio processing, peak generation and MP3 encoding |
| `src/composables/` | Import, export, recording, batch processing and project persistence |
| `src/components/` | Editor UI components and sidebar panels |
| `src/stores/` | Pinia stores for editor state and notifications |
| `public/` | Static assets, favicon, `robots.txt`, `sitemap.xml` and the self-hosted ffmpeg core |
| `.github/workflows/deploy.yml` | GitHub Pages deployment workflow |

## Deployment

The repository includes a GitHub Pages workflow that builds on every push to `main` and publishes `dist/`. The custom domain is `audio.yocim.top` (see `public/CNAME`), and Vite's `base` is set to `/` for root-path hosting.

## License

[ISC License](LICENSE) — Copyright (c) 2026 YOCIM.
