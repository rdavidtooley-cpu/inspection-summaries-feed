# Inspection Intel — Transcript Summaries Feed

Public read-only feed of conference call summaries for the 22-company Inspection Intel universe (NDT Services, Global NDT, Flow Control, Mech & On-Site Services).

This repository is **automatically updated** by the Inspection Intel morning pipeline on `Roberts-Mac-mini.local` at ~5:10 AM Central daily. Do not commit to this repo manually — your edits will be overwritten.

## What's in here

| File / folder | What it is |
|---|---|
| `transcript_summaries.json` | All summaries keyed by `<TICKER>_Q<n>_<YYYY>`. See **Schema** below for the exact entry shape. |
| `transcripts/` | Rendered HTML for each individual transcript summary. Named `<TICKER>_Q<n>_<YYYY>.html`. |

## Schema

Each entry in `transcript_summaries.json` is keyed `<TICKER>_Q<n>_<YYYY>` and looks like this:

```json
{
  "MG_Q3_2025": {
    "summary": "**KEY HIGHLIGHTS**\n- Q3 2025 revenue of $195.5 million…\n\n**SUMMARY**\n…\n\n**Q&A TAKEAWAYS**\n…\n\n**QoQ COMPARISON**\n…\n\n**KEY RISKS**\n…",
    "ticker": "MG",
    "quarter": 3,
    "year": 2025,
    "company": "Mistras Group",
    "date": "2025-11-05"
  }
}
```

| Field | Type | Always present? | What it is |
|---|---|---|---|
| `summary` | string (markdown) | Yes | The 5-section CEO brief: **KEY HIGHLIGHTS / SUMMARY / Q&A TAKEAWAYS / QoQ COMPARISON / KEY RISKS**. Parse sections by splitting on `**<HEADING>**`. |
| `ticker` | string | Yes (as of 2026-06-09) | The display ticker — same as the prefix of the key. Use this to join with your own ticker map (e.g. `BVI` → yfinance `BVI.PA`). |
| `quarter` | int 1–4 | Yes (as of 2026-06-09) | Fiscal quarter. |
| `year` | int (e.g. 2025) | Yes (as of 2026-06-09) | Fiscal year that the quarter belongs to. |
| `company` | string | Almost always (as of 2026-06-09) | Display company name. Omitted if the ticker isn't in the producer's static map (rare). |
| `date` | string `YYYY-MM-DD` | Almost always (as of 2026-06-09) | Calendar date the earnings call took place. May be omitted for sources that don't expose a clean date header. |
| `source_url` | string (URL) | Currently NOT present | Will be populated when the producer migrates from Koyfin to SEC 8-K / Motley Fool (expected ~2 weeks). Until then, omitted. |

**Schema history:**
- Before 2026-06-09: every entry was just `{ "summary": "<markdown>" }` — no other fields. Older consumers may need to parse ticker/quarter/year from the key.
- From 2026-06-09: `ticker`, `quarter`, `year`, `company`, `date` added. Additive change — pre-existing `summary` field unchanged.

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
