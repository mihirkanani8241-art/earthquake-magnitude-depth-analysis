# Earthquake Magnitude and Depth Analysis

## Project overview
This beginner geoscience data-analysis project explores earthquake records from the USGS Earthquake Catalog using Python, Pandas, and Matplotlib.

Questions explored:
- How are earthquake magnitudes distributed?
- How do recorded depths vary?
- How do median magnitudes compare across selected depth groups?
- Is depth linearly associated with magnitude in this sample?

## Data source
**USGS Earthquake Catalog API:** https://earthquake.usgs.gov/fdsnws/event/1/query?format=csv&starttime=2026-09-10T00:00:00&endtime=2026-10-10T23:59:59&minmagnitude=2.5&orderby=time-asc&limit=20000

Query settings:
- Start: 2026-09-10 00:00:00 UTC
- End: 2026-10-10 23:59:59 UTC
- Minimum magnitude: 2.5
- Format: CSV
- Maximum records requested: 20,000

The latest saved snapshot analyzed here contains **1,896 records and 23 columns**, including a derived `date` column. USGS catalog records can be updated, so a fresh API query may return different values. The file `earthquake_data.csv` is intended to preserve the exact snapshot used for these results.

## Tools
- Python
- Pandas
- Matplotlib
- Google Colab

## Workflow
1. Downloaded earthquake records from the USGS API.
2. Inspected columns, data types, and missing values.
3. Converted `time` to a UTC-aware datetime and extracted `date`.
4. Counted records by date.
5. Identified the largest-magnitude record in the downloaded sample.
6. Calculated magnitude and depth statistics.
7. Plotted magnitude distribution and magnitude versus depth.
8. Compared records in three selected depth groups.

## Results from the latest saved snapshot

### Overall statistics
- Records: **1,896**
- Columns: **23** (including the derived `date` column)
- Largest magnitude found: **7.7**
- Depth of that record: **12.647 km**
- Reported location: **12 km WSW of Pitaloza Arriba, Panama**
- Mean magnitude: **3.776**
- Median magnitude: **4.0**
- Mean reported depth: **56.235 km**
- Minimum reported depth: **-3.43 km**
- Maximum reported depth: **665.057 km**
- Pearson correlation between depth and magnitude: **0.1521** (weak positive linear association)

### Magnitude categories
These bins were chosen for this exercise and are not universal scientific classifications.

| Category | Definition | Count |
|---|---|---:|
| Small | Magnitude < 4 | 927 |
| Moderate | 4 <= magnitude < 6 | 961 |
| Large | Magnitude >= 6 | 8 |

### Depth-group comparison
These are simplified groups for descriptive analysis.

| Group | Definition | Count | Median magnitude |
|---|---|---:|---:|
| Shallow | Depth < 70 km | 1,458 | 3.525 |
| Intermediate | 70 km <= depth <= 300 km | 371 | 4.2 |
| Deep | Depth > 300 km | 67 | 4.3 |

Median magnitudes increase across these selected groups in this sample (3.525, 4.2, and 4.3). This is a descriptive pattern only.

## Interpretation and limitations
- A Pearson correlation of approximately **0.152** indicates a weak positive linear association between depth and magnitude in this dataset.
- The depth groups have unequal sample sizes: 1,458 shallow, 371 intermediate, and 67 deep records.
- These results do not establish that depth causes magnitude differences or that the pattern applies to all earthquakes.
- The query includes only earthquakes with magnitude >= 2.5; it does not represent all earthquakes.
- USGS catalog locations, magnitudes, and depths may be revised.
- The minimum reported depth (-3.43 km) is unusual. Check the original record and catalog definitions before deciding whether to modify or remove it.
- A more rigorous study should consider geographic and tectonic context, magnitude types, catalog completeness, and uncertainty.

## Reproducing the analysis
1. Open https://colab.research.google.com/ and create or open the notebook.
2. Open **[Earthquake Data Analysis with Python.ipynb](Earthquake%20Data%20Analysis%20with%20Python.ipynb)**.
3. To reproduce the exact saved results, load the saved `earthquake_data.csv` snapshot rather than re-querying the live USGS API. To refresh the analysis, rerun the API query and expect some numbers to change.
4. Run the notebook cells in order.
5. Export the summary with:

```python
summary.to_csv("earthquake_depth_summary.csv", index=False)
```

## Repository files
- `README.md` — project documentation
- `Earthquake Data Analysis with Python.ipynb` — code, outputs, and plots
- `earthquake_depth_summary.csv` — depth-group counts and median magnitudes
- `earthquake_data.csv` — exact data snapshot used for these results

## Project status
**Beginner exploratory analysis completed.** Further validation and deeper geoscientific interpretation remain future improvements.
