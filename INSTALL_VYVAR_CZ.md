# Instalace VYVARu (kratky navod)

Uplny navod je kapitola 2 prirucky ([docs/VYVAR_Manual_CZ.pdf](docs/VYVAR_Manual_CZ.pdf)).

## 1. Stazeni a kontrola

1. Stahnete `VYVAR-<verze>-win64.zip` (Windows) nebo `VYVAR-<verze>-linux-x64.tar.gz` (Linux) z
   <https://github.com/uhlarmilan-create/VYVAR-release/releases> spolu se souborem `SHA256SUMS`.
2. Porovnejte kontrolni soucet s radkem v `SHA256SUMS`:
   - Windows: `certutil -hashfile VYVAR-<verze>-win64.zip SHA256`
   - Linux: `sha256sum VYVAR-<verze>-linux-x64.tar.gz`
3. Rozbalte do trvale slozky, napriklad `C:\Program Files\VYVAR\` nebo `~/apps/vyvar/`.

Balicek obsahuje vlastni Python 3.12; systemovy Python se nepouziva. Linux potrebuje glibc 2.39 nebo novejsi.

## 2. Slozka programu a datova slozka

Vase data (nastaveni, databaze, katalogy, zpracovane noci) jsou v oddelene datove slozce, nikdy ve slozce
programu, takze aktualizace jen nahradi slozku programu.

| Platforma | Vychozi datova slozka |
|-----------|-----------------------|
| Windows | `%LOCALAPPDATA%\VYVAR` |
| Linux | `~/.local/share/vyvar` |

Jinou slozku (napriklad velky datovy disk) nastavite promennou prostredi `VYVAR_DATA_DIR` pred spustenim VYVARu.

## 3. Spusteni a kontrola

| Akce | Windows | Linux |
|------|---------|-------|
| spustit rozhrani | dvojklik na `VYVAR.bat` | jednou `chmod +x vyvar.sh`, pak `./vyvar.sh` |
| kontrola instalace | `VYVAR.bat --selftest` | `./vyvar.sh --selftest` |
| nocni beh z konzole | `VYVAR.bat --night-run -- <volby>` | `./vyvar.sh --night-run -- <volby>` |
| kontrola `config.json` | `VYVAR.bat --tool validate_config` | `./vyvar.sh --tool validate_config` |

Rozhrani se otevre v prohlizeci na `http://localhost:8501`; okno konzole nechte behem prace otevrene.
Samotest musi skoncit radkem `SELFTEST PASS`. Soubory programu nejsou podepsane: Windows SmartScreen se muze
pred prvnim spustenim zeptat.

## 4. Hvezdne katalogy

VYVAR potrebuje mistni katalogy; postavte je jednou v **Settings -> Paths and catalogs** nebo z konzole:

```
VYVAR.bat --tool build_gaia -- --mag-limit 16.5
VYVAR.bat --tool build_objects -- --vsx --exoplanets
VYVAR.bat --tool build_astro_index --
VYVAR.bat --tool gaia_maintain -- --report
```

(Linux: `./vyvar.sh` misto `VYVAR.bat`.) Katalog Gaia DR3 se stahuje hodiny az dny a ma 6-40 GB podle limitni
magnitudy; bez nej VYVAR nedokaze identifikovat hvezdy. Index pro astrometrii naslepo je potreba jen pro snimky
bez RA/Dec v hlavicce FITS.

## 5. Lokalita, dalekohled, kamera

Zadejte svou pozorovaci lokalitu, dalekohled a kameru v **Database Explorer** (prirucka, oddil 2.3) a zpracujte
prvni noc (prirucka, kapitola 3).
