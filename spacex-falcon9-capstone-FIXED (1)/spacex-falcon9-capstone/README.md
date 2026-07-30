# Winning the Space Race with Data Science — SpaceX Falcon 9 Landing Prediction

**Author:** Abhinav Jagtap · July 2026

Predicting whether a SpaceX Falcon 9 first stage will land successfully, using data collected from the SpaceX REST API and Wikipedia, explored with SQL/visualization/Folium/Plotly Dash, and modeled with classification algorithms.

**Full report (PDF):** [`report/Data-Science-Capstone-Project-Report.pdf`](./report/Data-Science-Capstone-Project-Report.pdf)

## Key Results

- Collected and cleaned 90 Falcon 9 launch records (SpaceX API + Wikipedia cross-check)
- Overall historical landing success rate: **66.7%**
- Best launch site by success rate: **KSC LC-39A (76.9%)**
- Best classification model: **Decision Tree, 88.9% test accuracy** (vs. 83.3% for Logistic Regression, SVM, KNN)

## Repository Structure

```
spacex-falcon9-capstone/
├── notebooks/
│   ├── 01-data-collection-api.ipynb        # SpaceX REST API data collection
│   ├── 02-data-wrangling.ipynb             # Cleaning, imputation, binary Class label
│   ├── 03-eda-sql.ipynb                    # SQL-based exploratory analysis
│   ├── 04-folium-launch-sites.ipynb        # Interactive Folium map + proximity analysis
│   ├── 05-machine-learning-prediction.ipynb # Logistic Regression, SVM, Decision Tree, KNN
│   └── 06-data-collection-webscraping.ipynb # Wikipedia web scraping (BeautifulSoup) cross-check
├── dashboard/
│   ├── spacex_dash_app.py                  # Plotly Dash interactive dashboard
│   ├── spacex_launch_dash.csv              # Data used by the dashboard
│   └── requirements.txt
├── maps/
│   └── spacex_launch_site_map.html         # Standalone interactive Folium map
├── report/
│   ├── Data-Science-Capstone-Project-Report.pdf
│   └── Data-Science-Capstone-Project-Report.pptx
└── README.md
```

> **Status note:** `01-data-collection-api.ipynb` is code-complete and correctly structured, but has not yet produced a full clean run — it depends on `api.spacexdata.com`, which was returning a Cloudflare 525 (origin server) error as of this writing. Check [status.spacexdata.com](https://status.spacexdata.com) and re-run once the host is back up; no further code changes should be needed. `06-data-collection-webscraping.ipynb` depends only on Wikipedia and has not yet been run — run it top to bottom before submitting.

## How to Run

**Notebooks:** open any notebook in `notebooks/` with Jupyter. `01-data-collection-api.ipynb` requires internet access to `api.spacexdata.com`.

**Dashboard:**
```bash
cd dashboard
pip install -r requirements.txt
python spacex_dash_app.py
```
Then open `http://127.0.0.1:8050` in your browser.

**Map:** open `maps/spacex_launch_site_map.html` directly in any browser.

## Methodology

1. **Data Collection** — SpaceX REST API (`v4/launches/past`) for structured launch records, cross-checked against Wikipedia's "List of Falcon 9 and Falcon Heavy launches."
2. **Data Wrangling** — imputed missing payload mass, mapped landing outcomes to a binary `Class` label (1 = landed, 0 = did not land).
3. **EDA** — visualization (flight number, payload, orbit type, yearly trend) and SQL queries (launch sites, payload by customer/booster, landing outcome ranking).
4. **Interactive Visual Analytics** — Folium map of launch sites and proximities; Plotly Dash dashboard with site/payload filters.
5. **Predictive Analysis** — standardized features, 80/20 train/test split, four classifiers tuned via 10-fold `GridSearchCV`, compared on held-out test accuracy.

## Data Sources

- [SpaceX REST API](https://github.com/r-spacex/SpaceX-API)
- Wikipedia: [List of Falcon 9 and Falcon Heavy launches](https://en.wikipedia.org/wiki/List_of_Falcon_9_and_Falcon_Heavy_launches)
