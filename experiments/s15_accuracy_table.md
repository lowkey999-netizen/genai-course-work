# Session 15 - loan eligibility, ten cases (2026-10-10)

Model: `llama3.2:3b`. Strategies: plain, cot, stepback, vote x5. A cell shows the answer, and ok or WRONG against the answer key.

| Case | Right answer | plain | cot | stepback | vote x5 |
|---|---|---|---|---|---|
| L01-clean | approve | decline WRONG | approve ok | decline WRONG | - |
| L02-ratio-narrow | decline | decline ok | decline ok | - | - |
| L03-score-699 | decline | decline ok | decline ok | - | - |
| L04-boundaries | approve | decline WRONG | approve ok | - | - |
| L05-age-at-end | decline | decline ok | decline ok | - | - |
| L06-age-60 | approve | decline WRONG | approve ok | - | - |
| L07-existing-emis | decline | approve WRONG | decline ok | - | - |
| L08-two-fail | decline | decline ok | decline ok | - | - |
| L09-large-numbers | approve | decline WRONG | decline WRONG | - | - |
| L10-months | approve | decline WRONG | approve ok | - | - |
| **Right** | | 4/10 | 9/10 | 0/1 | - |
| **Average tokens per case** | | 208 | 454 | 908 | - |
