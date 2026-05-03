# CubeSat EPS On-Orbit Power System Analysis & Anomaly Detection[cite: 1, 2]

## Project Overview
This project analyzes the on-orbit Electrical Power System (EPS) telemetry data from four 1U CubeSats in the BIRDS Constellation: **TSURU, NEPALISAT, RAAVANA, and UGUISU**[cite: 1, 5]. The EPS is responsible for providing uninterrupted power to the satellite during both sunlight and eclipse phases[cite: 5].

Using `pandas` and `matplotlib`, this repository converts raw `.xlsx` telemetry data into continuous time-series dataframes, performs thermal and power cycle analysis, and implements custom anomaly detection logic to identify permanent solar panel hardware failures in space[cite: 1, 2].

## Dataset Information
The data used in this project originates from the BIRDS open-source standardized bus system (Kyushu Institute of Technology) and is available via the BIRDSOpenSource GitHub and Mendeley Data[cite: 2, 4, 5].
*   **Satellites:** TSURU, NEPALISAT, RAAVANA, UGUISU[cite: 5].
*   **Orbit Details:** Low Earth Orbit (LEO), ~400 km altitude, 51.6° inclination, ~92.6-minute orbital period[cite: 2, 5].
*   **Telemetry Features:** Voltage (mV), Current (mA), and Temperature (°C) for the internal battery and 5 external solar panels (+X, -X, +Y, -Z, +Z)[cite: 1, 2].
*   **Sampling Rate:** Every 5 to 10 seconds per orbit[cite: 2, 4].

## Project Structure
*   `CubeSat_EPS_Analysis.ipynb`: The main Jupyter Notebook containing the data pipeline, smoothing functions, and anomaly detection algorithms[cite: 1].
*   `CubeSat_EPS_Presentation.pptx`: The accompanying slide deck summarizing the methodology, thermal findings, and detected anomalies[cite: 2].
*   `TSURU.xlsx`, `NEPALISAT.xlsx`, `RAAVANA.xlsx`, `UGUISU.xlsx`: The raw telemetry datasets containing EPS readings for each respective satellite[cite: 1, 5].
*   `.gitattributes`: Git configuration file for handling text/line-endings[cite: 6].
*   `LICENSE`: MIT License file.
*   `README.md`: This project documentation file.

## Analysis Pipeline

### 1. Data Loading & Preprocessing[cite: 1]
*   Dynamically loads and concatenates multiple `.xlsx` files using Python's `glob` and `pandas`[cite: 1].
*   Strips whitespace from column names and handles missing sensor values using linear interpolation (`ffill` / `bfill`)[cite: 1].
*   Creates a continuous relative time index (samples) for robust time-series plotting[cite: 1].

### 2. Power Cycle & Thermal Analysis[cite: 1]
*   **Power Cycles:** Uses `.rolling()` window means (window=10) to filter out raw sensor noise[cite: 1, 2]. Distinguishes between eclipse (discharging) and sunlight (charging) phases based on the battery current's sign[cite: 1, 2].
*   **Thermal Analysis:** Computes the hottest panel at each timestamp using `.max()` and plots it against internal battery temperature to validate the effectiveness of the spacecraft's thermal insulation[cite: 1].

### 3. Anomaly Detection[cite: 1, 2]
Finding real hardware failures in space telemetry is challenging because eclipses and satellite tumbling naturally cause panels to read 0 mA[cite: 2]. The notebook implements two distinct statistical filters:
*   **Hard Failure Detection (UGUISU):** Identifies panels that read near 0 mA (< 1mA) for more than 30% of the time *during confirmed sunlight phases* (when other panels are actively generating power)[cite: 2].
*   **Stuck Sensor Detection (RAAVANA):** Identifies panels stuck at a constant noise floor (e.g., ~18.64 mA) by checking for abnormally low variance (e.g., fewer than 10 unique values) and verifying the panel never exceeds a healthy threshold[cite: 2].

**Results:** The pipeline successfully flagged the +Y panel hardware failures on UGUISU and RAAVANA, while confirming the TSURU and NEPALISAT power systems were operating nominally[cite: 2, 5].

## Setup and Execution
To run this project locally:

1. Clone the repository and navigate to the project directory.
2. Ensure you have Python 3.x installed along with the required libraries:
   ```bash
   pip install pandas numpy matplotlib jupyterlab openpyxl