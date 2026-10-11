# MeedyaSubtitler: media preservation integration requirements

Status: proposed development/discovery requirements, 2026-10-11. No implemented support is claimed and existing milestones remain unchanged.

Use the [common media preservation and presentation contract](https://github.com/MeedyaSuite/MeedyaSuite-specs/blob/docs/cross-app-media-contract/standards/CROSS-APP-MEDIA-CONTRACT.md) alongside the [Converter research notes](https://github.com/MWBMPartners/MeedyaConverter/blob/docs/mp4-remux-preservation/docs/MP4-Remux-Preservation-Plan.md). These links reference draft working branches. Adopt a reviewed, commit-pinned contract before implementation/conformance claims; app-specific deviations need an explicit decision and capability report.

## Native subtitle/caption editing and cross-app handoff

Respect the existing product split: text/style/timing editing, OCR and quality tools live here; subtitle conversion, muxing and synchronization in the conversion pipeline stay in MeedyaConverter. Coordinate timing edits via an explicit handoff rather than silently assigning container authoring to this app.

- Treat CEA-608 and CEA-708 as native caption formats, including video-carried data, discrete tracks, multiple services and coexistence. Keep both by default. A generic subtitle exclusion or duplicate option must not remove captions; exclusions require explicit caption-specific track/service/standard choices.
- Maintain an original native payload plus an evidence-bearing editable view. Native commands, channel/service identity, style, positioning, language, timing and accessibility data must not be flattened into SRT/ASS/TTML/mov_text as an implicit editing intermediate. Derived text/preview can aid analysis without replacing native originals.
- Use a proven native reader/writer for approved caption edits and validate command/service semantics. If native reserialization is unavailable, preserve originals and disable/report that native edit/export path. Optional conversion/OCR/translation produces an explicitly transformed output with a loss report.
- Keep forced-only, full dialogue, SDH, commentary/accessibility roles and service sets distinct. Equal dialogue is not equivalence. Preserve ASS/SSA font/resource dependencies and bitmap presentation; OCR text does not prove bitmap identity.
- Preview uses the correct selected video/edition and rational source-to-presentation timeline: offsets, priming, edit lists, explicit stretch and cuts. Caption state must restore after seeks. AVFoundation preview limitations do not define format capabilities; show unsupported presentation data and bound resource parsing.
- Versioned handoff to Converter includes stable track/service/source identities, payload/resource references, intended cue/style edits, language/role/flags, relationships, timeline mapping, original metadata and expected verification. Preserve unedited tracks/services and unrelated HDR/stereo/audio data.
- Content-aware duplicate detection is configurable: disabled, recommend-only and opt-in proven consolidation. Compare full events/native semantics including timings/styles/forced/SDH. Keep uncertain equivalents and protected caption services; no silent normalization or omission.

## Discovery and acceptance

Prototype native caption read/edit/round-trip and cross-app handoff with synthetic/licensed 608/708 service fixtures. Validate open/no-edit round trips, intentional edits only, unaffected service identity, seek state, native export refusal, subtitle/forced/SDH distinctions, style/resources, stale sources and relocated handoff packages. Validate the Converter-exported result and Player display separately; preview success alone is insufficient.

## Planning integration

Carry these cases into future implementation issues and regression fixtures. Inventory/preview, safe edits and evidence contracts come first; edition-aware synchronization and incremental edits are bounded investigations. Do not infer support from a successful mux, codec label, progress message or an archived tag. Structural/sample checks, exhaustive preservation and target playback are different verification levels.
