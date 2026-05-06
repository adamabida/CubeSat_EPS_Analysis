# On-Orbit Power System Analysis and Anomaly Detection in CubeSats 🛰️🔋

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Pandas](https://img.shields.io/badge/Pandas-Data_Analysis-150458?logo=pandas)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualization-orange)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter)

## 📖 Project Overview
This project applies data science techniques to real-world spacecraft telemetry. We analyze the Electrical Power System (EPS) data from a constellation of four 1U CubeSats (**TSURU, NEPALISAT, RAAVANA, and UGUISU**) operating in Low Earth Orbit (LEO). 

The primary goal is to study the orbital power dynamics, thermal resilience, and to programmatically detect a known hardware anomaly (solar panel failure) that occurred on-orbit using advanced `pandas` data manipulation.

## 🎯 Project Objectives
1. **Analyze Power Cycles:** Visualize battery charging and discharging phases as the satellites transition between sunlight and eclipse during their ~92.6-minute orbits.
2. **Thermal Analysis:** Study the temperature fluctuations of external solar panels (-20°C to +60°C) versus the internally insulated battery system.
3. **Automated Anomaly Detection:** Programmatically pinpoint the exact moment of permanent solar panel failures on the *RAAVANA* and *UGUISU* satellites using rolling window statistics and time-series variance tracking.

## 📊 The Dataset
The data originates from the **BIRDS open-source standardized bus** designed by Kyutech. The satellites were deployed from the International Space Station (ISS) at an altitude of 400km with an inclination of 51.6º.

**Key Telemetry Included:**
* **Timestamps:** Relative time of data collection (sampled every 90s or 10s).
* **Voltage (mV) & Current (mA):** Collected for 5 solar panels (+X, -X, +Y, -Y, +Z) via LMP8640 sensors.
* **Temperatures (°C):** Collected for solar panels via LMT84 sensors and the battery via a G10K3976 thermistor.
* **Battery Stats:** Battery Voltage (`Vbat`) and Battery Current (`Ibatt`).

*Note: The dataset was originally compiled by members of the BIRDS team (Adolfo Jara, Pooja Lepcha, et al.).*

## 🗂️ Repository Structure
```text
├── data/
│   ├── TSURU/             # Contains TSURU.xlsx - [Date].csv files
│   ├── RAAVANA/           # Contains RAAVANA.xlsx - [Date].csv files
│   ├── UGUISU/            # Contains UGUISU.xlsx - [Date].csv files
│   └── NEPALISAT/         # Contains NEPALISAT.xlsx - [Date].csv files
├── notebooks/
│   └── cubesat_eps_analysis.ipynb  # Main Jupyter Notebook
├── images/
│   └── power_cycle_plot.png        # Generated charts
├── requirements.txt
└── README.md
```
💻 Tech Stack
This project heavily emphasizes the use of Pandas for robust data engineering and time-series analysis.

Data Processing: pandas, numpy, glob

Visualization: matplotlib, seaborn

Environment: Jupyter Notebook

🔍 Key Findings to Look For
The Eclipse Drop: Watch how Vbat (V) steadily declines when solar panel currents (Ipx, Ipy, etc.) drop to 0 mA, indicating the satellite has entered the Earth's shadow.

The RAAVANA Anomaly: Pay close attention to the solar panel current plots for RAAVANA. You will see one panel's current generation flatline to 0 mA permanently, indicating the physical failure on-orbit.

🤝 Acknowledgments
BIRDS Constellation Team (Kyushu Institute of Technology) for designing the satellite bus and providing the open-source dataset.

Data authors: Adolfo Jara, Pooja Lepcha, Sankyun Kim, Hirokazu Masui, Takashi Yamauchi, George Maeda, Mengu Cho.














