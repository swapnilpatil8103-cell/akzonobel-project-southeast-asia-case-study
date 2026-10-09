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

> **Table updated 2026-10-09** to the current headline figures (WACC 8.88%, DCF base EUR 613m, recommended range EUR 500/625/775m). The original Phase 13 table showed 9.66% / EUR 539m / 450-575-700; those figures were superseded by the 2026-09-18 live-data refresh (Addendum D) and the 2026-10-09 corrections (Addendum E). The ✓ marks above were re-verified on 2026-10-09 by a scripted check of 26 values.

**Method:** The chain ION Article → Transaction Context → Asset Perimeter → Financial Model → Valuation → Buyer Analysis → Pitch Deck → Information Memorandum should tell the same financial story. Headline figures were extracted programmatically from each workbook, the pitch deck (`.pptx`, via markitdown text extraction), and the Information Memorandum (`.pdf`, via pypdf text extraction), and compared.

| Figure | 02_Financial_Model | 03/04_Implied_Valuation | 05_Valuation | 06_Buyer_Analysis | 07_Pitch_Deck | 08_IM | 09_Assumptions |
|---|---|---|---|---|---|---|---|
| SEA FY2025 revenue anchor | EUR 300m | — | — | — | — | EUR 300.0m ✓ | EUR 300m ✓ |
| SEA FY2026E revenue | EUR 315m | EUR 315m ✓ | — | EUR 315m ✓ | "EUR315" ✓ | EUR 315.0m ✓ | — |
| SEA FY2026E EBITDA | EUR 52m | — | — | EUR 52m ✓ | — | — | — |
| WACC | 8.88% | — | (feeds DCF) | — | 8.88% ✓ | 8.88% ✓ | 8.88% ✓ |
| Terminal growth | 3.0% | — | (feeds DCF) | — | — | — | 3.0% ✓ |
| DCF base Enterprise Value | EUR 613m (613.33) | — | EUR 613m ✓ (linked) | — | "613" ✓ | EUR 613m ✓ | — |
| Recommended EV range (low/mid/high) | — | — | 500/625/775 | — | EUR500-775mm ✓ | 500/625/775 ✓ | 500/625/775 ✓ |

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

---

## Addendum E. LibreOffice Recalculation Pass and Corrections (2026-10-09)

**Pass performed.** LibreOffice (headless) was used for the first time to recalculate the workbooks and store computed values. `02_Financial_Model` and `05_Valuation` were recalculated in place (348 and 74 formulas, all with stored values). `03_Trading_Comps`, `04_Precedent_Transactions` and `06_Buyer_Analysis` were recalculated as throwaway copies for scanning only, so those three files themselves still hold formulas without stored values. Every workbook was then scanned for `#REF!`, `#DIV/0!`, `#NAME?`, `#VALUE!`, `#N/A`, `#NULL!`, `#NUM!` and `Err:` values: **none found**.

**Defect found and fixed: terminal value used the wrong year.** `02_Financial_Model/DCF_Valuation!F10` is labelled "Terminal Value (Gordon Growth, on FY2030E FCF)" but its formula referenced `E5` (FY2029E FCF, 39.59) instead of `F5` (FY2030E FCF, 42.11). The sensitivity grid beneath it used the correct FY2030E cash flow, so the model contradicted itself. Recalculated, the base-case Enterprise Value (`B15`) was **584.44** against a grid centre of **613.33**; the figure quoted across the project (EUR 613m) had been computed outside the workbook and did not match the workbook's own `B15`. After the fix `B15` = **613.33**, equal to the grid centre to machine precision, and the terminal value's share of EV (`B16`) is 78.7%. No headline figure changed. The earlier Phase 13 audit and the Python replication of the model missed this because the replication used the correct FY2030E cash flow, so it reproduced the grid rather than the cell.

**Valuation workbook linked to the model.** `05_Valuation/DCF_Summary` previously held typed copies of the base-case EV (613), TV share (0.787) and the 25-cell sensitivity grid. They are now live cross-workbook links to `02_Financial_Model/DCF_Valuation` (`B15`, `B16`, `A31:F36`); the grid and the base case can no longer drift from the model. Links use a relative path, so the numbered-folder layout must be kept.

