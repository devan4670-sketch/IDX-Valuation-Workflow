# IDX Valuation Workflow

A skill for Claude that walks an analyst through valuing one IDX-listed company from its audited filings: three-statement model, DCF, trading comps and LBO, with a pass or fail check at the end of every stage.

It was developed on PT Astra Agro Lestari Tbk (IDX: AALI) in September and October 2026.

## What it does

| Stage | Output | Gate before moving on |
|---|---|---|
| 1. Historical financials | Statements mapped to the model, every figure cited | Balance sheet ties; cash rolls forward |
| 2. Three-statement model | Driver-based forecast, five years | Five integrity tests |
| 3. Cost of capital | CAPM with a regressed beta | Every input sourced and dated |
| 4. DCF | Value per share, reverse DCF, sensitivities | Sensitivity centre equals base case |
| 5. Trading comps | Peer multiples, normalised | Source note for every input |
| 6. LBO | Debt schedule, covenants, returns | Sources equal uses; all checks pass |
| 7. Recalculation | Results rebuilt outside Excel | Outside figures match the workbook |

## Working rules built into the skill

- No invented inputs. Each one is cited or labelled as the author's assumption.
- When the AI's extraction and the filing disagree, the filing is right.
- The analyst enters the formulas; the AI specifies, explains and audits.
- No stage starts while the previous gate is failing.

## How to use it

`SKILL.md` is the skill file. Add it to Claude as a skill, supply the company's audited statements and peer filings, and ask for a valuation. Section 3 of the file lists the inputs to prepare.

## Worked example: AALI

| Item | Result |
|---|---|
| DCF value per share | Rp8,160 against a market price of Rp8,425 (10 September 2026) |
| WACC | 13.33%, equal to cost of equity (no bank debt) |
| Reverse DCF | Market implies a 5.56x exit multiple, or 6.42% perpetual growth |
| Bear to bull range | Rp7,270 to Rp9,071 per share on the mid-cycle CPO price |
| LBO at a 30% premium | 1.75% IRR, 1.09x MOIC; covenants pass in all scenarios |

## Limits

- For learning and portfolio work. It is not investment advice.
- Not suitable for banks and insurers, or for companies with fewer than three years of audited statements.
- The checks catch errors of arithmetic and consistency. They do not catch a wrong assumption.
- The same inputs give the same numbers, but the AI's wording differs between runs.

## Author

Reza Dila Andrea
