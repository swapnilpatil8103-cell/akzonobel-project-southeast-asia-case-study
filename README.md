# Project Southeast Asia
## Independent Sell-Side M&A Reconstruction — AkzoNobel Southeast Asia Decorative Paints

> **Disclaimer:** This project is an independent student analysis/reconstruction based on publicly available information. It is not affiliated with, commissioned by, or representative of Goldman Sachs or AkzoNobel.

---

## 1. Project Objective

This project builds a realistic, fully-sourced sell-side M&A execution case study around the reported potential sale of AkzoNobel's Southeast Asian decorative paints assets. It is not a Goldman Sachs work product and does not claim any access to the actual transaction process, confidential information, or Goldman Sachs' internal analysis.

The objective is **defensibility, not polish**: every material number in this project traces to one of three places — a cited public source, a disclosed formula applied to public sources, or a clearly labeled illustrative assumption with a stated rationale. Where public information does not support a conclusion, that gap is stated explicitly rather than filled in.

The project demonstrates: investment banking financial modeling, carve-out modeling, M&A valuation (DCF, trading comparables, precedent transactions), buyer analysis, sell-side process design, pitch-book and information memorandum construction, and source discipline.

## 2. Transaction Background

AkzoNobel N.V. (the Dutch listed paints and coatings manufacturer) has reportedly engaged Goldman Sachs to explore a sale of its Southeast Asian decorative paints operations — spanning Indonesia, Thailand, Malaysia and Vietnam — generating approximately EUR 300m (USD 346m) of annual revenue. The process reportedly follows CEO Greg Poux-Guillaume's April 2026 public comments regarding a potential divestiture, with non-binding offers reportedly due by mid-September 2026. Siam Cement Group (SCG) has been reported as a party to preliminary discussions; other global paints strategics (Sherwin-Williams, PPG, Nippon Paint, Kansai Paint, Asian Paints, Berger Paints) are named in market commentary as plausible bidders. The Seller has reportedly signaled openness to either a single whole-region sale or a country-by-country sale to whichever buyer offers the greatest synergies in each market.

**Primary source:** ION Analytics/Mergermarket, "AkzoNobel taps Goldman Sachs for sale of Southeast Asia paints assets" (SRC-001). See [01_Source_Data/Transaction_Research.md](01_Source_Data/Transaction_Research.md) for the full fact table.

## 3. Scope

The project covers the full sell-side workstream: transaction research, asset perimeter mapping, a carve-out financial model, trading comparables, precedent transactions, valuation triangulation, buyer analysis, a sell-side pitch deck, an information memorandum, an assumptions book, and a source database. It deliberately **does not** attempt to price a specific bid, does not simulate confidential buyer behavior, and does not claim knowledge of any actual Goldman Sachs valuation, buyer list, or process detail.

The modeled perimeter is treated as **Decorative Paints only**, in the four named countries — an analyst inference based on the source article's specific language, not a confirmed transaction scope. Performance Coatings facilities identified in the same countries are treated as outside the perimeter. See [01_Source_Data/SEA_Asset_Perimeter.xlsx](01_Source_Data/SEA_Asset_Perimeter.xlsx) for the full reasoning.

## 4. Source Methodology

Sources were prioritized in three tiers:

- **Tier 1** — AkzoNobel annual reports/press releases/investor materials, government tax statistics, LEI registry entity data, official transaction announcements.
- **Tier 2** — ION Analytics/Mergermarket, Reuters/Bloomberg-adjacent coverage, Coatings World, PCI Magazine, OECD publications.
- **Tier 3** — Company brand websites, secondary financial-data aggregators (stockanalysis.com, GuruFocus, companiesmarketcap.com), general trade press.

