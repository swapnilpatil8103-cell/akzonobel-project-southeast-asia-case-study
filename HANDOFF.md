# HANDOFF: reader guide

## 1. What this project is

An independent student reconstruction of AkzoNobel's sale of its Southeast Asia decorative paints business. It was built in September 2026, before any deal was announced, and updated on 9 October 2026 after AkzoNobel announced the sale to Nippon Paint. This project is an independent student analysis/reconstruction based on publicly available information. It is not affiliated with, commissioned by, or representative of Goldman Sachs, AkzoNobel or Nippon Paint.

## 2. Two layers of work

| Layer | Folders | Status |
|---|---|---|
| September record | `01`–`10` | Preserved as written, not rewritten with hindsight. The only changes are the fixes listed in section 5 and the post-announcement notes added to the documents. |
| v2 post-announcement | `11_Post_Announcement_v2/` | Financial model, valuation, buyer analysis, 14-slide Transaction Review deck, review memo, and a copy of the Information Memorandum with a status notice prepended. |

## 3. Start here

1. `11_Post_Announcement_v2/Project_Southeast_Asia_v2_Transaction_Review_Memo.pdf` (4 pages).
2. `11_Post_Announcement_v2/Project_Southeast_Asia_v2_Transaction_Review.pptx` or `.pdf` (14 slides).
3. `10_Supporting_Research/Post_Announcement_Addendum.md` (what the announcement showed against the September case).
4. `11_Post_Announcement_v2/Project_Southeast_Asia_v2_Financial_Model.xlsx` and `..._Valuation.xlsx` (method and limitations are in that folder's `README.md`).
5. `10_Supporting_Research/Quality_Control_Review.md` (what was checked, what was found, Addenda E to H).

## 4. Headline results

The announced price was used as a check, not a target. No assumption was tuned to reach it.

| Item | Figure | Label |
|---|---|---|
| Announced enterprise value | EUR 1.20bn (USD 1.35bn) | PUBLIC FACT |
| Announced multiple | 21x FY2025 EBITDA | PUBLIC FACT |
| Net cash proceeds | EUR 0.9bn (USD 1.0bn) | PUBLIC FACT |
| FY2025 revenue and EBITDA | About USD 291m and USD 65m (EUR 259m and EUR 58m), margin about 22% | REPORTED: several outlets, attributed to Nippon Paint; primary release not read; not in AkzoNobel's release |
| September recommended EV range | EUR 500–775m (DCF base EUR 613m); the announced price is 55% above its top | ANALYST CALCULATION |
| v2 weighted range (low / mid / high) | EUR 550 / 775 / 1,100m, rounded to 25; the unrounded mid-point is EUR 785m | ANALYST CALCULATION |
| v2 DCF enterprise value (Base / Buyer / Downside) | EUR 713 / 854 / 586m | ANALYST CALCULATION on ILLUSTRATIVE drivers |
| Reverse DCF to reach EUR 1,200m (Base / Buyer / Downside) | Terminal EBITDA margin of 38.7% / 34.9% / 43.0%, or terminal growth of 5.7% / 5.0% / 6.4% (reported FY2025 margin 22.3%; model growth 3.0%) | ANALYST CALCULATION |
| Synergies needed to justify the price | About EUR 27m to 39m a year of run-rate cost saving; it cannot separate synergies from a lower discount rate or a better business than reported | ILLUSTRATIVE |

## 5. What went wrong and was fixed

- **DCF terminal-value bug.** `DCF_Valuation!F10` used FY2029E instead of FY2030E cash flow, so the cell showed 584.44 against a grid centre of 613.33. Fixed in commit `3777ac7`; no headline figure changed.
- **Precedents mislabel.** The September precedent range was labelled Low / Mid / High as 87 / 690 / 578. It is now min / median / max, 87 / 578 / 690. Some September documents still carry the old ordering (see Quality_Control_Review.md, Addendum E).
- **v2 Cases-sheet overlap.** Three case blocks overlapped, overwriting labels and leaving header text in two reverse-DCF cells that the Valuation workbook had pasted. Re-laid out, with a scripted check on pasted values; no result changed (Addendum G).
- **Source-attribution corrections.** An earlier log entry said Yahoo Finance Singapore attributed the FY2024/FY2025 figures to a Nippon Paint press release; it does not. Wording on the financials was changed from "single-source" to "several outlets" (Addendum G).

## 6. Known limitations

- Comparables are dated 18 September 2026 (Yahoo Finance) and were not refreshed. Beta 0.821 is unchanged.
- The country split, country risk premiums, margin fade, downside step-down and integration-cost multiple are illustrative and unsourced.
- Nippon Paint's 2026 projection (revenue above about USD 330m, margin about 26%) and the Malaysian plant and brand details are single-source (PCI Magazine).
- The primary Nippon Paint release was not read. Several sources were read through an AI page-fetch summary, not verbatim.
- The bidder list is not public. SCG is "not mentioned" in the coverage checked, which does not show whether it bid.
- The September Information Memorandum body and the September deck (`07_Pitch_Deck/`: valuation, synergy and marketing slides) were not refreshed; the v2 deck and memo replace their post-announcement role.
- No equity value can be derived: the perimeter's net debt and minority interests are not disclosed.
- One deal is one data point. Nothing here shows the method predicts outcomes.

## 7. Label key

| Label | Meaning |
|---|---|
| PUBLIC FACT | Stated in a primary source such as AkzoNobel's release or filing |
| REPORTED | Reported by media or other secondary sources; not confirmed against a primary release |
| ANALYST CALCULATION | Derived by formula from disclosed or reported inputs |
| ILLUSTRATIVE ASSUMPTION | An analyst input with no source |
| UNAVAILABLE | Not public; left blank, never invented |

Workbook colour code: **blue** = input, **black** = formula, **green** = link to another sheet in the same workbook, **red** = value pasted from another workbook (source cell named).
