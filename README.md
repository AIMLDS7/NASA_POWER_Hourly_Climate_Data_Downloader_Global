<div align="center">

# 🛰️ NASA POWER Hourly Climate Data Downloader

<p align="center">
  <em>Production-grade climate data pipeline · NASA POWER API · Analysis-ready time-series output</em>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.8%2B-3776AB?style=flat-square&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/Jupyter-Notebook-F37626?style=flat-square&logo=jupyter&logoColor=white"/>
  <img src="https://img.shields.io/badge/NASA-POWER%20API-0B3D91?style=flat-square&logo=nasa&logoColor=white"/>
  <img src="https://img.shields.io/badge/License-MIT-22C55E?style=flat-square"/>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Data-Hourly%20Resolution-8B5CF6?style=flat-square"/>
  <img src="https://img.shields.io/badge/Coverage-Global%202001--Present-06B6D4?style=flat-square"/>
  <img src="https://img.shields.io/badge/Output-CSV%20%7C%20Excel-10B981?style=flat-square"/>
  <img src="https://img.shields.io/badge/Parameters-15%20Meteorological-F59E0B?style=flat-square"/>
</p>

<br/>

<img src="./images/NASA_POWER_Data_Downloader.jpg" width="750" alt="NASA POWER Data Downloader Interface"/>

</div>

---

## 📌 Overview

This notebook implements a **fully automated, end-to-end climate data pipeline** on top of NASA's POWER (Prediction Of Worldwide Energy Resources) API. It removes every friction point between raw satellite-derived reanalysis data and a clean, analysis-ready time-series dataset — making it a first-class data acquisition layer for energy forecasting, building simulation, and agroclimatic ML workflows.

> **Designed for data scientists and ML engineers** who need reproducible, high-quality meteorological features without manual API wrangling.

---

## 🔬 Why NASA POWER?

NASA POWER provides **satellite-derived, model-assimilated reanalysis data** at a 0.5° × 0.625° spatial grid — the gold standard for locations with no nearby weather station. Unlike scraping commercial APIs, POWER data is:

- **Free, open, and reproducible** — no API keys, no rate-limit billing surprises
- **Physically consistent** — gap-filled using NASA GEOS-5 model assimilation
- **ML-ready** — continuous hourly records since 2001 with defined missing-value flags (`-999`) auto-converted to `NaN`

---

