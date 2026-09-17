# Project Southeast Asia — Mock Senior Banker Review

**Phase 14.** A simulated review of this project's own work product, structured as an MD/VP/Associate/Analyst challenge. For every major number, the chain of questions is: **SOURCE? → CALCULATION? → ASSUMPTION?** Where the chain cannot be closed, that is stated plainly rather than papered over.

---

### MD: "Why should someone buy this asset?"

**Answer:** A confirmed, multi-decade decorative-paints footprint across four ASEAN markets (legal entities and at least one manufacturing site confirmed in each of Indonesia, Thailand, Malaysia — entity only — and Vietnam), sitting inside a market growing at an implied ~5.0% CAGR (ASEAN paints & coatings, USD7.78bn 2026 → USD9.92bn 2031, per the ION Analytics article). The Dulux brand carries recognized regional equity. The Seller has reportedly signaled structuring flexibility (whole-region or country-by-country), which widens the pool of buyers who can credibly participate.

**Push-back an MD would actually give:** this is a thin case built on one disclosed number (EUR300m revenue) and a market-growth statistic from the same single article. There is no disclosed profitability, no disclosed customer base, no disclosed competitive share outside two of the four countries (Malaysia, Thailand — via Nippon Paint's position, not AkzoNobel's own). **This is an investment thesis that would need to be validated in real diligence, not one this project can independently confirm.**

---

### VP: "What is the valuation?"

**Answer:** Recommended primary range **EUR 500-775m Enterprise Value**, midpoint EUR625m (05_Valuation/Triangulation; updated 2026-09-18 following a live-data refresh of the WACC beta and trading comps — see Quality_Control_Review.md Addendum D).

**VP follow-up: "Walk me through how you got there, not just the number."**

- DCF: EUR468-908m (base EUR613m), built on a carve-out model whose only public anchor is FY2025 revenue, discounted at a WACC using a real live peer-median beta (0.821, updated 2026-09-18).
- Trading comps: EUR535-1,360m depending on basis — materially higher, now computed across a complete 6-company live dataset (Yahoo Finance) rather than a partial one, still with Asian Paints' 33.6x EV/EBITDA (India-market premium) pulling the range up hard.
- Precedents: EUR87-690m — spans a low-margin PE-sponsor floor deal (PPG/AIP) to a rejected mega-offer (Nippon/AkzoNobel global).
- The recommended range is **not** an average or a midpoint of these three — it is an explicit analyst judgment call, anchored on DCF and the two most structurally similar precedents, with the trading comps and outlier precedents (JSW's 25x, PPG's 0.275x) treated as context, not inputs to a formula.

**VP would flag:** "You're telling me your three methodologies don't agree, and then hand-picking which ones anchor your number. That's a legitimate approach in banking, but it means this range is an opinion, dressed as analysis, on top of a model that is itself mostly assumption. Say that plainly to the client, don't let the range's precision (EUR500m, not 'roughly half a billion') imply more confidence than the inputs support." **This critique is accepted and already stated in 05_Valuation's README and Triangulation tab.**

---

### Associate: "Show me the comps."

**Answer:** Six named comps (Sherwin-Williams, PPG, Nippon Paint, Kansai Paint, Asian Paints, Berger Paints) plus AkzoNobel shown for reference only. Full table in 03_Trading_Comps/Comps.

**Associate follow-up: "Why are two of your six comps missing an EV/EBITDA multiple?"**

- PPG: aggregator data couldn't be reconciled to a reliable EBITDA figure — left blank.
- Berger Paints: the aggregator-reported EV/EBITDA (36.8x) was internally inconsistent with Berger's own disclosed net income and typical decorative-paints margins — left blank rather than used, with the inconsistency flagged in the workbook.

**Associate would say (as originally posed, before the 2026-09-18 data refresh):** "Good — that's the right call, don't force a number that doesn't reconcile. But it also means your median EV/EBITDA (16.1x) is built on 4 companies, not 6, and your median EV/Revenue (3.76x) on 3. That's a thin sample for a 'median' — say 'the available data points' rather than implying statistical robustness a 3-4 name sample doesn't have." **This critique is now resolved rather than merely accepted: live market data (Yahoo Finance via yfinance, pulled 2026-09-18) gave a usable figure for all 6 peers on both bases, so the median EV/EBITDA (15.2x) and median EV/Revenue (2.83x) are now genuinely computed across the full comp set, not a partial one. See 03_Trading_Comps/README and Quality_Control_Review.md Addendum D.**

---

### Analyst: "Where did this number come from?"

Applied to the five numbers most load-bearing in this project:

| Number | SOURCE? | CALCULATION? | ASSUMPTION? |
|---|---|---|---|
| EUR300m SEA revenue (FY2025 anchor) | ION Analytics article (SRC-001) | — | — |
| 15.8% FY2025 EBITDA margin used for SEA | AkzoNobel's actual disclosed **Group Decorative Paints** margin (SRC-013, SRC-015) | — | Applied as a SEA proxy — this is the assumption layer: the number itself is real, but its *application to SEA* is not disclosed or confirmed |
| 8.88% WACC | Beta (0.821) is now real peer-median data, Yahoo Finance, 2026-09-18 | Built from Rf + Beta×ERP + CRP, blended with after-tax cost of debt | Rf 4.0%, ERP 5.5%, CRP 1.5%, cost of debt 5.5%, D/(D+E) 20% remain illustrative assumptions; beta is no longer one |
| EUR500-775m recommended range | — | — | Pure analyst judgment call, explicitly labeled as such, with written rationale in 05_Valuation |
| 21.4% blended tax rate | Four countries' statutory CIT rates (OECD/Trading Economics/PwC/Thaicore — SRC-016) are PUBLIC FACT | Revenue-weighted average of those four rates | The weighting itself uses the illustrative country revenue split (40/25/20/15%) |

**Analyst self-critique:** every one of these five numbers has at least one assumption layer between the public source and the number used (WACC's beta is now a genuine exception — it is live market data, not an assumption). None of the rest is fabricated — each traces cleanly to either a cited source or a disclosed formula — but a reader skimming a single figure (e.g., "WACC 8.88%") without opening the Assumptions tab could mistake precision for certainty. This is a real risk in how the pitch deck and IM present these figures with two decimal places; the underlying uncertainty is disclosed in the source workbooks but not repeated on every slide.

---

### Where the chain could NOT be closed (flagged, not resolved)

- **Malaysia's decorative manufacturing site** — no SOURCE found this research pass; stated as UNKNOWN in 01_Source_Data, not guessed.
- **SEA-specific EBITDA, working capital, capex/D&A** — no SOURCE exists; every downstream number is ASSUMPTION, clearly labeled.
- **Confirmed transaction perimeter** (decorative-only vs. broader) — no SOURCE confirms this; it is an ANALYST INFERENCE from the ION article's wording, disclosed as such everywhere it is used.
- **Equity Value** — cannot be computed; no SOURCE for asset-level debt/cash. Correctly left blank rather than assumed at "debt-free/cash-free" or any other convention.

---

## Verdict

This project's numbers survive the SOURCE/CALCULATION/ASSUMPTION test in the sense that matters most: **nothing is fabricated, and every gap is disclosed rather than filled.** The legitimate criticism a real senior banker would raise is not about hidden errors — the Phase 13 QC pass found none — but about **the appearance of precision** (specific-looking multiples and ranges) sitting on top of a foundation that is honestly, and repeatedly, disclosed as mostly illustrative. That tension is inherent to reconstructing a real, in-progress M&A process from a single trade-press article, and is the central limitation of this entire project, not a flaw in its execution.
