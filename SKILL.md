---
name: idx-valuation-workflow
description: Build and audit a three-statement model, DCF, trading comps and LBO for an IDX-listed company from its audited filings, with a check at every stage. Use for a learning or portfolio valuation.
---

# IDX Valuation Workflow

A repeatable procedure for valuing one IDX-listed company with an AI assistant, from raw filings to a checked DCF, trading comps and an LBO. It was developed on PT Astra Agro Lestari Tbk (IDX: AALI) in September and October 2026 by Reza Dila Andrea. Section 7 gives the AALI results so a rerun can be compared against them.

## 1. What it is for, and what it is not

**Use it to**

- value a listed operating company from public filings, with every input traceable to a page;
- learn the mechanics of a three-statement model, DCF, comps and LBO on a real company;
- produce a model that survives questioning, because each stage ends in a test.

**Do not use it for**

- investment or transaction decisions. The output is a study, not advice;
- banks, insurers and other financials. Their debt is operating, so the free cash flow and EV logic here does not apply;
- companies without at least three years of audited statements;
- anything that needs private information, management forecasts or precedent transaction data.

**Limits of reproducibility**

- The same filings and the same assumptions give the same numbers, because every result is an Excel formula.
- The AI's wording and suggestions vary between runs. What repeats is the sequence of steps and the checks, not the conversation.
- Judgement inputs (mid-cycle price, beta, exit multiple, deal terms) are choices. A different analyst can run this workflow correctly and reach a different value.
- The checks catch arithmetic and consistency errors. They do not catch a wrong assumption.

## 2. Working rules

Follow these in every stage.

1. **No invented inputs.** Every input is either cited (document, page, original label) or labelled "author's assumption". If a figure cannot be found, say so and leave the cell empty.
2. **The filing wins.** When your extraction and the filing disagree, the filing is right. Report the difference; do not smooth it.
3. **The analyst owns the model.** By default the analyst enters formulas and you specify, explain and audit. Write formulas into the file yourself only when asked, and record which sheets you wrote.
4. **Audit at cell level.** When a file is uploaded, open it and report errors by sheet and cell address, with the corrected formula. Do not review from a description.
5. **No stage is finished until its gate passes.** Do not start the next stage on a failing check.
6. **Nothing is claimed before it can be explained.** A formula counts as the analyst's only once they can rebuild it without help. Say so when a result is being used before that point.
7. **Check the locale.** Indonesian Excel uses a comma for decimals and a semicolon between formula arguments. Give formulas in the analyst's locale.
8. **Excel for the web has no Goal Seek or Data Tables.** Build sensitivities from live formulas, and run goal seeks by formula or in a recalculation outside Excel.

## 3. Inputs the analyst must supply

| Input | Detail |
|---|---|
| Audited annual statements | At least three years, with comparatives, from IDX |
| Latest interim statements | For LTM figures: LTM = last full year + current interim period - same period last year |
| Annual reports | Operating data that drives revenue (for a plantation: mature area, yield, extraction rate, volumes, selling price) |
| Peer filings | Five to nine listed peers; state which exchange each reports to |
| Market data | Share price and date, shares outstanding, weekly prices for the beta regression |
| A lender benchmark | Loan terms of one listed peer, for LBO interest and covenants |

## 4. Procedure

### Stage 1. Historical financials

