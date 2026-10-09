# 11_Post_Announcement_v2: valuation refresh after the 5 October 2026 announcement

This project is an independent student analysis/reconstruction based on publicly available information. It is not affiliated with, commissioned by, or representative of Goldman Sachs or AkzoNobel (or Nippon Paint).

The September workbooks in folders 01–10 are **unchanged** and remain the pre-announcement record. This folder rebuilds the model and valuation on the announced perimeter and checks the result against the announced price.

**The announced price is a check, not a target.** No assumption was tuned to reach EUR 1.2bn. The weights used to combine methods were fixed before the comparison.

## Files

| File | What it is |
|---|---|
| `Project_Southeast_Asia_v2_Financial_Model.xlsx` | Seven-country model: Assumptions (with a case selector), Case_Drivers, Revenue_Build, Working_Capital, Capex_DA, Carveout_PnL, DCF_Valuation (active case), Cases (all three cases side by side, with an integrity check), Sources |
| `Project_Southeast_Asia_v2_Valuation.xlsx` | Comps, Precedents, Implied_Valuation, Triangulation, Deal_Check |
| `Project_Southeast_Asia_v2_Buyer_Analysis.xlsx` | The September buyer workbook (columns and sheets unchanged) plus an Outcome layer (Buyer_Fit_Matrix columns F-G, Outcome_Summary) and Synergy_v2 (Nippon Paint synergies on reported FY2025 revenue; synergies needed to justify the price) |
| `Project_Southeast_Asia_v2_Transaction_Review.pptx` / `.pdf` | 14-slide transaction review deck (not a marketing deck) |
| `Project_Southeast_Asia_v2_Transaction_Review_Memo.pdf` | 4-page memo summarising the v2 findings |
| `Project_Southeast_Asia_v2_Information_Memorandum_with_Status_Notice.pdf` | Copy of the September Information Memorandum with a one-page status notice prepended; the original is untouched |

**Link choice.** The Valuation workbook holds *pasted values* (red font) copied from the model, each labelled with its source cell, not live external links. Script-built external links make Excel prompt to update and break if the folder moves. A scripted check confirmed every pasted value equals its model cell. After any model change, rebuild the valuation workbook.

## Method

- **Perimeter and FX.** Decorative Paints in seven countries (Vietnam, Indonesia, Malaysia, Thailand, Singapore, Papua New Guinea, Australia). One FX input, USD 1.125 per EUR (USD 1.35bn / EUR 1.20bn from the release).
- **History.** FY2024 and FY2025 are the reported figures (USD 299m / 69m and 291m / 65m revenue / EBITDA), converted at the FX cell. Not back-solved.
- **Forecast.** FY2026E–FY2030E, unlevered free cash flow, end-year discounting. Terminal value uses a normalised terminal year (margin, D&A, capex and working capital at steady state), so the margin and growth sensitivities are exact.
- **WACC 8.82%.** Risk-free 4.0%, equity risk premium 5.5%, beta 0.821 (unchanged), blended statutory tax 22.04% and revenue-weighted country risk premium 1.44% (both from the seven-country split), debt weight 20%, terminal growth 3.0%.
- **Tax.** Statutory rates only. Singapore 17% (IRAS), Papua New Guinea 30% (PwC), Australia 30% (ATO), plus the four rates from the September model.

## The three cases

