```
███╗   ██╗ █████╗ ███████╗ █████╗     ██████╗  ██████╗ ██╗    ██╗███████╗██████╗
████╗  ██║██╔══██╗██╔════╝██╔══██╗    ██╔══██╗██╔═══██╗██║    ██║██╔════╝██╔══██╗
██╔██╗ ██║███████║███████╗███████║    ██████╔╝██║   ██║██║ █╗ ██║█████╗  ██████╔╝
██║╚██╗██║██╔══██║╚════██║██╔══██║    ██╔═══╝ ██║   ██║██║███╗██║██╔══╝  ██╔══██╗
██║ ╚████║██║  ██║███████║██║  ██║    ██║     ╚██████╔╝╚███╔███╔╝███████╗██║  ██║
╚═╝  ╚═══╝╚═╝  ╚═╝╚══════╝╚═╝  ╚═╝   ╚═╝      ╚═════╝  ╚══╝╚══╝ ╚══════╝╚═╝  ╚═╝
```

# 🛰️ NASA POWER Data Downloader

**Download hourly climate data from NASA's POWER API — no coding required. Just open, click, and download.**

[![Python](https://img.shields.io/badge/Python-3.8%2B-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white)](https://jupyter.org/)
[![NASA POWER](https://img.shields.io/badge/NASA-POWER%20API-0B3D91?style=for-the-badge&logo=nasa&logoColor=white)](https://power.larc.nasa.gov/)
[![ipywidgets](https://img.shields.io/badge/ipywidgets-Interactive%20UI-orange?style=for-the-badge)](https://ipywidgets.readthedocs.io/)
[![License](https://img.shields.io/badge/License-MIT-22C55E?style=for-the-badge)](LICENSE)

---

## 🔭 What Is This?

A fully interactive **Jupyter Notebook** that pulls hourly climate data directly from [NASA's POWER API](https://power.larc.nasa.gov/) — covering any land location on Earth from **2001 to yesterday**. No API keys. No configuration files. No scripting needed.

Pick your location, date range, community, and parameters — hit **Download Data** — and get a clean, labelled CSV or Excel file in seconds.

![NASA POWER Data Downloader Interface](images/NASA_POWER_Data_Downloader.jpg)

---

## ✨ Features at a Glance

|   | Feature |
|---|---------|
| 🌍 | **Global Coverage** — Any land point on Earth at 0.5° × 0.625° grid resolution |
| 📅 | **Hourly Resolution** — Timestamped in UTC from 2001-01-01 to yesterday |
| 🏙️ | **Location Presets** — 25+ cities across 🇦🇹 Austria, 🇩🇪 Germany, and Europe |
| 🏢 | **3 Data Communities** — RE (Renewable Energy), SB (Sustainable Buildings), AG (Agroclimatology) |
| 📊 | **15 Climate Parameters** — Solar radiation, wind, temperature, humidity, precipitation |
| 💾 | **Export to CSV or Excel** — Auto-named with location + date range |
| 📈 | **Instant Summary** — Preview table, statistics, and download link after every fetch |
| ⚡ | **Zero Config** — 2 cells to run: install → launch |

---

## 🖥️ Interface Preview

![Parameters Selection Interface](images/parameters.jpg)

---

## 🚀 Quick Start

### 1 — Clone the repository

```bash
git clone https://github.com/AIMLDS7/NASA_POWER_Data_Downloader.git
cd NASA_POWER_Data_Downloader
```

### 2 — Open the notebook

```bash
jupyter notebook NASA_POWER_Downloader_R05.ipynb
```

### 3 — Run Cell 1 (once only)

```
📦 Installing dependencies...
✅ All dependencies installed!
```

Installs: `ipywidgets` · `requests` · `pandas` · `openpyxl`

### 4 — Run Cell 2 to launch the UI

```
┌─────────────────────────────────────────────────────────────┐
│  🛰️  NASA POWER Data Downloader                             │
│       Hourly Climate Data • Global Coverage • 2001-Present  │
├─────────────────────────────────────────────────────────────┤
│  📅 Date Range    [ 2026-05-31 ]  →  [ 2026-06-06 ]         │
│  📍 Location      Vienna (Wien)   48.2082°N  16.3738°E       │
│  🏢 Community     ● RE   ○ SB   ○ AG                         │
│  📊 Parameters    ☑ Solar  ☑ Wind  ☑ Temperature  ☑ Humidity │
│  💾 Output        ● CSV   ○ Excel                            │
│                                                             │
│              [ ⬇ Download Data ]                            │
└─────────────────────────────────────────────────────────────┘
```

### 5 — Your file is ready

```
✅ Download Complete!
📁 File:       NASA_RE_48.2082_16.3738_2026-05-31_2026-06-06.csv
📍 Location:   48.2082°N, 16.3738°E
📅 Period:     2026-05-31 to 2026-06-06
📊 Records:    168 hourly observations
📈 Parameters: ALLSKY_SFC_SW_DWN, WS10M, T2M, RH2M ...
⚠️ Missing Data: 0.0%
```

---

## 🏢 Data Communities

Three NASA POWER communities are supported, each optimized for a different domain:

| Community | Focus | Best For |
|-----------|-------|----------|
| **RE** | Renewable Energy | Solar panel sizing, wind turbine analysis, PV system design |
| **SB** | Sustainable Buildings | HVAC design, building energy simulation, thermal comfort |
| **AG** | Agroclimatology | Crop modeling, irrigation planning, agricultural forecasting |

![Community Descriptions and Troubleshooting](images/community_description_and_trouble_shooting.jpg)

Switching communities **automatically reorders** the parameter list by relevance and applies smart defaults.

---

## 📊 Parameter Reference

All 15 available climate parameters:

![Parameter Reference Table](images/parameters_reference.jpg)

| Parameter | Description | Units |
|-----------|-------------|-------|
| `T2M` | Temperature at 2 meters | °C |
| `T2MDEW` | Dew/Frost Point at 2 meters | °C |
| `T2MWET` | Wet Bulb Temperature at 2 meters | °C |
| `RH2M` | Relative Humidity at 2 meters | % |
| `QV2M` | Specific Humidity at 2 meters | g/kg |
| `PS` | Surface Pressure | kPa |
| `WS10M` | Wind Speed at 10 meters | m/s |
| `WS50M` | Wind Speed at 50 meters | m/s |
| `WD10M` | Wind Direction at 10 meters | Degrees |
| `WD50M` | Wind Direction at 50 meters | Degrees |
| `PRECTOTCORR` | Precipitation (Corrected) | mm/hour |
| `ALLSKY_SFC_SW_DWN` | All Sky Surface Shortwave Downward Irradiance | W/m² |
| `ALLSKY_SFC_SW_DNI` | All Sky Direct Normal Irradiance | W/m² |
| `ALLSKY_SFC_SW_DIFF` | All Sky Diffuse Horizontal Irradiance | W/m² |
| `CLRSKY_SFC_SW_DWN` | Clear Sky Shortwave Downward Irradiance | W/m² |

> Parameters are dynamically filtered and reordered by relevance when you switch communities.

---

## 🏙️ Built-In Location Presets

No need to look up coordinates for common cities — just select from the dropdown:

```
🇦🇹 AUSTRIA          🇩🇪 GERMANY             🌍 OTHER
─────────────────   ──────────────────────  ───────────────────────
Vienna (Wien)       Berlin                  London, UK
Graz                Munich (München)        Paris, France
Linz                Hamburg                 Zurich, Switzerland
Salzburg            Frankfurt am Main       Amsterdam, Netherlands
Innsbruck           Cologne (Köln)          Rome, Italy
Klagenfurt          Stuttgart               Madrid, Spain
Villach             Düsseldorf              New York, USA
Wels                Leipzig
St. Pölten          Dortmund
Dornbirn            Dresden, Hannover ...
```

For any other location, type in custom latitude/longitude — or use [latlong.net](https://www.latlong.net/).

---

## 📂 Output File Format

Output files are auto-named using this convention:

```
NASA_{COMMUNITY}_{LAT}_{LON}_{START_DATE}_{END_DATE}.csv
```

**Example:**
```
NASA_RE_48.2082_16.3738_2026-05-31_2026-06-06.csv
```

The file contains:
- **Index**: `DateTime_UTC` — hourly timestamps in UTC (`YYYY-MM-DD HH:MM:SS`)
- **Columns**: One column per selected parameter (NASA missing values `-999` replaced with `NaN`)
- **Format**: Clean, analysis-ready; compatible with pandas, Excel, R, and any CSV tool

---

## 📦 Dependencies

| Package | Version | Purpose |
|---------|---------|---------|
| `ipywidgets` | ≥ 7.6 | Interactive UI (dropdowns, date pickers, checkboxes, buttons) |
| `requests` | ≥ 2.25 | NASA POWER API calls |
| `pandas` | ≥ 1.3 | Data parsing, formatting, and export |
| `openpyxl` | ≥ 3.0 | Excel `.xlsx` file writing |

> **Note:** `ipywidgets` requires **Jupyter Notebook** or **JupyterLab**. Widgets will not render in static GitHub file previews.

---

## 📁 Project Structure

```
📦 NASA_POWER_Data_Downloader/
├── 📓 NASA_POWER_Downloader_R05.ipynb   ← Main notebook (2 cells: install + UI)
├── 📁 images/                           ← Screenshots used in this README
│   ├── 🖼️ NASA_POWER_Data_Downloader.jpg
│   ├── 🖼️ parameters.jpg
│   ├── 🖼️ parameters_reference.jpg
│   └── 🖼️ community_description_and_trouble_shooting.jpg
├── 📄 README.md
└── 📄 LICENSE
```

---

## ⚠️ Troubleshooting

**Error 422?** This usually means one of the following:

- Coordinates are over the ocean → try a land location
- Too many parameters selected → try selecting fewer
- Date range too long → start with 7–14 days
- Some parameters are not available for hourly data

**Timeout?** NASA servers can be slow:

- Try a shorter date range (under 30 days recommended)
- Try during off-peak hours (European mornings tend to be fastest)
- Select fewer parameters per request

---

## 🔗 Resources

- [NASA POWER Data Access Viewer](https://power.larc.nasa.gov/data-access-viewer/)
- [NASA POWER Parameter Dictionary](https://power.larc.nasa.gov/docs/tutorials/parameters/)
- [NASA POWER API Documentation](https://power.larc.nasa.gov/docs/services/api/)
- [latlong.net — Find coordinates for any city](https://www.latlong.net/)

---

## 🤝 Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you'd like to change.

---

**Built with 🛰️ NASA POWER API · 🐼 Pandas · 🪐 Jupyter · 🔧 ipywidgets**

*Climate data, no friction.*
