# Cocoa prices and West African rainfall

Does rainfall in the Ivory Coast and Ghana cocoa belt predict the global cocoa price, and does the market react immediately or only when the harvest comes in?

The full pre-registered hypothesis, method, results and limitations are in [`hypothesis.md`](hypothesis.md).

## Data

- **Price:** [FRED PCOCOUSDM](https://fred.stlouisfed.org/series/PCOCOUSDM). IMF global cocoa price, USD/tonne, monthly, from 1992. Saved in `data/raw/PCOCOUSDM.csv`.
- **Rainfall:** [NASA POWER](https://power.larc.nasa.gov/) daily point API, `PRECTOTCORR`, from 1981, at eight points across the Ivorian and Ghanaian cocoa belt. Downloaded live when the notebook runs.

## Method in brief

1. Monthly rainfall at eight points, averaged into one regional series.
2. Standardised anomalies against each calendar month's long-run mean and standard deviation, signed and absolute.
3. Monthly log price changes regressed on the anomaly at lags 0–6: 14 pre-specified regressions with Newey–West (HAC) standard errors.
4. Season-level version: April–August rainfall against the September → February price change.
5. Robustness check excluding 2023–24.

## Findings

- **Full sample:** none of the 14 monthly regressions is significant at 5%. No evidence that rainfall predicts cocoa price changes.
- **Excluding 2023–24:** a month 1 standard deviation wetter than normal is followed by a price change about 1.2% lower the next month (p = 0.005, R² ≈ 3%). It has the expected sign but doesn't pass a correction for 14 tests, so it's suggestive rather than established.
- **No delayed reaction:** lags 4–6, where a harvest-timed price response would appear, show nothing in either sample. This is consistent with markets pricing weather in quickly.
- **No "unusual weather" effect:** the absolute anomaly (drought or excess rain) shows no reliable relationship outside the 2023–24 drought period.

## Repository

```
cocoa.ipynb        analysis notebook, run top to bottom
hypothesis.md      hypothesis, method, results, limitations
data/raw/          FRED price series
```

## Running it

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

Open `cocoa.ipynb` in VS Code or Jupyter, select the `.venv` kernel and run all cells. The NASA POWER download needs an internet connection and takes a minute or two.