This project had **no access to a licensed market-data terminal** (Bloomberg, Capital IQ, Refinitiv) or a paywalled Mergermarket subscription — the ION Analytics article itself was accessed via an AI-summarized page fetch, not a verbatim read, and is flagged as such in [01_Source_Data/Transaction_Research.md](01_Source_Data/Transaction_Research.md). All other web research was performed via AI-mediated search and page-fetch tools. Several Tier 3 sources showed material cross-source inconsistency (e.g., Sherwin-Williams' and AkzoNobel's own market capitalization varied by 10-20% across aggregators depending on date; Berger Paints India's reported EV/EBITDA was internally inconsistent with its disclosed net income). These are flagged individually at the point of use rather than silently reconciled.

The full source log — 36 sources (SRC-001 to SRC-036), tier-classified, with the specific fact each supports and where it was used — is at [10_Supporting_Research/Support_Sources.xlsx](10_Supporting_Research/Support_Sources.xlsx).

## 5. Fact vs. Estimate Methodology

Every transaction-specific and financial claim in this project is classified as one of four things:

| Classification | Meaning |
|---|---|
| **PUBLIC FACT** | Directly reported by AkzoNobel, ION Analytics, a company filing, a government source, or another credible source. |
| **ANALYST CALCULATION** | A calculation derived from public information via a disclosed formula (e.g., a blended tax rate, an implied multiple from two disclosed figures). |
| **ILLUSTRATIVE ASSUMPTION** | An assumption required because asset-level information is not publicly disclosed — always accompanied by a stated rationale and, where relevant, a sensitivity note. |
| **UNAVAILABLE / NOT PUBLICLY DISCLOSED** | Flagged explicitly as a gap. Never filled in with an invented number. |

This discipline is applied consistently in every workbook (color-coded: blue = input/assumption, black = formula, green = cross-sheet link) and is the single most important rule governing this project. No confidential Goldman Sachs valuation, buyer list, bid, synergy figure, or process detail is claimed or implied anywhere in this project.

## 6. Model Methodology

The carve-out financial model ([02_Financial_Model/Project_Southeast_Asia_Financial_Model.xlsx](02_Financial_Model/Project_Southeast_Asia_Financial_Model.xlsx)) is built from the single public revenue anchor (EUR 300m, FY2025) because AkzoNobel does not disclose SEA-decorative-specific financials of any kind. It is **not** a generic AkzoNobel consolidated forecast scaled down — it is a purpose-built carve-out with:

- A country-level revenue split (Indonesia/Thailand/Malaysia/Vietnam) — illustrative, anchored to each country's confirmed asset footprint.
- An EBITDA margin path anchored to AkzoNobel's **actual, disclosed** global Decorative Paints segment margin (14.2% FY2024, 15.8% FY2025) as a starting proxy, ramping toward regional peer margins.
- An explicit carve-out cost bridge separating standalone operating expenses from TSA costs and stranded/standalone-replacement costs, each modeled to phase out over the first two forecast years.
- A working capital schedule (DSO/DIO/DPO), capex/D&A schedule, and a blended effective tax rate calculated from the four countries' actual statutory CIT rates weighted by the revenue split.
- A 3-year "historical" period (FY2023-FY2025) that is explicitly **not** observed historical data — FY2023/FY2024 are back-solved from the FY2025 anchor using an illustrative growth assumption, and the workbook's own README says so.

Every input beyond the EUR 300m anchor and the four statutory tax rates is an ILLUSTRATIVE ASSUMPTION, documented cell-by-cell in the model's Assumptions tab and consolidated in [09_Assumptions/Support_Assumptions.xlsx](09_Assumptions/Support_Assumptions.xlsx).

**Note on formula verification:** the workbooks were originally built on a machine without LibreOffice, so for most of the project their formulas were verified by manual cell-by-cell audit and by independently replicating the financial model's calculation chain in plain Python. **On 2026-10-09 a LibreOffice headless recalculation pass was run**: `02_Financial_Model` and `05_Valuation` were recalculated and saved with stored values, and the other workbooks were recalculated as throwaway copies for an error scan. No `#REF!`, `#DIV/0!`, `#NAME?`, `#VALUE!` or other error values were found in any workbook. That pass also exposed a terminal-value formula bug in `DCF_Valuation!F10`, since fixed (see `10_Supporting_Research/Quality_Control_Review.md`, Addendum E).

## 7. Valuation Methodology

Enterprise Value is triangulated across three methodologies, consolidated in [05_Valuation/Project_Southeast_Asia_Valuation.xlsx](05_Valuation/Project_Southeast_Asia_Valuation.xlsx):

1. **DCF** — unlevered FCF from the carve-out model, discounted at a WACC of ~8.9% (built up from risk-free rate, ERP, a real live peer-median beta of 0.821, and a SEA country risk premium), with a full WACC × terminal-growth sensitivity table. Base case ≈ **EUR 613m**, range **EUR 468-908m**.
2. **Trading Comparables** — Sherwin-Williams, PPG, Nippon Paint, Kansai Paint, Asian Paints, Berger Paints (AkzoNobel shown for reference only, excluded from statistics as the seller). Median EV/Revenue 2.83x, median EV/EBITDA 15.2x — computed across a complete, live, single-source 6-company dataset (Yahoo Finance, pulled 2026-09-18), still influenced by Asian Paints' rich India-market multiple.
3. **Precedent Transactions** — five paints & coatings deals, most notably JSW/AkzoNobel India (25x EBITDA, excluded from the range as an India-specific outlier), the Sherwin-Williams/BASF Suvinil deal (the closest structural match), and Nippon Paint's rejected EUR 7.5bn offer for AkzoNobel's global Decorative Paints segment.

**The three methodologies do not converge** — this is disclosed as a genuine finding, not smoothed over. A recommended primary range of **EUR 500-775m** (midpoint EUR 625m) is presented as an explicit analyst judgment call, anchored on the DCF base case and cross-checked against the two most structurally comparable precedents, with full written rationale in the Triangulation tab. **Equity Value cannot be calculated** — no public disclosure of asset-level debt or cash exists for the carve-out perimeter.

**Data refresh (2026-09-18):** the WACC's beta input and the entire trading comps dataset were originally illustrative/secondary-aggregator placeholders; they were subsequently updated to live market data (Yahoo Finance via yfinance, one consistent pull across all 6 peers), which is what the figures above now reflect. See 09_Assumptions/Support_Assumptions.xlsx and 10_Supporting_Research/Support_Sources.xlsx (SRC-034) for full methodology.

## 8. Buyer Analysis Methodology

Buyer fit is assessed using an **evidence → strategic implication → potential synergy** structure for each of six named buyers across up to twelve fit categories (geographic, product, distribution, manufacturing, customer, procurement, cross-sell, cost synergy, revenue synergy, financial capacity, transaction complexity, regulatory) — see [06_Buyer_Analysis/Project_Southeast_Asia_Buyer_Analysis.xlsx](06_Buyer_Analysis/Project_Southeast_Asia_Buyer_Analysis.xlsx). No arbitrary numerical buyer scores are used anywhere.

Buyer-specific synergy sizing (for the two best-evidenced buyers, Nippon Paint and Siam Cement Group) uses standard percentage-of-revenue M&A synergy heuristics, since no deal-specific or buyer-specific synergy figure is publicly disclosed for this transaction — labeled ILLUSTRATIVE ASSUMPTION throughout, with methodology and rationale disclosed rather than a bare number.

## 9. Known Limitations

- **No SEA-specific financial disclosure exists.** Every dollar figure beyond the EUR 300m revenue anchor and the four statutory tax rates is either calculated or illustrative.
- **No market-data terminal access.** Trading comps data came from secondary aggregators and showed real cross-source inconsistencies, individually flagged.
- **Recalculation coverage.** A LibreOffice headless recalculation pass was run on 2026-10-09 (the earlier "no LibreOffice" limitation no longer applies). Only `02_Financial_Model` and `05_Valuation` were saved with stored values; `03_Trading_Comps`, `04_Precedent_Transactions` and `06_Buyer_Analysis` were scanned via recalculated copies and still contain formulas without stored values until they are next opened in Excel or LibreOffice. `05_Valuation/DCF_Summary` links to the model by relative path, so keep the numbered-folder layout; Excel will ask to update links on open.
- **Malaysia's decorative manufacturing site location was not confirmed** against a primary source in this research pass.
- **The transaction perimeter is an analyst inference**, not a confirmed fact — whether Performance Coatings assets, shared services, or specific brands transfer with the decorative business is unknown.
- **Equity Value cannot be calculated** — no public asset-level debt/cash exists for the carve-out.
- **DCF, trading comps, and precedent transactions do not converge** on a valuation — treated as a genuine finding.

## 10. Key Assumptions

The full, individually-sourced assumptions book (43 rows) is at [09_Assumptions/Support_Assumptions.xlsx](09_Assumptions/Support_Assumptions.xlsx). Headline illustrative assumptions:

| Assumption | Value |
|---|---|
| Country revenue split (Indonesia/Thailand/Vietnam/Malaysia) | 40% / 25% / 20% / 15% |
| Forecast revenue growth | ~5.0% CAGR (ASEAN market-anchored) |
| EBITDA margin (FY2026E → FY2030E) | 16.5% → 18.0% |
| Gross margin | 45% flat |
| D&A / Capex (% of revenue) | 2.5% / 3.0% (3.5% in separation years) |
| Working capital (DSO/DIO/DPO) | 45 / 60 / 45 days |
| Blended effective tax rate | 21.4% (calculated from disclosed statutory rates) |
| WACC / Terminal growth | 8.88% / 3.0% |

## 11. Folder Structure

```
PROJECT-SOUTHEAST-ASIA/
├── 01_Source_Data/              Transaction research, SEA asset perimeter
├── 02_Financial_Model/          Carve-out P&L, working capital, capex/D&A, DCF
├── 03_Trading_Comps/            Trading comparables and implied valuation
├── 04_Precedent_Transactions/   Precedent M&A transactions and implied valuation
├── 05_Valuation/                Triangulation, football field, equity bridge
├── 06_Buyer_Analysis/           Buyer fit matrix, synergy analysis
├── 07_Pitch_Deck/               17-slide sell-side pitch deck (.pptx and .pdf)
├── 08_Information_Memorandum/   information memorandum (.pdf): 22 numbered sections, 24 pages
├── 09_Assumptions/              Consolidated assumptions book
├── 10_Supporting_Research/      Source database (36 sources)
├── README.md                    This file
└── FINAL_REVIEW.md              Senior-banker-style quality review (Phase 15)
```

## 12. Reproduction Instructions

All workbooks were built programmatically with `openpyxl` (Python) and are fully formula-driven — reopening any `.xlsx` in Excel or LibreOffice and recalculating will reproduce every output shown in this project from the blue-highlighted input cells. The pitch deck was built with `pptxgenjs` (Node.js) and structurally validated; the Information Memorandum was built directly as a PDF with `reportlab` (Python). Build scripts are not included in the delivered folder structure (per the spec) but follow a consistent pattern: read the assumptions, compute the chain, write formulas (never hardcoded results) with a documented rationale for every blue input cell.

To update any output: change the relevant blue input cell in the source workbook (starting with `02_Financial_Model/Assumptions` for anything valuation-related), recalculate, and propagate any changed headline figures manually into the downstream workbooks (05_Valuation, 06_Buyer_Analysis, 07_Pitch_Deck, 08_Information_Memorandum, 09_Assumptions) — with one exception: the DCF figures on `05_Valuation/DCF_Summary` are live links to `02_Financial_Model/DCF_Valuation`. Everything else is typed across files.

---

*This project is an independent student analysis/reconstruction based on publicly available information. It is not affiliated with, commissioned by, or representative of Goldman Sachs or AkzoNobel.*
