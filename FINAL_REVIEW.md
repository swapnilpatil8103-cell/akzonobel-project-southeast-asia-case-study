# Project Southeast Asia — Final Review

> Independent student analysis/reconstruction based on publicly available information. Not affiliated with, commissioned by, or representative of Goldman Sachs or AkzoNobel.

This is the closing quality assessment of the project, consolidating the Phase 13 quality-control review and Phase 14 senior-banker review into the twelve items requested. It is a qualitative assessment, not a numerical score.

---

## 1. What Is Factually Established

- Seller (AkzoNobel), reported adviser (Goldman Sachs), reported business line (SEA decorative paints across Indonesia, Thailand, Malaysia, Vietnam), reported revenue (EUR300m), reported NBO timing (mid-Sep-2026), one named possible bidder (Siam Cement Group), and the reported optionality to sell whole-region or country-by-country — all from the ION Analytics article (SRC-001).
- Confirmed legal entities and at least one manufacturing site in Indonesia, Thailand and Vietnam (Malaysia's site unconfirmed), each independently corroborated across 2-3 secondary sources.
- AkzoNobel Group-level FY2024/FY2025 Decorative Paints segment revenue and EBITDA margin (disclosed in AkzoNobel's own results releases).
- The four countries' statutory corporate income tax rates.
- Four of five precedent transactions' disclosed deal values (JSW/AkzoNobel India, Nippon Paint's rejected AkzoNobel bid, Sherwin-Williams/Suvinil, PPG/AIP).

## 2. What Is Analyst-Calculated

- The blended 21.4% effective tax rate (statutory rates weighted by an illustrative country split).
- WACC (8.88%), built up from a live peer-median beta (0.821, updated 2026-09-18) plus otherwise disclosed-methodology but individually illustrative inputs.
- Implied EV/Revenue and EV/EBITDA multiples for the Nippon Paint/AkzoNobel offer and the Sherwin-Williams/Suvinil and PPG/AIP precedents, each derived from two independently disclosed figures.
- Trading comps percentile statistics (median/P25/P75), computed from the 3-4 usable peer data points that survived the "never manufacture a multiple" screen.

## 3. What Is Illustrative

The large majority of the financial model: country revenue split, all forecast growth rates, the FY2026E-FY2030E margin ramp, TSA/stranded cost assumptions, capex/D&A percentages, working capital days, most WACC build-up inputs (beta itself is now real peer-median data, but Rf/ERP/CRP/cost of debt/leverage remain illustrative), the recommended EUR500-775m valuation range, and both buyers' synergy sizing. All are labeled ILLUSTRATIVE ASSUMPTION at the point of use, with a stated rationale and, where relevant, a sensitivity note — never presented as disclosed fact.

## 4. Biggest Model Limitations

- **No SEA-specific financial statements exist publicly.** Every line beyond the EUR300m revenue anchor and the four tax rates is either calculated or assumed — this is the single largest limitation and is disclosed on the first page of 02_Financial_Model's own README, not buried.
- **No live formula recalculation was possible** (no LibreOffice on the build machine). Substituted with a full manual formula audit and an independent Python replication of the calculation chain — a reasonable but not equivalent substitute.
- **Malaysia's decorative site is unconfirmed**, and the transaction perimeter itself (decorative-only) is an analyst inference from the source article's wording, not a confirmed scope.
- **Equity Value cannot be calculated** — no public asset-level debt/cash for the carve-out.

## 5. Biggest Valuation Sensitivities

- DCF Enterprise Value swings from EUR468m to EUR908m across a plausible ±1.0% WACC and ±1.0% terminal-growth band — a ~94% range purely from discount-rate/growth uncertainty on an already-uncertain cash flow forecast.
- The trading comps range is still influenced by Asian Paints' 33.6x EV/EBITDA multiple (now within a complete 6-company dataset rather than a partial one); removing that single company would materially compress the comps-implied range downward, closer to the DCF.
- The country revenue split (40/25/20/15%) is a pure assumption with no public support; a materially different split would not change total Enterprise Value (which is anchored on the whole-perimeter EUR300m) but would change any country-specific buyer or structuring analysis.

## 6. Key Buyer Considerations

- **Nippon Paint** has the strongest evidenced fit and the highest evidenced regulatory/antitrust risk simultaneously (Malaysia #2 position, ~50% Thailand JV share) — a genuine tension, not resolved by this project, that any real process would need to work through with competition counsel.
- **Siam Cement Group** is the only buyer with confirmed process involvement, but its paints business sits inside a much larger, non-paints-specific conglomerate, changing both its likely valuation approach and its synergy thesis relative to the pure-play strategics.
- **Asian Paints' prior exit from Indonesia** (a disclosed divestiture) is a real contrary data point against an Asian Paints/Berger re-entry thesis that this project surfaced rather than omitted.
- **PPG's 2024 architectural coatings divestiture** similarly argues against PPG as a highly motivated buyer for this asset class, despite being named in market commentary.

## 7. Key Transaction Risks

Financial data scarcity; regulatory/antitrust exposure concentrated in a Nippon Paint scenario; perimeter uncertainty (which entities/brands/shared services actually transfer); multi-country execution complexity under a split-sale structure; carve-out execution risk (TSA/stranded costs, standalone systems build-out); and the fundamental non-convergence of DCF, trading comps and precedent valuations, which widens the defensible pricing range beyond what a single clean number would suggest.

## 8. Source-Quality Assessment

Of the 36 logged sources (33 from the original research phases plus 3 added 2026-09-18 documenting the live-data API pulls), roughly 5 are Tier 1 (AkzoNobel's own disclosures, government tax data, LEI registry), roughly 9 are Tier 2 (ION Analytics, Coatings World, deal-specific trade press), and roughly 22 are Tier 3 (secondary financial aggregators, live market-data feeds, and general trade press) — see 10_Supporting_Research/Support_Sources.xlsx. This project had no market-data terminal access, and several Tier 3 sources showed real cross-source inconsistency (Sherwin-Williams' and AkzoNobel's own market caps varied materially by source/date; Berger Paints' reported EV/EBITDA was internally inconsistent with its own disclosed net income). Every such inconsistency was flagged individually at the point of use rather than silently averaged or picked without comment. The primary source itself (ION Analytics) was accessed via an AI-summarized page fetch of a paywalled article, not a verbatim read — disclosed explicitly in 01_Source_Data/Transaction_Research.md from Phase 1 onward.

## 9. Model-Integrity Assessment

433 formulas scanned across 8 workbooks in the Phase 13 QC pass; zero genuine defects found (7 initial flags were false positives from the scan's own heuristic, traced and explained). Every workbook follows consistent color-coding (blue input / black formula / green cross-sheet link), and headline figures were confirmed consistent across every document that cites them — the financial model, valuation workbook, buyer analysis, pitch deck and information memorandum all report the same EUR300m anchor, EUR315m FY2026E revenue, 8.88% WACC, and EUR500-775m recommended range (updated 2026-09-18 following the live beta/trading-comps data refresh, and re-verified consistent across every document at that time). The unresolved gap is that no live Excel/LibreOffice recalculation pass was possible on this machine; the manual audit and independent Python replication are a reasonable substitute but a user with Excel access should still do one open-and-recalculate pass before relying on these files for anything beyond this case study.

## 10. Presentation-Quality Assessment

The pitch deck (17 slides, structurally validated, content-QA'd) and Information Memorandum (24 pages, native PDF, text-verified) both follow conclusion-oriented headlines, disclosed sourcing on every slide/section, and — where data doesn't exist — say so explicitly (e.g., the IM's Customers, Distribution and Management sections) rather than padding with invented operating detail. The one open item is that neither document received a visual/rendered QA pass (no LibreOffice for slide-image rendering; the IM's reportlab-based table layout was verified only via column-width math and text extraction, not a rendered image) — disclosed in both phases' delivery messages rather than claimed as complete.

## 11. Questions an IB Associate / VP Would Challenge

- "Your recommended range is an opinion on top of three non-converging methodologies — does the client understand that, or does the precision of 'EUR500-775m' oversell your confidence?"
- "Your trading comps median is built from 3-4 companies — is 'median' the right word, or does it overstate the robustness of that sample?"
- "You've assumed AkzoNobel's Group Decorative Paints margin applies to SEA specifically — what's your fallback if SEA actually runs materially below or above that, given it's a growth market with different competitive dynamics than AkzoNobel's larger EU/NA decorative business?"
- "You've flagged Nippon Paint as both your best-fit and highest-regulatory-risk buyer — have you actually sized what a country-by-country carve-out (excluding Nippon Paint from Malaysia/Thailand specifically) does to the achievable buyer universe and price? This project raises the question but does not answer it quantitatively."

## 12. Specific Improvements Required

Before this project could inform any real decision (which it is not intended to, but as a matter of rigor):

- Obtain and directly parse AkzoNobel's FY2025 Annual Report line-by-line (identified as SRC-014 but never fully parsed) to check whether any SEA or "South Asia Pacific" segment note narrows the revenue/margin assumptions used here.
- Confirm Malaysia's decorative manufacturing site against a primary source.
- Re-run every workbook through a live Excel/LibreOffice recalculation and a rendered visual QA of the pitch deck and IM, on a machine where those tools are available.
- If pursued further, size the country-by-country structuring question raised in Section 11 quantitatively rather than qualitatively — specifically, what the achievable buyer universe and price look like if Nippon Paint is excluded from Malaysia/Thailand on regulatory grounds.
- Seek a second, live pull of the trading comps data from a proper market-data terminal to resolve the cross-source inconsistencies flagged throughout 03_Trading_Comps.