| Case | Revenue growth | EBITDA margin | Rationale |
|---|---|---|---|
| Base (seller / standalone) | 5% a year | Reported FY2025 margin (22.3%) held flat | The ~5% ASEAN market growth is the only cited growth anchor. No source supports margin expansion. |
| Buyer | FY2026E revenue USD 330m (Nippon Paint's projection), then 5% | 26% in FY2026E, fading to 24.2% by FY2030E | Nippon Paint's view (single-source), with an illustrative fade. |
| Downside | 3% a year | Base less 1pp in FY2026E and 2pp after | Standalone-cost risk: AkzoNobel keeps Global Business Services, so replacing them is a real cost. |

TSA and stranded costs are shown inside the case margin, not deducted a second time. Only the one-time separation cost (EUR 8m, unchanged and probably understated) reduces cash flow separately.

## Results

| EUR m | Base | Buyer | Downside |
|---|---|---|---|
| DCF enterprise value | **712.7** | **853.7** | **586.2** |
| Low / High (WACC ±0.5pp, g ∓0.5pp) | 618 / 846 | 741 / 1,012 | 510 / 694 |
| Implied EV / FY2025 EBITDA | 12.3x | 14.8x | 10.1x |

| EUR m | Low | Mid | High |
|---|---|---|---|
| Weighted triangulation (rounded to 25) | 550 | **775** | 1,100 |

Weights (fixed first): DCF 40% (Base 25, Buyer 7.5, Downside 7.5), comps EV/EBITDA 25%, comps EV/Revenue 10%, precedents EV/EBITDA 15%, precedents EV/Revenue 10%. The logic is on the Triangulation sheet.

## Gap versus the announced EUR 1,200m

- The announced EV is **EUR 415m (53%) above** the weighted mid-point (EUR 785m unrounded) and above the top of the range (EUR 1,100m). All three DCF cases fall short: Base by 487 (68%), Buyer by 346 (41%), Downside by 614 (105%).
- Methods whose *high* case reaches EUR 1,200m: two of seven (comps EV/EBITDA at P75, precedents EV/EBITDA at the maximum). The precedent EV/EBITDA mid (EUR 1,058m) is the closest single mid-point; it rests on two data points, one a rejected offer.
- The conclusion is stable across the alternative weightings on Deal_Check (gap 46%–68%).
- At the announced price: 20.8x FY2025 reported EBITDA (AkzoNobel states 21x); 19.8x Base FY2026E EBITDA; 15.7x Buyer FY2026E EBITDA (Nippon Paint states about 16x, an arithmetic cross-check of the 2026 projection).

## Reverse DCF: what you need to believe to reach EUR 1,200m

| Holding all else | Base | Buyer | Downside |
|---|---|---|---|
| Terminal EBITDA margin needed | 38.7% | 34.9% | 43.0% |
| Terminal growth needed (WACC 8.82%) | 5.7% | 5.0% | 6.4% |

For comparison, the reported FY2025 margin is 22.3%, Nippon Paint's 2026 projection is about 26%, and the model's terminal growth is 3.0%. Reaching the announced price on stand-alone cash flows needs a margin 9–16 points above reported, or perpetual growth of 5–6%. The remaining gap is most plausibly buyer-specific synergies and strategic value that a seller-side standalone DCF does not capture, a lower discount rate than 8.8%, or a better business than the reported numbers show. This analysis cannot tell these apart.

## Synergies needed to justify the price (ILLUSTRATIVE)

The announced EV exceeds the standalone DCF by EUR 487m (Base, 41% of price) and EUR 346m (Buyer case, 29%). Closing that gap with run-rate cost savings alone, capitalised after tax at WACC 8.82% and growth 3.0% with a one-off integration cost of 1.0x the saving, would need about **EUR 38.6m a year (Base; 14.9% of FY2025 revenue)** or **EUR 27.5m (Buyer case; 10.6%)**. September's heuristic applied to FY2025 revenue gives EUR 5.2m to 10.3m of cost savings; one outlet (SRC-048, attribution not stated) reports savings in the high single digits as a percentage of sales (about EUR 18m to 23m at 7% to 9%). This cannot separate synergies from a lower discount rate, a better business than reported, or strategic value.

## Buyer outcome

Nippon Paint is the buyer (PUBLIC FACT). SCG is not mentioned in the coverage checked (which does not show whether it bid); there is no evidence either way for Kansai Paint, Asian Paints / Berger, Sherwin-Williams or PPG. No bidder list is public.

## EV versus what AkzoNobel keeps

EV EUR 1.2bn less net cash proceeds EUR 0.9bn is EUR 0.3bn (25%), which the release attributes to taxes and payments to minority partners. It is **not** an equity value: the perimeter's net debt and minority interests are not disclosed.

## Limitations

- **Financials are reported, not in AkzoNobel's release.** FY2024 and FY2025 revenue and EBITDA are reported by several outlets, attributed to Nippon Paint; the primary Nippon Paint release was not read; not in AkzoNobel's release. (Investing.com and Yahoo Finance UK attribute them to Nippon Paint; Yahoo Finance Singapore gives them without a named source.) Labelled REPORTED, not PUBLIC FACT.
- **2026 projection is single-source** (PCI Magazine; not found in five other outlets checked (SRC-041 to SRC-043, SRC-047, SRC-048); revenue "above ~USD 330m" uses the floor). It is the buyer's view.
- **Country split and country risk premiums are illustrative.** The split rescales the September four-country split and adds Australia 8%, Singapore 5% and Papua New Guinea 2%. The risk-premium tiers are an analyst ordering, not a published table. Sensitivity: weighting the seven countries equally moves WACC by −0.02pp.
- **Comps are dated 2026-09-18** and were not refreshed. Beta 0.821 is unchanged.
- Gross margin, D&A, capex, working capital and separation cost are the September illustrative inputs.
- Whether the reported margin is on a standalone basis is unknown.
- **Not refreshed:** `07_Pitch_Deck/` and the September Information Memorandum remain the September record (the memorandum has a status-notice copy here; the transaction review deck replaces the pitch deck's post-announcement role). The synergy-needed block, integration-cost multiple and full-run-rate timing are illustrative.

## Verification performed

- Both workbooks recalculated with LibreOffice headless; every formula has a stored value; scan for `#REF!`, `#DIV/0!`, `#NAME?`, `#VALUE!`, `#N/A` found none.
- The DCF (all three cases, Low/High scenarios and the reverse DCF) was replicated independently in plain Python and matched the workbook to better than 1e-6.
- Pasted model values in the Valuation workbook were checked against the model cells.
- The Cases sheet carries an in-workbook check that the active-case DCF equals the matching case (0.000000).
