# Aviation Accidents Analysis — 1919–2023

An exploratory analysis of recorded aviation events using **Python, Pandas, NumPy and Matplotlib**, with a **GeoPandas** choropleth map.

Developed for **Python Data Toolkit: Numpy, Pandas, Pyplot**, part of the **ProfessionAI Master in Data Analytics**. The project incorporates revisions following coach feedback on preprocessing and interpretation.

**[View the analysis notebook](Analisi_Incidenti_Aerei_1919_2023.ipynb)**

The notebook is written in Italian. This README provides an English overview.

## Project questions

- Which countries are most represented in the recorded events?
- How are events distributed across weekdays?
- Which operators and aircraft types are associated with more recorded events or fatalities?
- How do annual event counts evolve over time?
- What differences are visible in the time series before and after 2001?

The analysis is descriptive. Event counts and fatalities per recorded event are not measures of risk per flight.

## Data sources

- [Aviation accidents CSV supplied for the course](https://proai-datasets.s3.eu-west-3.amazonaws.com/aviation-accidents.csv)
- [Natural Earth country boundaries](https://naturalearth.s3.amazonaws.com/110m_cultural/ne_110m_admin_0_countries.zip)

The saved notebook outputs cover **23,967 records** with recoverable years from 1919 to 2023. The latest complete date is **15 May 2023**, so 2023 is a partial year.

Both sources are downloaded by the notebook and are not included as standalone files in the repository.

## Data preparation

The notebook inspects the raw data before applying cleaning rules and preserves the original values for comparison.

- **Fatalities:** expressions such as `2+ 3` are parsed as sums of non-negative integers. Unknown values remain missing, rather than being treated as zero. No `eval()` is used.
- **Dates:** years are recovered from the date string or the original year column without inventing missing days or months. Conflicting years are flagged and excluded from temporal analysis pending review.
- **Coverage:** weekday and monthly analyses use complete dates; annual analysis also uses records with a recoverable year.
- **Quality checks:** repeated dates and identical rows are reported, not automatically removed.
- **Labels:** `Unknown country` is excluded from the country ranking; generic `Unknown` and `private` operator labels are excluded from comparisons between individual operators.

## Selected results

Values below come from the saved outputs of the published notebook.

| Measure | Result |
|---|---:|
| Recorded events | 23,967 |
| Sum of fatalities in records with known values | 132,732 |
| Records with missing fatality information | 3,938 |
| Additive fatality expressions recovered | 353 |
| Records with complete usable dates | 23,408 |
| Most represented country | USA — 4,377 events |
| Peak year by recorded event count | 1944 — 1,505 events |
| Aircraft type with the largest sum of known fatalities | Douglas C-47A (DC-3) — 5,780 |
| Mean annual events, 1980–2000 | 240.67 |
| Mean annual events, 2002–2022 | 210.48 |

The fatality sum covers known values only. Country and aircraft rankings reflect the source's labels and recorded events, not comparative safety.

## Analysis and visualisations

The notebook contains nine charts covering fatality-information categories, country counts, weekdays, operators, aircraft types, long-term trends, annual and monthly comparisons around 2001, and a world map.

### Temporal comparison

Two equally sized 21-year windows, **1980–2000** and **2002–2022**, support the annual comparison. The transition year 2001 remains visible but is excluded from the averages; partial-year 2023 is shown separately. A monthly view for 1996–2006 marks 11 September 2001.

These comparisons do not isolate a causal effect of 9/11. Traffic volumes, historical coverage and operational conditions also change over time.

### Operator analysis

Operators with at least **20 recorded incidents** are examined using known-case mean fatalities and data-completeness indicators. The ordered severity comparison requires complete fatality information for the operator's recorded events. The threshold concerns incidents, not flights, and the result is not a safety ranking.

### Geographical bonus

The GeoPandas map uses present-day boundaries and explicitly reports unmatched geographical labels. The saved run maps **21,246 events**, with **2,721** associated with unmatched labels. Historical states are not arbitrarily assigned to a single modern successor, and grey areas do not establish an absence of accidents.

## Limitations

- The source does not provide total flights, flight hours or passengers carried, so exposure-adjusted risk cannot be calculated.
- Missing fatality values and incomplete dates limit completeness and comparability.
- Historical reporting may be uneven, and repeated records require event-level investigation.
- Operator and aircraft comparisons do not control for fleet size, operating period or civilian/military activity.
- Remote source files may change, affecting future runs.

## Repository contents

| File | Description |
|---|---|
| [Analisi_Incidenti_Aerei_1919_2023.ipynb](Analisi_Incidenti_Aerei_1919_2023.ipynb) | Analysis, methodological notes, saved tables and charts. |
| [README.md](README.md) | Project overview and running instructions. |
| [.gitignore](.gitignore) | Git ignore rules. |

## How to run

Download the notebook and upload it to Google Colab. Run the cells from top to bottom, including the initial GeoPandas installation cell. Internet access is required for the CSV and map data.

Alternatively, install the dependencies and open the notebook in Jupyter:

```bash
pip install pandas numpy matplotlib geopandas jupyter
```

## Author

[Claudio Lombardi](https://github.com/PsyClaudio)
