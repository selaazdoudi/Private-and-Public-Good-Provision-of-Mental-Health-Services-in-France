# Private and Public Good Provision of Mental Health Services in France

**Authors:** Salma El Aazdoudi · Cynthia Francis · Anahi Reyes Miguel · Rafaël Mourouvin  
**Course:** Data Analysis in Economics: Collection and Visualisation — Telecom Paris (2025)

---

## Research Question

> To what extent is the private sector **substituting** for state-provided mental health services in France?

Using data scraped from [Psychologue.net](https://www.psychologue.net) and public statistics from DREES and INSEE, we examine the geographic relationship between the density of public *Centres Médico-Psychologiques* (CMPs) and the supply of independent (liberal) psychotherapists across French departments.

**Key finding:** A 10% increase in CMP density is associated with approximately an 8% reduction in the number of independent therapists, consistent with a substitution effect — though reverse causality cannot be excluded.

---

## Repository Structure

```
.
├── 01_data_collection.ipynb        # Web scraping (Selenium + hidden API)
├── 02_descriptive_analysis.ipynb   # Correlation matrix, binsreg, service stats
├── 03_maps_analysis.ipynb          # Choropleth maps (therapist & CMP density, services)
├── 04_regression_analysis.ipynb    # OLS regression: therapists ~ CMP density
│
├── data/
│   ├── raw/                        # Source files (geojson, xlsx, csv) — see note below
│   └── processed/                  # Outputs produced by the notebooks
│
└── figures/                        # All plots and maps saved as PNG
```

---

## Data Sources

| File | Source | Description |
|------|--------|-------------|
| `full_therapists.geojson` | [Psychologue.net](https://www.psychologue.net) (scraped) | One record per therapist: name, location, price, services, ratings |
| `departements.geojson` | IGN / OpenStreetMap | France department polygons |
| `POPULATION_MUNICIPALE_DEPARTEMENT_FRANCE.xlsx` | INSEE (2021) | Population and surface area by department |
| `data-2.xlsx` / `data.csv` | DREES (2019) | CMP density per 100,000 inhabitants by department |
| `cities.csv` | OpenStreetMap | French city coordinates for map annotation |

> **Note:** Raw data files are not included in this repository due to size and licensing constraints. Place them in `data/raw/` before running the notebooks.

---

## Notebook Overview

### `01_data_collection.ipynb`
Collects therapist data using two complementary methods:
- **Method 1 (Selenium + BeautifulSoup):** Automates browser clicks on the "load more" button to capture all therapist cards, then parses JSON-LD embedded in the HTML.
- **Method 2 (Hidden API):** Queries the site's undocumented internal REST API for paginated therapist records and real-time appointment availability.

Data was collected on **23 December 2024** and **13 January 2025**. The final merged dataset is saved as `therapists_final.csv`.

### `02_descriptive_analysis.ipynb`
Produces three types of exploratory analysis:
1. **Correlation matrix** of numeric platform features (price, rating, online presence, visibility score).
2. **Binned scatter plots** (via `binsreg`) of session price vs. distance from Paris, for both in-person and online consultations.
3. **Service specialty breakdown** — national counts and department-level most/least offered specialties.

### `03_maps_analysis.ipynb`
Generates four choropleth maps:
1. Private therapist density (per 100,000 inhabitants, by department).
2. CMP density (per 100,000 inhabitants, 2019).
3. Most offered psychological service per department.
4. Least offered psychological service per department + supporting barplot.

### `04_regression_analysis.ipynb`
Estimates six OLS regression models of the form:

$$\log(\text{Therapists}_d) = \alpha + \beta_1 \log(\text{CMP density}_d) + \beta_2 \cdot \text{Area}_d + \varepsilon_d$$

Robustness checks exclude Paris (Île-de-France), overseas territories (DOM-TOM), and both combined. Results are displayed in a `stargazer` publication-ready table and a coefficient plot.

---

## Installation

```bash
pip install geopandas pandas numpy matplotlib seaborn geopy binsreg stargazer \
            statsmodels mapclassify selenium webdriver-manager beautifulsoup4 \
            openpyxl tabulate
```

Python 3.9+ recommended. For Selenium (notebook 01), Chrome and `chromedriver` must be installed.

---

## Results Summary

| Model | β(log CMP density) | p-value | n |
|-------|-------------------|---------|---|
| Full dataset | −0.805 | < 0.01 | 100 |
| Online therapists | −0.631 | < 0.01 | 94 |
| Offline therapists | −0.753 | < 0.01 | 99 |
| Excl. Paris | −0.657 | < 0.01 | 92 |
| Excl. Overseas | −0.800 | < 0.01 | 96 |
| Excl. Paris & Overseas | −0.710 | < 0.01 | 88 |

---

## Citation

El Aazdoudi S., Francis C., Reyes Miguel A., Mourouvin R. (2025). *Private and Public Good Provision of Mental Health Services in France: An analysis based on Psychologue.net data.* Telecom Paris.
