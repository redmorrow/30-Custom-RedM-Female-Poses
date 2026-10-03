# Changelog

Version history for the RM 30 Custom Female Pose Pack.

---

## v1.0.0 — Initial Release

**Release date:** 2026

### Added
- 29 custom female pose `.ycd` animation dictionaries
- Streamed via `stream/` folder with asset pack protection
- `clips.lua` — full animation reference (dict, clip, duration, suggested mode)
- `config.lua` — basic resource settings
- Cfx.re Keymaster escrow-ready
- Full customer documentation in `docs/`

### Animations included
- lean, pose5, pose6, hatsdown_clip (pose7), pose8
- pose10, pose11, pose13, pose17, pose18, pose23
- pose29 (pose26 dict), pose31, pose32, pose33, pose36
- pose41, pose42, pose44, pose49, pose51, pose52, pose55
- pose56, pose57, pose58, pose59, pos60, pose65

---

## v2.0.0 — Planned

The following items are planned for a future update. Dates and contents may change.

### Planned
- Additional female pose animations
- Improved animation timing and blend quality
- Updated `clips.lua` with clearer labels and categories
- Optimized `.ycd` file sizes
- Expanded integration examples in documentation

---

## Upgrading

1. Back up your edited `clips.lua` and `config.lua`.
2. Replace the resource files with the new version from Keymaster.
3. Restore your custom `clips.lua` edits (labels, categories).
4. Run `restart rm_30-custom-female-pose` or restart the server.
5. Re-test a pose using the verification snippet in [01-installation.md](01-installation.md).

Do not replace your edited files without backing up first.