1. Extract the income statement, balance sheet and cash flow statement for each year into one table, mapped row by row to the model template.
2. Cite every figure. Keep the original Indonesian label next to the English one.
3. Where the template has no row for a real item, add "Other assets" and "Other liabilities" rows. Do not force the balance.
4. Keep an open items list for gaps (for example, a note missing from one year's filing).

**Gate 1:** assets equal liabilities plus equity in every year, and cash rolls forward from one year to the next.

### Stage 2. Three-statement model

1. Decompose revenue into its drivers before any forecast. For a commodity producer: volume times price, with own production and third-party throughput built separately.
2. Reconcile the driver build to reported revenue for every historical year.
3. Forecast five years. Build schedules for D&A, working capital and debt.
4. For a cyclical business, set the terminal year on a mid-cycle price, derived in real terms from the history.

**Gate 2, five integrity tests:** profit before tax, net earnings, closing cash against the balance sheet, balance sheet check equal to zero, and debt closing schedule.

**Gate 2b, sanity checks:** growth against its drivers, margins against history and peers, capex against D&A (converging to 1.0x by the terminal year), cash build-up, working capital days, terminal year assumptions.

### Stage 3. Cost of capital

1. Risk-free rate: the 10-year government bond yield in the model's currency.
2. Equity risk premium: 7% to 9% for Indonesia, including country risk. Do not add a country premium again if the risk-free rate is already a local yield.
3. Beta: regress weekly log returns of the company and each peer against their local index. Apply the Blume adjustment, unlever, take the peer median, relever to the target structure.
4. Compare the result with the company's own regression. If a data vendor shows values that make no economic sense, reject them and record why.
5. If the company has no financial debt, WACC equals cost of equity. State this as a fact about the capital structure, not as a shortcut.

**Gate 3:** each input has a source and date; the beta choice is explained in one sentence.

### Stage 4. DCF

1. Unlevered free cash flow = EBIT - tax on EBIT + D&A - capex - increase in net working capital. Tax is on EBIT, not on profit before tax.
2. Discount with the mid-year convention.
3. Terminal value by exit multiple, then compute the perpetual growth it implies. Report the implied growth even when it falls outside a sensible range, and explain the cause.
4. Bridge enterprise value to equity: add cash and investments in joint ventures, subtract debt and non-controlling interests.
5. Reverse DCF: find the exit multiple and the growth rate that reproduce the market price.
6. Sensitivities from live formulas: value against the main driver, the discount rate and the exit multiple.
7. Scenarios: bear, base and bull on the single most important driver.

**Gate 4:** the centre cell of each sensitivity table equals the base case output, and the implied terminal multiple and growth are both reported.

### Stage 5. Trading comps

1. Spread LTM figures for each peer from its own filings.
2. Build EV for each peer with the same bridge as Stage 4.
3. Do not convert currencies. Multiples are ratios, so the currency cancels.
4. Report medians separately by country when tax or levy regimes differ.
5. Normalise: remove fair value gains on biological assets from EBITDA, and align D&A sources, joint venture income, non-controlling interests and reporting units.
6. Exclude a peer when its multiple is an artefact (for example, net cash close to market value, or a change of control in the period). Record the reason.

**Gate 5:** every input has a source note, and each exclusion has a written reason.

### Stage 6. LBO

1. Export the forecast (revenue, EBITDA, D&A, capex, working capital) and the bridge items from the DCF file into an import sheet.
2. Assumptions: premium, fees, minimum cash, leverage, interest, amortisation, hold period, exit multiple, target returns, covenants. Mark each as sourced or assumed.
3. Sources and uses, with sponsor equity as the balancing item.
4. Operating forecast with levered tax.
5. Debt schedule: interest on opening balances (no circular reference), mandatory amortisation, cash sweep above minimum cash, covenant ratios each year.
6. Returns: exit equity, MOIC, IRR, a value bridge (EBITDA growth, multiple change, debt paydown, fees), and the highest price that still earns the target return.
7. Scenarios reuse the DCF scenarios. Keep the debt amount fixed at the base case, because debt is sized at closing.

**Gate 6:** sources equal uses, no debt balance goes negative, the sensitivity centre equals the base case, and an overall status cell reads `ALL PASS`.

### Stage 7. Independent recalculation and documentation

1. Rebuild the debt schedule and the scenario results outside Excel (for example in Python) and compare.
2. Add a cover sheet, a methodology sheet, and a source column beside every input row.
3. Write the limitations down before presenting any result.

**Gate 7:** the outside recalculation matches the workbook, and the limitations list exists.

## 5. What to hand back at the end of each stage

- the gate result, pass or fail, with the failing cells if any;
- the open items list;
- which formulas were written by the AI in this stage;
- one sentence the analyst can say in an interview about what the stage showed.

## 6. Known weak points of this workflow

1. It values on one driver. A company with several independent drivers needs a wider scenario set.
2. The terminal value usually carries most of the value, and the two terminal methods often disagree. The workflow reports the gap; it does not resolve it.
3. Comps depend on a small peer set. With fewer than five clean peers the median is fragile.
4. LBO deal terms are assumed unless a comparable transaction is found.
5. An AI can misread a figure or write a wrong formula with confidence. The gates reduce this risk; they do not remove it.

## 7. Worked example: AALI

Use these to check a rerun on the same inputs.

| Item | Result |
|---|---|
| Model period | FY2022A to FY2030E |
| Capital structure | No bank debt at FY2025, so WACC equals cost of equity |
| WACC | 13.33% |
| Beta | 0.76 (midpoint of peer median 0.734 and own regression 0.788) |
| Exit multiple | 5.25x EBITDA |
| DCF value per share, base | Rp8,160 against a market price of Rp8,425 |
| Implied perpetual growth | 6.04%, outside the 1.0% to 2.5% range, caused by 36% cash conversion in the terminal year |
| Reverse DCF at market price | 5.56x exit multiple, or 6.42% perpetual growth |
| Peers used | TAPG, SGRO, DSNG, GENP, SDG. LSIP excluded (net cash about 84% of market value) |

| Scenario | Mid-cycle CPO price | Value per share | LBO IRR | LBO MOIC | Covenants |
|---|---|---|---|---|---|
| Bear | 13,500 | Rp7,270 | (2.83%) | 0.87x | Pass |
| Base | 14,884 | Rp8,160 | 1.75% | 1.09x | Pass |
| Bull | 16,300 | Rp9,071 | 5.72% | 1.32x | Pass |

LBO terms: 30% premium, 2.0x senior debt at 10%, 7.5% amortisation, full cash sweep, five-year hold, exit at 5.25x. A 15% IRR requires a price of at most Rp7,754 per share.

**To rerun the scenarios:** change the mid-cycle price in `'3 Statements'!I169` of the valuation file, copy the `LBO Export` sheet into `DCF_Import` of the LBO file, and leave `Assumptions!D10` (mid-cycle EBITDA) at the base value.

**Who did what in the AALI files:** the AI acted mainly as tutor and reviewer. It explained each method, set the order of work, and proposed and audited formulas. It also wrote some parts directly: the historical data extraction, the LBO skeleton, checks and debt schedule, the bear and bull scenario runs, and the written methodology. The analyst chose the company and every assumption, entered the valuation model, and wrote the LBO returns sheet.
