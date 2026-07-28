**English** | [한국어](./README.ko.md)

# News/Search Trends & Stock Market Response

> Exploratory analysis of market-attention proxies and next-trading-day price and volume responses
> 4-person team project · Year 2, Semester 2, 2025

## Project Overview

This project explored whether changes in news volume and search activity were associated with next-trading-day stock-price and trading-volume responses. News counts and search volume were combined into an `issue_intensity` variable as an interpretive **market-attention proxy**.

In this project, the term FOMO does not mean that investor psychology or behavior was directly observed or measured. The analysis was exploratory and was not designed to establish causality or validate a trading strategy.

## Research Question

The project considered days with increased news and search activity as periods of higher market attention and explored three questions:

1. Is higher market attention associated with the direction of next-trading-day returns?
2. Is higher market attention associated with next-trading-day trading volume?
3. Can stock-level response patterns be grouped through exploratory clustering?

## Project Status

| Item | Current public status |
|---|---|
| Project type | **Team Project** |
| Repository type | **Documentation + sanitized refactored Notebook** |
| Project documentation | Public in this README |
| Data documentation | Public in [`data/README.md`](./data/README.md) |
| Analysis code and Notebook | [`notebooks/01_team_integrated_analysis.ipynb`](./notebooks/01_team_integrated_analysis.ipynb) |
| Original, derived, and sample data | Not public in this repository |
| Environment list | [`requirements.txt`](requirements.txt) is public but does not pin package versions |
| Independent reproduction | **Conditional; no end-to-end public-data run** |

The public Notebook exposes a reviewed analysis flow, but the methodology and numerical values below remain historical records from the original team documents. They cannot be recalculated or independently verified without compatible, permitted source data.

## Data Sources

| Source | Data | Intended use |
|---|---|---|
| [KRX Information Data System](https://data.krx.co.kr/) | Daily prices, trading volume, and investor-flow fields | Price, volume, and flow responses |
| [Naver DataLab](https://datalab.naver.com/) | Search volume by stock | Public-attention proxy |
| [BIGKinds](https://www.bigkinds.or.kr/) | News-article counts by stock | News-attention proxy |

The historical analysis covered 10 stocks: Samsung Electronics, NAVER, Kakao, Hyundai Motor, LG Energy Solution, Celltrion, Ecopro, Pearl Abyss, POSCO Future M, and Hanwha Ocean.

The original team documents record an integrated dataset of **3,620 rows × 29 variables**. This figure is an unverified historical record. The analysis period, collection dates, and rationale for selecting the 10 stocks cannot be confirmed from the public repository.

The user approved publication of the reviewed team code on 2026-07-29. Original CSV, XLSX, and HWP files, copied figures, and the team report remain excluded because code approval does not establish data redistribution or document-publication rights.

## Methodology

The original team documents and the public refactored Notebook describe the following workflow. The Notebook was statically checked, but the steps have not been independently verified end to end because the input data are not public.

### Historical data processing

1. Reshape stock-level wide-format data into long format using `date`, `종목`, and `변수`.
2. Merge news, search, and market data using `date` and `종목`.
3. Create `next_trade_date` to associate events on market holidays with the next trading day.
4. Forward-fill price and holding-related fields.
5. Fill missing trading-volume and investor-flow fields with `0` according to the analysis definitions.
6. Apply `log1p` transformations to news counts and search volume.

| Variable | Historical definition |
|---|---|
| `뉴스_log` | `log1p(뉴스건수)` |
| `검색_log` | `log1p(검색량)` |
| `이슈강도` | `뉴스_log + 검색_log` |
| `등락률_abs` | Absolute value of the daily return |
| `거래량_log` | `log1p(거래량)` |
| `등락률_next` | Next-trading-day return |
| `거래량_log_next` | Next-trading-day log trading volume |

### Historical analysis design

- **Clustering:** Standardize summary measures related to return volatility and trading-volume spikes, then apply the historically recorded K-Means setting of `K=3`.
- **Event comparison:** Select the single highest-`이슈강도` date for each stock and compare returns and trading volume around that event.
- **Holiday handling:** Associate an event on a market holiday with the next trading day.
- **Correlation review:** Compare `이슈강도` with next-trading-day returns and trading volume, including stock-level differences.

These methods applied techniques learned in class to a limited exploratory dataset. They do not constitute a new algorithm or a validated causal model.

## My Contribution

- Collected Naver search-volume data together with the other team members.
- Organized BIGKinds news data together with the other team members.
- Completed the final consolidation of the collected data and analysis results.
- Was responsible for the main visualization work.

## Historical Findings

The following values are **unverified historical records** from the original team documents:

| Comparison | Historical record | Current verification status |
|---|---:|---|
| `이슈강도` vs. next-trading-day return | Approximately `0.03` | Cannot be recalculated or independently verified |
| `이슈강도` vs. next-trading-day trading volume | Approximately `0.56` | Cannot be recalculated or independently verified |

The original team documents also record that one of the `K=3` clusters contained only Ecopro. This singleton-cluster result cannot be verified from the public repository and should not be generalized as a stable market pattern.

These observations describe associations in a limited historical analysis. They do not establish a causal relationship between news or search activity and subsequent price or volume changes.

## Limitations

- News volume and search volume are indirect market-attention proxies, not direct measurements of investor FOMO, psychology, or behavior.
- The analysis did not separate positive and negative news, so different meanings of increased attention may be mixed.
- The sample was limited to 10 stocks and one representative event per stock.
- The correlations did not control for stock, market, or time effects and must not be interpreted causally.
- The historical `K=3` setting and singleton-cluster record cannot be verified with the public materials.
- A sanitized refactored Notebook is public, but original, derived, and sample data are not.
- The public Notebook has not completed a clean end-to-end run with permitted source data.
- The historical numerical values and clustering result cannot currently be independently validated.

## Lessons Learned and Next Steps

Organizing and visualizing search and news data reinforced that these variables are closer to indirect measures of market attention than direct measurements of investor psychology.

The project also showed that an interesting visualization does not justify a causal conclusion, and that a cluster containing only one stock is too unstable to generalize as a recurring market pattern.

Future work would test whether the observations remain stable across different analysis periods and cluster counts.

## Public Code

- [`notebooks/01_team_integrated_analysis.ipynb`](./notebooks/01_team_integrated_analysis.ipynb)

The Notebook is a `PORTFOLIO_REFACTORED_VERSION` of a team artifact. It may differ from the historically submitted or presented file and is not presented as solely authored code. Embedded outputs, execution counts, copied news excerpts, individual article links, local absolute paths, and inline installation commands were removed.

The separate two-stock visualization candidate was not selected because its sources and input files do not match the primary public flow.

## Reproduction Status

`STATICALLY_VALIDATED` · `CONDITIONAL_REPRODUCIBILITY` · `FULL_RUN_NOT_VERIFIED`

Code inspection is available through the public Notebook. Original, derived, and sample data are not redistributed, so execution requires compatible data obtained under the relevant source conditions. The Notebook has zero stored outputs and has not been clean-run in this repository. In addition, `requirements.txt` lists package names without fixed versions. The historical values and clustering result therefore remain unverified.

---

[Back to English Profile](https://github.com/jun5007) · [View English Portfolio](https://jun5007.github.io/)
