# MeedyaSubtitler

> Comprehensive subtitle editor for the Apple ecosystem — and beyond.

**Status**: pre-alpha / planning. Issues + milestones describe the planned scope.

## Vision

A capable, native subtitle editor for macOS, iPadOS, iOS, and visionOS. Inspired by [Subtitle Edit](https://www.nikse.dk/SubtitleEdit/) on Windows — but Apple-first, with native UX, AVFoundation video integration, Apple Vision OCR, and iCloud sync. Windows and Linux to follow.

## Relationship to MeedyaConverter

MeedyaSubtitler is a **companion** to [MeedyaConverter](https://github.com/MWBMPartners/MeedyaConverter):

- **Subtitle conversion, muxing, and sync** stay in MeedyaConverter — they're part of the conversion pipeline
- **Subtitle editing** (text edits, formatting, timing fixes, OCR, quality tools, style management) lives here
- The two apps integrate via document handoff and URL schemes so you can move between conversion + editing workflows without leaving the Apple ecosystem

## Planned feature areas

See [Issues](../../issues) and [Milestones](../../milestones) for the live roadmap.

Highlights:

- Full subtitle format support (SRT, ASS / SSA, WebVTT, TTML, SUB / IDX, PGS, VOBSUB, CEA-608 / 708, and more)
- Native macOS / iPadOS table view with inline editing
- Embedded video preview via AVFoundation with frame-accurate subtitle overlay
- Audio waveform alignment view
- OCR for image-based subtitles via Apple Vision (Tesseract fallback later for Windows / Linux)
- Auto-fix for the long tail of common subtitle errors
- Style management for ASS / SSA
- Translation, karaoke timing, closed-caption support (advanced phases)
- Cross-app document handoff with MeedyaConverter

## MeedyaSuite family

- [MeedyaConverter](https://github.com/MWBMPartners/MeedyaConverter) — video / audio converter
- [MeedyaDL](https://github.com/MWBMPartners/MeedyaDL) — media downloader
- [MeedyaManager](https://github.com/MWBMPartners/MeedyaManager) — library manager
- [MeedyaDB](https://github.com/MWBMPartners/MeedyaDB) — metadata service
- MeedyaSubtitler — *this repo*

All built on [MeedyaSuite-core](https://github.com/MWBMPartners/MeedyaSuite-core) — shared Rust crates for fingerprinting, metadata, transcoding helpers, etc.

## License

All rights reserved by MWBM Partners Ltd, 2026. Licensing terms TBD as the project matures.
