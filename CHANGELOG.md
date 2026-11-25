# Changelog (VYVAR-release)

## 0.9.0b1 - updated packages of 25 November 2026

Same version (beta testing); new packages replace the earlier 0.9.0b1 downloads.

- **Live view** (Pipeline page): light curves of all eclipsing (EA, EB, EW) and RR Lyrae stars of the field
  while you observe - every new light in the capture folder adds a point; quick-look aperture photometry
  against at most three comparison stars (manual chapter 5).
- Faster plate solving and catalogue reads on wide fields: the Gaia sky-box reads always use the (RA, Dec)
  index (some SQLite versions chose a much slower plan; BO CVn hinted solve 3 min 48 s -> 9 s).
- Results no longer depend on the row order SQLite returns: Gaia and VSX reads in a fixed order, and the two
  seeded samples (artifact check, transient FWHM) are taken in a fixed order.
- `--vacuum-into` of the Gaia catalogue keeps the WAL journal mode of the copy.

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