## ⚙️ Data Pipeline Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                     NASA POWER DATA PIPELINE                        │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ┌──────────────┐    ┌──────────────┐    ┌──────────────────────┐  │
│  │  USER INPUT  │───▶│  REST API    │───▶│   RAW JSON RESPONSE  │  │
│  │              │    │  (HTTPS GET) │    │   NASA POWER Server  │  │
│  │ · Date range │    │              │    └──────────┬───────────┘  │
│  │ · Lat / Lon  │    │ Timeout: 180s│               │              │
│  │ · Community  │    │              │               ▼              │
│  │ · Parameters │    └──────────────┘    ┌──────────────────────┐  │
│  └──────────────┘                        │  DATA PROCESSING     │  │
│                                          │                      │  │
│                                          │ · JSON → DataFrame   │  │
│                                          │ · Index → DateTime   │  │
│                                          │ · -999 → NaN         │  │
│                                          │ · Sort by timestamp  │  │
│                                          └──────────┬───────────┘  │
│                                                     │              │
│                                                     ▼              │
│                                          ┌──────────────────────┐  │
│                                          │  STRUCTURED OUTPUT   │  │
│                                          │                      │  │
│                                          │ NASA_{COM}_{LAT}_    │  │
│                                          │ {LON}_{START}_{END}  │  │
│                                          │ .csv / .xlsx         │  │
│                                          └──────────────────────┘  │
└─────────────────────────────────────────────────────────────────────┘
```

---

## 🚀 Quick Start

### Prerequisites

```bash
pip install jupyter ipywidgets requests pandas openpyxl
```

### Launch

```bash
git clone https://github.com/AIMLDS7/NASA_POWER_Hourly_Climate_Data_Downloader.git
cd NASA_POWER_Hourly_Climate_Data_Downloader
jupyter notebook NASA_POWER_Downloader_R05.ipynb
```

**Cell 1 — Install dependencies** *(run once)*

```python
# Auto-installs: ipywidgets · requests · pandas · openpyxl
```

**Cell 2 — Launch interactive interface** *(configure & download)*

```
▶ Run → interactive UI renders inline
```

---

## 🖥️ Interactive Interface

<div align="center">
<img src="./images/parameters.jpg" width="700" alt="Parameter Selection Interface"/>
</div>

The UI is built with `ipywidgets` and renders fully inside Jupyter. All inputs are validated before the API call is dispatched.

| Section | Options |
|---|---|
| **Date Range** | Any range from 2001-01-01 to yesterday; <30 days recommended |
| **Location** | 25+ city presets (Austria / Germany / Europe) or custom lat/lon |
| **Community** | RE · SB · AG (auto-reorders parameters by domain relevance) |
| **Parameters** | 15 meteorological variables with Select All / Clear All |
| **Output Format** | CSV (`.csv`) or Excel (`.xlsx`) |

---

## 🏢 Data Communities & Domain Mapping

<div align="center">
<img src="./images/community_description_and_trouble_shooting.jpg" width="700" alt="Community Descriptions and Troubleshooting"/>
</div>

Each NASA POWER community optimises the parameter set for a specific scientific domain:

| Community | Domain | ML / Engineering Applications |
|---|---|---|
| **RE** — Renewable Energy | Solar & wind resource assessment | PV yield modelling, wind power forecasting, grid dispatch optimisation |
| **SB** — Sustainable Buildings | Building thermodynamics | HVAC load prediction, thermal comfort simulation, EnergyPlus inputs |
| **AG** — Agroclimatology | Crop & soil science | Evapotranspiration modelling, irrigation scheduling, yield forecasting |

> Switching communities **automatically reorders** the parameter list by relevance and applies domain-appropriate smart defaults.

---

## 📊 Parameter Reference

<div align="center">
<img src="./images/parameters_reference.jpg" width="700" alt="Full Parameter Reference Table"/>
</div>

| Parameter | Description | Units | Domain Priority |
|---|---|---|---|
| `ALLSKY_SFC_SW_DWN` | All Sky Surface Shortwave Downward Irradiance | W/m² | RE · SB · AG |
| `CLRSKY_SFC_SW_DWN` | Clear Sky Shortwave Downward Irradiance | W/m² | RE · SB |
| `ALLSKY_SFC_SW_DNI` | Direct Normal Irradiance | W/m² | RE |
| `ALLSKY_SFC_SW_DIFF` | Diffuse Horizontal Irradiance | W/m² | RE |
| `WS10M` | Wind Speed at 10 m | m/s | RE · SB · AG |
| `WS50M` | Wind Speed at 50 m | m/s | RE |
| `WD10M` | Wind Direction at 10 m | Degrees | RE · SB |
| `WD50M` | Wind Direction at 50 m | Degrees | RE |
| `T2M` | Air Temperature at 2 m | °C | RE · SB · AG |
| `T2MDEW` | Dew/Frost Point Temperature | °C | RE · SB · AG |
| `T2MWET` | Wet Bulb Temperature | °C | SB · AG |
| `RH2M` | Relative Humidity at 2 m | % | RE · SB · AG |
| `QV2M` | Specific Humidity at 2 m | g/kg | SB · AG |
| `PS` | Surface Pressure | kPa | RE · SB |
| `PRECTOTCORR` | Corrected Total Precipitation | mm/hr | SB · AG |

---

## 📁 Output Schema

Files are auto-named using a deterministic convention for full reproducibility:

```
NASA_{COMMUNITY}_{LATITUDE}_{LONGITUDE}_{START_DATE}_{END_DATE}.csv
```

**Example:**
```
NASA_RE_48.2082_16.3738_2026-05-31_2026-06-06.csv
```

| Column | Type | Description |
|---|---|---|
| `DateTime_UTC` | `DatetimeIndex` | Hourly UTC timestamps (`YYYY-MM-DD HH:MM:SS`) |
| `ALLSKY_SFC_SW_DWN` | `float64` | Solar irradiance — W/m² |
| `WS10M` | `float64` | Wind speed — m/s |
| `T2M` | `float64` | Temperature — °C |
| `...` | `float64` | All selected parameters |

Missing values (`-999`, `-99`) are automatically replaced with `NaN` for clean downstream ingestion into pandas, scikit-learn, or any ML pipeline.

---

## 🧠 Downstream ML Use Cases

This downloader was designed as the **data acquisition layer** for meteorology-driven ML pipelines:

```
NASA POWER Downloader
        │
        ▼
  Hourly CSV / Excel
        │
   ┌────┴──────────────────────────────────────────┐
   │                                               │
   ▼                                               ▼
