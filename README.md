# Mars on Earth: Terrestrial Analogs for Utopia Planitia (Viking 2 site)

NASA Space Apps Challenge, Giza. Team: [your name]

## Question
Which Earth regions are closest to the Viking 2 site in Utopia Planitia, on which variables, and where does the analogy break down?

## Data
Mars (Viking 2 lander, NASA PDS Atmospheres Node): binned meteorology (air temperature, wind), daily average pressure, atmospheric optical depth.
Earth (NASA Earthdata, MERRA-2 monthly, 2022): M2TMNXSLV, M2TMNXAER, M2TMNXLND, M2C0NXASM.

## Mars reference values (Viking 2)
| Variable | Value |
|---|---|
| Air temperature (1.6 m) | 193.7 K |
| Wind speed | 4.48 m/s |
| Pressure | 874 Pa |
| Optical depth | 0.85 |
| Vegetation, surface soil moisture | 0 (assumption) |

## Method
Six Earth sites chosen from the literature. Similarity score per variable = 100 x (1 - |Earth - Mars| / scale), clipped to 0-100. Five variables are scored (temperature, dust, vegetation, soil moisture, wind); the total is the weighted mean, missing values ignored. Elevation is not scored (not comparable with Mars datum elevation). Pressure is reported separately. Sensitivity analysis with 4 weighting scenarios.

## Results
| Rank | Site | Total score | Rank in 4 scenarios |
|---|---|---|---|
| 1 | Taklamakan (China) | 66.7 | 1, 1, 1, 1 |
| 2 | Gilf Kebir (Egypt) | 51.3 | 2, 2, 2, 3 |
| 3 | Tibesti (Chad) | 50.0 | 3, 3, 4, 4 |
| 4 | Lut Desert (Iran) | 50.0 | 4, 4, 3, 2 |
| 5 | Puna de Atacama (Chile) | 35.4 | 5, 5, 6, 5 |
| 6 | Dry Valleys (Antarctica) | 27.5 | 6, 6, 5, 6 |

Taklamakan is the closest match. Its strongest variable is dust (99.4) and its weakest is temperature (0.0). Rank 1 holds in all four scenarios; ranks 2 to 6 shift.

Interactive map: https://b0489677-ctrl.github.io/mars_analog/map.html

## Where the analogy fails
- Earth surface pressure at these sites is about 70 to 108 times Mars' 874 Pa.
- Earth cannot reproduce Mars' gravity (about 38% of Earth's), radiation or CO2 atmosphere.
- All Earth sites are warmer than the Viking 2 site (temperature scores 0 to 11 out of 100).

## Limitations
- One lander site, one Earth year (2022)
- MERRA-2 is a model with about 50 km resolution
- Viking temperature is air temperature at 1.6 m; optical depth includes dust and ice haze
- Mars vegetation and surface soil moisture are assumed to be zero

## Files
- mars_analog_FINAL.ipynb: Earth data download, scoring, sensitivity, map
- results.csv, sensitivity.csv, mars_reference_values.csv, scores (1).png, map.html
- vl_* files: raw Viking 2 data files

## How to run
Run mars_analog_FINAL.ipynb in Google Colab. A free Earthdata account is required.
