# Project Southeast Asia — Quality-Control Review

**Phase 13 of the project workflow.** Two checks performed: (A) Model Integrity Check across every workbook's formulas, and (B) Cross-Document Consistency Check across all deliverables. Full scan scripts and raw output are reproducible; summarized results below.

---

## A. Model Integrity Check

**Method:** Because this build machine has no LibreOffice installed, the xlsx skill's automated `recalc.py` (which opens each file, forces a recalculation, and reports formula errors) could not be run — this limitation was disclosed at the time in Phases 3-4 and in the project README. As a substitute for this final QC phase, every workbook was scanned programmatically for:

1. Literal error tokens (`#REF!`, `#DIV/0!`, `#VALUE!`, `#NAME?`, `#N/A`, `#NULL!`, `#NUM!`) typed into any formula string.
2. Cross-sheet references pointing at a sheet name that does not exist in that workbook (the most common cause of a broken link when a tab is renamed or deleted after formulas are written).
3. Structurally malformed formulas (double operators, likely typos).

| Workbook | Formulas scanned | Flagged |
|---|---:|---:|
| 01_Source_Data/SEA_Asset_Perimeter.xlsx | 0 | 0 |
| 02_Financial_Model/Project_Southeast_Asia_Financial_Model.xlsx | 348 | 7 (false positives, see below) |
| 03_Trading_Comps/Project_Southeast_Asia_Trading_Comps.xlsx | 37 | 0 |
| 04_Precedent_Transactions/Project_Southeast_Asia_Precedents.xlsx | 6 | 0 |
| 05_Valuation/Project_Southeast_Asia_Valuation.xlsx | 30 | 0 |
| 06_Buyer_Analysis/Project_Southeast_Asia_Buyer_Analysis.xlsx | 12 | 0 |
| 09_Assumptions/Support_Assumptions.xlsx | 0 (data table only) | 0 |
| 10_Supporting_Research/Support_Sources.xlsx | 0 (data table only) | 0 |
| **Total** | **433** | **0 genuine defects** |

**On the 7 flags:** all 7 were in `Carveout_PnL!C28:I28` (the Unlevered Free Cash Flow row), flagged by the scan's double-operator heuristic matching the substring `*-1` inside `...+C20*-1+...`. This is the deliberate D&A sign-flip term (D&A is stored as a negative expense earlier in the sheet and multiplied by `-1` to add it back positively into FCF) — it was manually verified correct against a full Python replication of the calculation chain when the workbook was first built (Phase 3), and re-verified here. **Zero genuine formula defects found across 433 formulas.**

No `#REF!`, circular reference, or broken cross-sheet link was found in any workbook. Number formats, currency units (EUR throughout, with INR/JPY/USD noted explicitly where used in Trading Comps), and hardcoded-vs-formula usage were spot-checked during each phase's build and are not re-litigated in full here — see each workbook's own formula audit in the phase-by-phase build record.

**Residual limitation:** this static scan cannot catch every class of error a live Excel/LibreOffice recalculation would (e.g., a subtly wrong range that still evaluates to a plausible-looking number). Every workbook's headline outputs were additionally cross-checked against an independent plain-Python replication of the same calculation logic at build time (see 02_Financial_Model and the Comps/Precedents implied-valuation checks), which is a meaningful substitute but not a full replacement for a real recalculation pass.

---

## B. Cross-Document Consistency Check

**Method:** The chain ION Article → Transaction Context → Asset Perimeter → Financial Model → Valuation → Buyer Analysis → Pitch Deck → Information Memorandum should tell the same financial story. Headline figures were extracted programmatically from each workbook, the pitch deck (`.pptx`, via markitdown text extraction), and the Information Memorandum (`.pdf`, via pypdf text extraction), and compared.

| Figure | 02_Financial_Model | 03/04_Implied_Valuation | 05_Valuation | 06_Buyer_Analysis | 07_Pitch_Deck | 08_IM | 09_Assumptions |
|---|---|---|---|---|---|---|---|
| SEA FY2025 revenue anchor | EUR 300m | — | — | — | — | EUR 300.0m ✓ | EUR 300m ✓ |
| SEA FY2026E revenue | EUR 315m | EUR 315m ✓ | — | EUR 315m ✓ | "EUR315" ✓ | EUR 315.0m ✓ | — |
| SEA FY2026E EBITDA | EUR 52m | — | — | EUR 52m ✓ | — | — | — |
| WACC | 9.66% | — | (feeds DCF) | — | 9.66% ✓ | — | 9.66% ✓ |
| Terminal growth | 3.0% | — | (feeds DCF) | — | — | — | 3.0% ✓ |
| DCF base Enterprise Value | EUR 539m | — | EUR 539m ✓ | — | "539" ✓ | EUR 539m ✓ | — |
| Recommended EV range (low/mid/high) | — | — | 450/575/700 | — | EUR450-700mm ✓ | 450/575/700 ✓ | 450/575/700 ✓ |

