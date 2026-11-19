# Changelog (VYVAR-release)

## 0.9.0b1 - first public beta

First public release. Earlier preview builds were internal test builds and are not supported; data processed
with them should be processed again with this version.

- Night processing from raw FITS to light curves: calibration (dark, flat, calibration library), frame quality
  control, alignment, plate solving against Gaia DR3, aperture photometry, comparison-star ensemble,
  systematics, BJD_TDB, variability statistics and candidates.
- Mono and one-shot colour (OSC) cameras; AAVSO Extended Format and VarAstro export; PDF reports.
- ePSF photometry available as beta, off by default.
- Command-line night run: `VYVAR.bat --night-run -- <options>` / `./vyvar.sh --night-run -- <options>`.
- `config.json` check: `VYVAR.bat --tool validate_config`.
- User manual in English and Czech (`docs/`).
- Free license for download and use (LICENSE); third-party licenses in `THIRD_PARTY_NOTICES.txt`.