**Precedent range relabelled.** `Precedent_Summary` labelled the three implied EVs Low (PPG/AIP, 87), Mid (SHW/Suvinil, 690) and High (Nippon/AkzoNobel, 578), so the "Mid" exceeded the "High". They are now shown per deal, with a computed Low / Mid / High of **87 / 578 / 690** (min / median / max), the deal at each point looked up by formula, and `Triangulation!B8:D8` pointing at the sorted row. The football-field helper columns (`H16:J20`) still compute (precedent bar 87 to 690, width 603), and the chart survived the LibreOffice round trip.

**Still inconsistent (not changed in this pass).** The old Low / Mid / High ordering for precedents remains in: the Information Memorandum's valuation table (Section 19, "87 / 690 / 578"), `04_Precedent_Transactions/Implied_Valuation` and the matching rows in `09_Assumptions/Support_Assumptions.xlsx`. The precedents workbook also computes 88.2 / 689.9 / 576.5 because it stores its multiples rounded to two decimals, versus the 87 / 690 / 578 typed in `05_Valuation`.

**Cross-document check re-run (26 values).** WACC 8.88%, DCF base EV 613.33 and the recommended range 500 / 625 / 775 are identical in the model, `05_Valuation`, the pitch deck (`.pptx` and `.pdf`), the Information Memorandum and the assumptions book. No stale 9.66%, EUR 539m or 450-700 figures remain in the deck or the IM.

---

## Addendum F. Post-Announcement Update (2026-10-09)

AkzoNobel announced binding agreements on 5 October 2026 to sell its South East Asia decorative paints businesses to Nippon Paint (EV about USD 1.35bn / EUR 1.20bn, 21x FY2025 EBITDA, seven countries). See `Post_Announcement_Addendum.md` in this folder.

**What was checked:** the announced EV, multiple, net proceeds, perimeter and closing timing were identical across AkzoNobel's media release, its SEC Form 6-K and trade-press coverage (SRC-037 to SRC-040). Reported FY2025 revenue (about USD 291m) and EBITDA (about USD 65m) come from one trade article (SRC-039) only; the EBITDA figure reconciles arithmetically with the stated 21x on USD 1.35bn, the revenue figure has no independent support. Every figure in the addendum was recomputed from these inputs at the release-implied USD 1.125 per EUR.

**What was changed:** documentation and the pitch deck only (README, FINAL_REVIEW, Transaction_Research, Support_Sources, this file, the addendum, deck wording and an update slide).

**What was not changed:** no workbook formula or input was edited. The headline figures in Section B and Addendum E (WACC 8.88%, DCF base EUR 613m, recommended range EUR 500/625/775m) are therefore still consistent across the model, valuation workbook, deck and memorandum, and are now known to sit well below the announced price. The Information Memorandum PDF was not rebuilt and still describes a live process and a four-country perimeter.

---

## Addendum G. Review of Commit dc4710b: Cases-Sheet Overlap, Source Attribution and Wording (2026-10-09)

**Defect: overlapping blocks on the v2 model's `Cases` sheet.** The three case blocks were laid out 26 rows apart but each needs 28 rows (the reverse-DCF lines sit at the bottom). The Base block's "terminal EBITDA margin needed" and "terminal growth needed" rows therefore shared rows 40-41 with the Buyer block's header, and the Buyer block's last two rows shared rows 66-67 with the Downside header. Labels were overwritten, and the Base and Buyer "terminal growth needed" cells held header text ("FY2026E"). The Downside block (last) was intact. **Effect on `Deal_Check`:** the pasted reverse-DCF cells B44 and C44 contained the text "FY2026E" instead of the Base and Buyer growth needed, and the margin row was read from the wrong cells for those cases. No DCF value, range or weight was affected: the EV, Low and High rows, the summary table and the integrity check were all correct.

**Fix.** The blocks are now spaced 31 rows apart (rows 14-41, 45-72, 76-103), with identical structure and a gap between them; all formulas remain live. The valuation workbook was rebuilt from the corrected model, and a scripted check now confirms that 36 pasted values equal their model source cells and that no pasted cell contains text (0 mismatches, 0 text cells). Corrected reverse DCF to reach EUR 1,200m: terminal EBITDA margin Base 38.67%, Buyer 34.91%, Downside 42.99%; terminal growth Base 5.72%, Buyer 4.99%, Downside 6.36%. An independent Python replication matches all three EVs, the Low/High values and the reverse DCF.