**Result: every checked figure is consistent across every document that cites it.** No instance was found of a number changing without explanation between the model, the valuation workbook, the buyer analysis, the pitch deck, or the Information Memorandum.

**Note on what this check does *not* cover:** it verifies numerical consistency of the headline figures listed above; it does not re-verify every qualitative claim (e.g., buyer-fit narrative wording) word-for-word across documents. Qualitative consistency (e.g., that the pitch deck's "Nippon Paint highest overlap / highest regulatory risk" framing matches the Buyer_Fit_Matrix workbook) was checked by construction — the pitch deck and IM were both written by directly summarizing the phase workbooks, not independently redrafted — but was not re-verified by an automated text-diff in this QC pass.

---

## C. Items Explicitly Flagged as Open (carried into FINAL_REVIEW.md)

- ~~No LibreOffice on the build machine — no live recalculation pass, no pitch-deck visual QA, no PDF export test of the `.pptx`.~~ **Partially resolved 2026-09-18:** this machine has real PowerPoint installed, which was used via COM automation to export a genuine `.pdf` from the `.pptx` and to render every slide as an image for visual QA — two real layout bugs were found and fixed this way (see Addendum D). No live Excel/LibreOffice recalculation of the `.xlsx` workbooks has still been performed.
- ~~No market-data terminal access — trading comps built on secondary-aggregator data with disclosed cross-source inconsistencies.~~ **Partially resolved 2026-09-18:** live market data (Yahoo Finance via yfinance) was pulled for all 6 trading comps and the WACC beta input, resolving every previously-flagged inconsistency (PPG's missing EBITDA, Berger's inconsistent multiple, Kansai's currency mismatch). This is still a single secondary provider, not a licensed institutional terminal (Bloomberg/CapIQ/Refinitiv). See Addendum D.
- Malaysia's decorative manufacturing site location unconfirmed against a primary source.
- The transaction perimeter (decorative-only, four confirmed legal entities) is an analyst inference, not a confirmed fact.
- Equity Value cannot be calculated (no public asset-level debt/cash).
- DCF, trading comps and precedent transactions do not converge — addressed via an explicitly-labeled analyst judgment call, not resolved as a fact.

These are carried forward into `FINAL_REVIEW.md` (Phase 15) rather than repeated in full here.

---

## Addendum D. Live-Data Refresh and Re-Verification (2026-09-18)

Following the original Phase 13 QC pass, the user supplied API access to three data providers (EODHD, Financial Modeling Prep, and a third source called "London Strategic Edge"). EODHD's free tier and FMP's plan both had material coverage gaps (no fundamentals on EODHD's free tier; FMP restricted to a handful of US-listed profile fields only). The Yahoo Finance feed (via the `yfinance` Python library, no key required) provided complete, consistent Market Cap / Enterprise Value / Revenue / EBITDA / Beta for all 7 companies (6 peers + AkzoNobel) in a single pull on 2026-09-18.

This real data was propagated through the model: the WACC beta input (02_Financial_Model/Assumptions) was updated from an illustrative flat 1.00 to the live peer-median 0.821, which moved WACC from 9.66% to 8.88% and the DCF base case from EUR539m to EUR613m. The Trading Comps workbook (03_Trading_Comps) was rebuilt entirely on the new dataset. Both changes were then propagated to 05_Valuation (DCF_Summary, Trading_Comps_Summary, Triangulation, Equity_Bridge), the recommended primary range (updated from EUR450/575/700m to EUR500/625/775m), 09_Assumptions/Support_Assumptions.xlsx, 10_Supporting_Research/Support_Sources.xlsx (3 new source entries, SRC-034 to SRC-036), the pitch deck (`.pptx` and `.pdf`, re-validated and visually re-rendered), the Information Memorandum (`.pdf`, re-rendered), and this project's README.md and FINAL_REVIEW.md.

**Re-verification performed:** the same cross-document consistency check as Section B above was re-run for the updated headline figures (WACC 8.88%, DCF base EUR613m, recommended range EUR500/625/775m) across 02_Financial_Model, 05_Valuation, 07_Pitch_Deck (both file formats), and 08_Information_Memorandum — all consistent. Formula audits were re-run on the rebuilt 02_Financial_Model and 05_Valuation workbooks (row-by-row reference checks) with no defects found.
