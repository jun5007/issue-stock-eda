**English** | [한국어](./README.ko.md)

# Data Access and Expected Schema

Status: `SCHEMA_ONLY` · `NO_DATA_INCLUDED` · `LICENSE_REVIEW_REQUIRED`

This directory contains documentation only. It does not contain raw, derived,
synthetic, or sample rows.

## Expected local inputs

The public Notebook expects these local-only files under `data/`.

### `주식통합.xlsx`

| Column or group | Expected type | Use |
|---|---|---|
| `일자` | date-like text or datetime | Parsed strictly by pandas and converted to `date` |
| `종목` | string | Stock identifier |
| `종가`, `시가`, `고가`, `저가`, `대비`, `등락률` | numeric | Price and return fields |
| `거래량`, `거래대금` | numeric | Trading activity |
| `시가총액`, `상장주식수`, `외국인 보유수량`, `외국인 지분율`, `외국인 한도수량`, `외국인 한도소진율` | numeric | State fields used by the historical preprocessing |
| `개인(매도)`, `개인(매수)`, `개인(순매수)` | numeric | Investor-flow fields |

### `뉴스, 검색 데이터.xlsx`

| Column pattern | Expected type | Use |
|---|---|---|
| `일자` | date-like text or datetime | Merge key |
| Stock-specific columns containing `검색량` and ending in `_<stock>` | numeric | Search-attention values; the suffix becomes the stock key |
| Stock-specific columns beginning with `NEWS 건수_` or `건수_` and ending in `_<stock>` | numeric | News-count values; the suffix becomes the stock key |

Column names and types are expectations inferred from the reviewed code. They
have not been validated against a publishable source dataset.

## Local derived output

The Notebook may create:

```text
outputs/derived/이슈기준_통합데이터_final.csv
```

This is an output, not an input. `outputs/` and all CSV/XLSX files are ignored
and must not be committed.

## Historical integrated schema

The original team document records 3,620 rows and 29 variables including:

`date`, `종목`, `검색량`, `뉴스건수`, `종가`, `등락률`, `거래량`,
`개인(순매수)`, `뉴스_log`, `검색_log`, `이슈강도`, `등락률_abs`,
`거래량_log`, `next_trade_date`, `등락률_next`, and
`거래량_log_next`.

This is an unverified historical record, not a public dataset or a guaranteed
schema.

## Rights and source constraints

The project used KRX market data, Naver DataLab search-volume data, and
BIGKinds news-volume data. Code-publication approval does not establish
redistribution rights for those datasets or derived rows. Obtain each source
through its permitted access process and review its current terms before use.

No copied news text, individual article link collection, team report, or
presentation is included.

`이슈강도` is an indirect market-attention proxy. It is not a direct
measurement of investor psychology or FOMO.

---

[Back to English Project README](../README.md)
