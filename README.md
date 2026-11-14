# Mars on Earth: Terrestrial Analogs for Utopia Planitia (Viking 2 site)

NASA Space Apps Challenge, Giza. Team: [The Powerpuff Girls]

## Question
Which Earth regions are closest to the Viking 2 site in Utopia Planitia, on which variables, and where does the analogy break down?

Utopia Planitia is a cold northern plain where radar has detected buried ice, and Viking 2 gave us real surface measurements there.

## Data
**Mars (Viking 2 lander, NASA PDS Atmospheres Node, volume `vl_1001`):**
- `VL1/VL2-M-MET-4-BINNED-P-T-V-V1.0`: air temperature, wind
- `VL1/VL2-M-MET-4-DAILY-AVG-PRESSURE-V1.0`: pressure
- `VL1/VL2-M-LCS-5-ATMOS-OPTICAL-DEPTH-V1.0`: atmospheric optical depth

**Earth (NASA Earthdata, MERRA-2 monthly means, 2022):** `M2TMNXSLV` (2 m air temperature, 2 m wind, pressure), `M2TMNXAER` (dust), `M2TMNXLND` (LAI, surface soil wetness), `M2C0NXASM` (elevation)

## Mars reference values (computed from Viking 2 files)
| Variable | Value | Notes |
|---|---|---|
| Air temperature (1.6 m) | 193.7 K (-79.5 C) | Balanced by season and time of day; 21,152 good-quality bins; range 149.3 to 247.4 K |
| Wind speed | 4.48 m/s | 95th percentile of bins: 12.2 m/s |
| Pressure | 874 Pa | 970 valid daily means (sols 0 to 1050); range 7.36 to 10.20 mbar |
| Optical depth | 0.85 | Season-balanced median of 452 points; 0.45 for Ls 0-180, 1.13 for Ls 180-360 |
| Vegetation (LAI), surface soil moisture | 0 | Assumption |

Missing, interpolated and lander-interference bins were excluded using the PDS quality flags. Averages were balanced by season (12 bins of solar longitude) so seasons sampled more often do not bias the result.

## Method
- 8 Earth sites chosen from the literature before running the numbers: [list of sites]
- Five scored variables: temperature, dust, vegetation, soil moisture, wind.
- Score per variable = 100 x (1 - |Earth - Mars| / scale), clipped to 0-100. Scales: temperature 100 K, dust 0.5, vegetation 1, soil moisture 1, wind 5 m/s.
- Total score = weighted mean; missing values are ignored, not counted as zero.
- Elevation is not scored: Utopia lies about 4 km below the Mars datum, so almost every Earth site would score 0.
- Pressure is reported separately.
- Sensitivity analysis: 4 weighting scenarios (equal, temperature x3, dust+wind x3, with elevation).

## Results
[Paste the new ranking table: rank, site, total score, rank in the 4 scenarios]

[One sentence: best site, its strongest and weakest variable, whether the ranking is stable.]

![Similarity per variable](scores%20.png)

Interactive map: `map.html` (download and open in a browser) [or the GitHub Pages link if enabled]

## Where the analogy fails
- Earth surface pressure at these sites is about [X] to [Y] times Mars' 874 Pa.
- Earth cannot reproduce Mars' gravity (about 38% of Earth's), radiation or CO2 atmosphere.
- All Earth sites are warmer than the Viking 2 site; temperature is the weakest variable.

## Limitations
- One lander site and one Earth year (2022). Viking 2 data cover about 1.6 Mars years.
- MERRA-2 is a model with about 50 km resolution, so small sites (e.g. Meteor Crater) are not resolved.
- Viking temperature is air temperature at 1.6 m; MERRA-2 2 m air temperature is used for comparison.
- Optical depth includes dust and ice haze, was measured at about 670 nm, and the limitation flags were not filtered (52 of 452 points have flag 1 or 2).
- Antarctic and other ice-covered cells can have missing or non-comparable vegetation and soil moisture values.
- Mars vegetation and surface soil moisture are assumed to be zero.

## Files
- `mars_analog_FINAL.ipynb`: Earth data download (Earthdata), scoring, sensitivity analysis, map
- `viking2_extraction.ipynb`: computes the Mars reference values from the Viking 2 files
- `results.csv`, `sensitivity.csv`, `mars_reference_values.csv`, `scores .png`, `map.html`
- `vl_*` files: raw Viking 2 data and labels from the PDS Atmospheres Node (public NASA data). File names contain a space; remove it to run the extraction notebook.

## How to run
1. Run `viking2_extraction.ipynb` in Google Colab (upload the `vl_*` files) to print the Mars reference values.
2. Run `mars_analog_FINAL.ipynb` in Google Colab. A free NASA Earthdata account is required, and the GES DISC application must be approved in the Earthdata profile.
