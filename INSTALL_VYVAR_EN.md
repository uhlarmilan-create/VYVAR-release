# Installing VYVAR (short guide)

The full guide is chapter 2 of the manual ([docs/VYVAR_Manual_EN.pdf](docs/VYVAR_Manual_EN.pdf)).

## 1. Download and check

1. Download `VYVAR-<version>-win64.zip` (Windows), `VYVAR-<version>-linux-x64.tar.gz` (Linux on a PC) or
   `VYVAR-<version>-linux-aarch64.tar.gz` (Raspberry Pi 4 / 5, 64-bit OS) from
   <https://github.com/uhlarmilan-create/VYVAR-release/releases>, together with `SHA256SUMS`.
2. Compare the checksum with the line in `SHA256SUMS`:
   - Windows: `certutil -hashfile VYVAR-<version>-win64.zip SHA256`
   - Linux: `sha256sum VYVAR-<version>-linux-x64.tar.gz`
3. Unpack to a permanent folder, for example `C:\Program Files\VYVAR\` or `~/apps/vyvar/`.

The package brings its own Python 3.12; your system Python is not used. Linux on a PC needs glibc 2.39 or
newer; the Raspberry Pi package needs a 64-bit system with glibc 2.28 or newer (Raspberry Pi OS 64-bit Bookworm
or newer), and is started like the Linux package.

## 2. Program folder and data folder

Your data (settings, database, catalogues, processed nights) lives in a separate data folder, never in the
program folder, so an upgrade only replaces the program folder.

| Platform | Default data folder |
|----------|---------------------|
| Windows | `%LOCALAPPDATA%\VYVAR` |
| Linux | `~/.local/share/vyvar` |

To use another folder (for example a large data disk), set the environment variable `VYVAR_DATA_DIR` before
starting VYVAR.

## 3. Start and check

| Action | Windows | Linux |
|--------|---------|-------|
| start the interface | double-click `VYVAR.bat` | `chmod +x vyvar.sh` once, then `./vyvar.sh` |
| health check | `VYVAR.bat --selftest` | `./vyvar.sh --selftest` |
| night run from the console | `VYVAR.bat --night-run -- <options>` | `./vyvar.sh --night-run -- <options>` |
| check `config.json` | `VYVAR.bat --tool validate_config` | `./vyvar.sh --tool validate_config` |

The interface opens at `http://localhost:8501` in your browser; keep the console window open while you work.
The self-test must end with `SELFTEST PASS`. The program files are not signed: Windows SmartScreen may ask
before the first start.

## 4. Star catalogues

VYVAR needs local catalogues; build them once from **Settings -> Paths and catalogs** or from the console:

```
VYVAR.bat --tool build_gaia -- --mag-limit 16.5
VYVAR.bat --tool build_objects -- --vsx --exoplanets
VYVAR.bat --tool build_astro_index --
VYVAR.bat --tool gaia_maintain -- --report
```

(Linux: `./vyvar.sh` instead of `VYVAR.bat`.) The Gaia DR3 catalogue takes hours to days to download and
6-40 GB depending on the faint limit; without it VYVAR cannot identify stars. The blind plate-solve index is
needed only for frames without RA/Dec in the FITS header.

## 5. Site, telescope, camera

Enter your observing site, telescope and camera in **Database Explorer** (manual section 2.3), then process
your first night (manual chapter 3).