Energy Price Forecasting                  PV / Wind Yield Modelling
(XGBoost · LSTM · Transformer)            (Regression · Neural Net)
        │                                          │
        ▼                                          ▼
  Feature Engineering                    Irradiance → Power Curve
  · Lag features (t-1, t-24, t-168)      · Temperature derating
  · Rolling statistics                   · Wind Weibull fitting
  · Calendar encoding                    · Capacity factor calc
```

**Directly feeds into:**

- ⚡ [Day-Ahead Energy Price Forecaster (Austria)](https://github.com/AIMLDS7/ML_Dayahead_XGBoost_energy_price_forecaster_Austria) — meteorological features pipeline
- 🌞 Solar PV yield simulation
- 🌬️ Wind resource assessment & turbine siting

---

## 🏙️ Location Presets

25+ pre-loaded cities with validated coordinates:

```
🇦🇹 AUSTRIA              🇩🇪 GERMANY               🌍 EUROPE & BEYOND
────────────────────    ─────────────────────    ──────────────────────
Vienna (Wien)           Berlin                   London, UK
Graz                    Munich (München)         Paris, France
Linz                    Hamburg                  Zurich, Switzerland
Salzburg                Frankfurt am Main        Amsterdam, Netherlands
Innsbruck               Cologne (Köln)           Rome, Italy
Klagenfurt              Stuttgart                Madrid, Spain
Villach                 Düsseldorf               New York, USA
Wels                    Leipzig
St. Pölten              Dresden
Dornbirn                Hannover · Dortmund...
```

For any other location → [latlong.net](https://www.latlong.net/)

---

## 📦 Dependencies

| Package | Role |
|---|---|
| `ipywidgets ≥ 7.6` | Interactive UI — date pickers, dropdowns, checkboxes |
| `requests ≥ 2.25` | HTTP client for NASA POWER REST API |
| `pandas ≥ 1.3` | Data ingestion, timestamp parsing, NaN handling, export |
| `openpyxl ≥ 3.0` | Excel `.xlsx` serialisation |

---

## 📂 Repository Structure

```
📦 NASA_POWER_Hourly_Climate_Data_Downloader/
├── 📓 NASA_POWER_Downloader_R05.ipynb   ← Pipeline notebook (2 cells)
├── 📁 images/                           ← README screenshots
│   ├── NASA_POWER_Data_Downloader.jpg
│   ├── parameters.jpg
│   ├── parameters_reference.jpg
│   └── community_description_and_trouble_shooting.jpg
├── 📄 README.md
└── 📄 LICENSE
```

---

## ⚠️ Troubleshooting

| Error | Cause | Fix |
|---|---|---|
| `422 Unprocessable Entity` | Coordinates over ocean | Use a land location |
| `422 Unprocessable Entity` | Too many parameters | Select ≤ 8 parameters |
| `422 Unprocessable Entity` | Date range too long | Start with 7–14 days |
| `Timeout` | NASA server congestion | Retry during European morning hours |
| `KeyError: properties` | Unexpected API response format | Reduce parameters or retry |

---

## 🔗 Resources

- [NASA POWER Data Access Viewer](https://power.larc.nasa.gov/data-access-viewer/)
- [NASA POWER Parameter Dictionary](https://power.larc.nasa.gov/docs/tutorials/parameters/)
- [NASA POWER API Documentation](https://power.larc.nasa.gov/docs/services/api/)
- [GEOS-5 Reanalysis System](https://gmao.gsfc.nasa.gov/GEOS_systems/)

---

## 📜 License

Distributed under the MIT License. See [`LICENSE`](LICENSE) for details.

---

<div align="center">

**Built by [AIMLDS7](https://github.com/AIMLDS7)**

*Part of an end-to-end energy analytics & ML portfolio*

`NASA POWER API` · `Pandas` · `ipywidgets` · `Jupyter`

</div>
