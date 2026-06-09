# Inspection Intel — Transcript Summaries Feed

Public read-only feed of conference call summaries for the 22-company Inspection Intel universe (NDT Services, Global NDT, Flow Control, Mech & On-Site Services).

This repository is **automatically updated** by the Inspection Intel morning pipeline on `Roberts-Mac-mini.local` at ~5:10 AM Central daily. Do not commit to this repo manually — your edits will be overwritten.

## What's in here

| File / folder | What it is |
|---|---|
| `transcript_summaries.json` | All summaries keyed by ticker + quarter. Schema: `{ "<TICKER>_Q<n>_<YYYY>": { ticker, quarter, year, title, sections: [...], company, date, source_url } }`. Each summary follows the 5-section format: **KEY HIGHLIGHTS / SUMMARY / Q&A TAKEAWAYS / QoQ COMPARISON / KEY RISKS**. |
| `transcripts/` | Rendered HTML for each individual transcript summary. Named `<TICKER>_Q<n>_<YYYY>.html`. |

## How to consume

### Read the JSON directly (recommended for programmatic use)

```
https://raw.githubusercontent.com/rdavidtooley-cpu/inspection-summaries-feed/main/transcript_summaries.json
```

Fetch this URL once per morning (the pipeline updates it shortly after 5 AM CT). Parse the JSON and render however you want.

### Clone the repo (recommended for development / offline use)

```
git clone https://github.com/rdavidtooley-cpu/inspection-summaries-feed.git
```

To stay current, `cd inspection-summaries-feed && git pull` daily.

### Read individual transcript HTML files

```
https://raw.githubusercontent.com/rdavidtooley-cpu/inspection-summaries-feed/main/transcripts/MG_Q3_2026.html
```

Or after cloning: `cat transcripts/MG_Q3_2026.html`.

## What this feed is NOT

- Not a real-time feed — updated once daily.
- Not authoritative for prices, news, or anything other than transcript summaries.
- Not a substitute for the live Inspection Intel dashboard at `https://inspection-intel.pages.dev` (which requires auth).

## Source ticker universe (22 companies)

| Category | Tickers |
|---|---|
| NDT Services | MG, TISI, TIC, OII, XPRO, TRNS, THR |
| Global NDT | BVI.PA, ITRK.L, COTN.SW, SGSN.SW |
| Flow Control | FLS, ROR.L, IMI.L, SPX.L, WEIR.L, WHD |
| Mech & On-Site Services | MTRX, PRIM, MTZ, CLH, FET |

## Update cadence

The morning pipeline runs at ~5:10 AM Central. New transcripts (last 30 days) are downloaded from Koyfin, summarized via Claude CLI on Roberts-Mac-mini.local, and pushed here. If you're consuming the feed and don't see today's update by 7 AM CT, the pipeline likely failed — check Robert.

## License / use

Reference data for internal use. Not for redistribution. No warranty.