**Source attribution corrected (SRC-041 to SRC-043).** Re-reading the articles: Investing.com and Yahoo Finance UK attribute the FY25 revenue, EBITDA, ~22% margin and the ~16x multiple to Nippon Paint and do not mention a press release. Yahoo Finance Singapore gives the FY24 and FY25 figures without naming a source in the sentence; its only "press release" reference concerns Nippon Paint's funding plan, in an earlier paragraph. The earlier log entry and the v2 model text, which said the Singapore article attributed the figures to the Nippon Paint press release, were wrong and are corrected.

**Wording.** "Single-source" was replaced for FY2024 and FY2025 revenue and EBITDA by: reported by several outlets, attributed to Nippon Paint; the primary Nippon Paint release was not read; not in AkzoNobel's release (README, FINAL_REVIEW, Addendum, Transaction_Research, v2 README and workbooks, pitch deck slides 2, 18, 19; PDF re-exported). The 2026 projection (revenue above ~USD 330m, ~26% margin) stays single-source: it was not found in five other outlets checked (Investing.com, Yahoo Finance Singapore and UK, SRC-047, SRC-048).

**No result changed.** DCF EV Base 712.65, Buyer 853.74, Downside 586.20; Low/High as before; WACC 8.822%; weighted triangulation 551.3 / 785.5 / 1,096.9, rounded 550 / 775 / 1,100.

---

## Addendum H. Buyer Analysis v2, Transaction Review Deck, Memo and IM Status Notice (2026-10-09)

**Built (all in `11_Post_Announcement_v2/`; nothing in folders 01-10 overwritten except the listed documents).** (1) `Project_Southeast_Asia_v2_Buyer_Analysis.xlsx`: the September workbook with columns and sheets unchanged (0 September cells differ), plus an Outcome layer (Buyer_Fit_Matrix columns F-G, Outcome_Summary) and Synergy_v2 (Nippon Paint synergies on reported FY2025 revenue, and synergies needed to justify the price). (2) `Project_Southeast_Asia_v2_Transaction_Review.pptx` and PDF: 14 slides, native charts, same visual style as the September deck. (3) `Project_Southeast_Asia_v2_Transaction_Review_Memo.pdf`: 4 pages. (4) `Project_Southeast_Asia_v2_Information_Memorandum_with_Status_Notice.pdf`: the September IM (24 pages) with a one-page status notice prepended; the original is untouched. SRC-047 (Pulse 2.0) and SRC-048 (Briefs Finance) were added to the source log, now 48 sources.

**Result.** Synergies needed to close the gap between the announced EV and the standalone DCF: about EUR 38.6m a year run-rate cost saving on the Base DCF (14.9% of FY2025 revenue) and EUR 27.5m on the Buyer-case DCF (10.6%), against a September heuristic of EUR 5.2m to 10.3m. ILLUSTRATIVE; it cannot separate synergies from a lower discount rate or a better business.

**Verification.** Buyer workbook recalculated in LibreOffice headless: 49 formulas, all with stored values, no error values. The synergy-needed calculation was replicated independently in plain Python (38.644 and 27.456, matching the sheet). Every deck slide, the memo pages and the notice page were rendered to images and inspected; chart titles that overlapped captions and a text-only slide were corrected before commit. Headline figures were cross-checked across the buyer workbook, deck, memo and READMEs (see the commit report).

**Assumptions made.** (a) 'High single digits as a percentage of sales' (SRC-048, attribution not stated) read as 7% to 9%. (b) Integration cost 1.0x the run-rate saving, tax-effected, and full run-rate from the first year (flatters the result). (c) Revenue synergies were converted to profit at the reported FY2025 margin in a separate line; the September sheet had added sales uplift to cost savings, and that September sheet was left unchanged. (d) Buyer entities on deck slide 12 come from one article (SRC-042). (e) The September deck was not modified; the transaction review deck replaces its post-announcement role.

**Follow-up fixes (2026-10-09).** (1) SRC-048 date re-checked: the page states 'Published Oct 4, 2026' (no updated date), so the date stands and the log row now notes it is dated the day before AkzoNobel's release; no other file cites it. (2) Deck slide 6 now labels the 786 bar 'Weighted blend (unrounded)' and slide 13 labels 775 'v2 weighted mid-point (rounded to 25)'; the memo states both figures together. (3) Status-notice footer shortened to fit one line; the 24 September pages are unchanged (text identical). (4) Slide 12 retitled 'Reported structure: ...' and its note states the single source (Yahoo Finance Singapore / MT Newswires). The buyer workbook was recalculated again: 0 formula errors, 0 value changes. No valuation number changed.
