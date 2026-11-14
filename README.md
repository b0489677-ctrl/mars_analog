# mars_analog
# Mars on Earth: Terrestrial Analogs for Utopia Planitia (Viking 2 site)

NASA Space Apps Challenge, Giza. Team: [The Powerpuff Girls]

## Question
Which Earth regions are closest to the Viking 2 site in Utopia Planitia, on which variables, and where does the analogy break down?

## Data
**Mars (Viking 2 lander, PDS Atmospheres Node, volume vl_1001):**
- VL1/VL2-M-MET-4-BINNED-P-T-V-V1.0 (air temperature, wind)
- VL1/VL2-M-MET-4-DAILY-AVG-PRESSURE-V1.0 (pressure)
- VL1/VL2-M-LCS-5-ATMOS-OPTICAL-DEPTH-V1.0 (optical depth)

**Earth (NASA Earthdata, MERRA-2 monthly, 2022):** M2TMNXSLV, M2TMNXAER, M2TMNXLND, M2C0NXASM

## Mars reference values (Viking 2)
| Variable | Value |
|---|---|
| Air temperature (1.6 m) | 193.7 K |
| Wind speed | 4.48 m/s |
| Pressure | 874 Pa |
| Optical depth | 0.85 |
| Vegetation, surface soil moisture | 0 (assumption) |

## Method
Similarity score per variable = 100 x (1 - |Earth - Mars| / scale), clipped to 0-100. Total score = weighted mean (missing values ignored). Elevation is not scored. Pressure is reported separately. Sensitivity analysis with 4 weighting scenarios.

## Results
[Paste the ranking table here]

## Limitations
- One lander site, one Earth year (2022)
- MERRA-2 is a model with about 50 km resolution
- Viking temperature is air temperature at 1.6 m; optical depth includes dust and ice haze
- Earth cannot reproduce Mars' gravity, pressure, radiation or atmosphere

## Files
- `mars_analog_FINAL.ipynb`: Earth data download, scoring, sensitivity, map
- `viking2_extraction.py`: Mars reference values from Viking 2 files
- `results.csv`, `sensitivity.csv`, `mars_reference_values.csv`, `scores.png`, `map.html`

## How to run
Run `mars_analog_FINAL.ipynb` in Google Colab. An Earthdata account is required (free).
