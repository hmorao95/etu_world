# The Energy Transportation Uncertainty (ETU) Index
The Energy Transportation Uncertainty (ETU) index represents a novel approach to measuring disruptions in the critical midstream segment of *global* energy supply chains. Building on the established methodology of Baker, Bloom, and Davis (2016) for constructing economic policy uncertainty indices, this index systematically tracks threats and disruptions to energy transportation infrastructure through comprehensive media analysis.

**Reference**: Morão (2025)  
Hugo Morão,   
The economic effects of tensions in energy transportation,  
Research in Transportation Economics,  
Volume 112, 2025, 101598,  
https://doi.org/10.1016/j.retrec.2025.101598.  

## Economic Intuition Behind the Index
From an economic perspective, the ETU index captures a fundamental source of supply-side risk in energy markets. The midstream sector—encompassing pipelines, storage facilities, and transportation networks—serves as the crucial link between energy production and consumption. Disruptions in this segment can create significant bottlenecks, leading to price volatility, supply shortages, and broader economic uncertainty. By quantifying media coverage of these disruptions, the ETU index provides an early warning system for potential energy market stress.

## Construction Methodology
The index employs a text-mining approach that identifies relevant articles through three semantic categories: Energy terms (oil, gas, petroleum, energy), Transportation terms (pipeline, midstream, shipping, rail), and Uncertainty terms (threat, risk, concern, warn). Articles are included only when energy and transportation terms appear within five words of each other, ensuring precise identification of midstream disruptions rather than general energy or transportation news.

## Global Coverage and Data Quality
Beginning in January 1969, the index draws from an extensive network of English-language media sources across major economies including the United States, United Kingdom, Canada, Australia, Asia-Pacific nations, Middle Eastern countries, and key European markets. This global perspective is economically significant because energy transportation networks are inherently international, and disruptions in one region can have cascading effects across global energy markets. The published paper covers the period through December 2024; the data in this repository is periodically extended to the latest available month. The full list of sources, with each source's coverage window and importance weight, is provided in `config/sources.csv`.

The index thus serves as a valuable tool for understanding how transportation infrastructure risks translate into broader economic uncertainty, providing researchers and policymakers with quantitative insights into a previously difficult-to-measure aspect of energy market dynamics.

## Repository Structure
```
etu_world/
├── config/
│   ├── config.json      # search definition: boolean query, languages, interval
│   └── sources.csv      # media sources with coverage windows and importance weights
├── data/
│   ├── raw/
│   │   └── num_hits.csv # raw monthly article counts per source (index numerator and denominator)
│   └── processed/
│       ├── index.csv    # computed ETU index (two series)
│       ├── index.xlsx   # computed ETU index (spreadsheet)
│       └── etuindex_data.xlsx  # frozen dataset published with Morão (2025)
├── docs/
│   ├── paper.pdf        # the full research publication
│   └── etu_annotated.pptx      # annotated presentation materials
├── CITATION.cff         # machine-readable citation metadata
├── CHANGELOG.md         # record of notable changes
├── LICENSE              # license terms (CC BY 4.0)
└── README.md
```

## Reproducing the Index
The index is built in three stages, moving left to right through the folders above:

1. **Define the search** — `config/config.json` holds the exact boolean query (energy/transportation/uncertainty terms, the `NEAR5` proximity constraint, the word-count filter, and excluded subject codes) together with the target languages and reporting interval. `config/sources.csv` lists the media sources to query and the coverage window over which each is available.
2. **Collect raw counts** — running the query in `config.json` against each source in `sources.csv` (via the news database, e.g. Factiva) yields `data/raw/num_hits.csv`: for every source and month, the number of matching articles (`num_hits`) and the total number of articles published (`total_articles`).
3. **Compute the index** — the raw counts are scaled by each source's total article volume, aggregated across sources (optionally weighted by `importance`), and standardized to produce `data/processed/index.csv`. The result is provided in both CSV and XLSX form and covers 1969-01 through the latest available month.

### Data Dictionary
**`config/config.json`**
| Field | Description |
| --- | --- |
| `type` | Index type (`index`). |
| `languages` | Languages of the retrieved articles. |
| `interval` | Reporting frequency of the index (`Monthly`). |
| `search_text` | The full boolean query: uncertainty terms, an energy-industry code / energy terms placed within five words (`NEAR5`) of transportation terms, the word-count filter (`wc>150`), and excluded subject codes (`NOT ns=...`). |

**`config/sources.csv`**
| Column | Description |
| --- | --- |
| `name` | Source (publication) name. |
| `fry`, `frm`, `frd` | Coverage start — from year, month, day. |
| `toy`, `tom`, `tod` | Coverage end — to year, month, day. |
| `importance` | Relative weight of the source used in the weighted index series. |

**`data/raw/num_hits.csv`**
| Column | Description |
| --- | --- |
| `source` | Source name (matches `sources.csv`). |
| `year`, `month`, `day` | Period of the count (`day` empty for monthly aggregates). |
| `num_hits` | Number of articles matching the ETU query in that source-period. |
| `total_articles` | Total number of articles published by the source in that period (scaling denominator). |
| `error` | Retrieval error message, if any (empty on success). |
| `num_tries` | Number of retrieval attempts made. |

**`data/processed/index.csv`**
| Column | Description |
| --- | --- |
| `year`, `month` | Period of the observation. |
| `standardized` | Standardized (mean/standard-deviation normalized) ETU index, equal weighting. |
| `standardized weighted` | Standardized ETU index, weighted by source `importance`. |

## How to Cite
If you use this index or dataset, please cite the companion paper:

> Hugo Morão, "The economic effects of tensions in energy transportation," *Research in Transportation Economics*, Volume 112, 2025, 101598. https://doi.org/10.1016/j.retrec.2025.101598

A machine-readable citation is available in `CITATION.cff`, and GitHub's
"Cite this repository" button will generate APA and BibTeX entries from it.

## License
The data and documentation in this repository are released under the
[Creative Commons Attribution 4.0 International License (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).
You are free to share and adapt the material, including for commercial purposes,
provided you give appropriate credit by citing the paper above.
