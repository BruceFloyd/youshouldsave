# Changelog

All notable changes to Glidepath, the Monte Carlo retirement simulator.

## [2.1] — 2026-08-19

The single calculator becomes a three-page site for ishouldsave.com.

### Added
- **Landing page (`index.html`).** Welcomes visitors and routes them to one of two tools: the Simple Investment Calculator ("quick estimate", ~2 min) or the Advanced Simulation ("full plan", ~10 min), with a "not sure which?" guide, growth-chart hero, and shared site navigation.
- **Simple Investment Calculator (`simple.html`).** A calculator.net-style compound growth tool: starting amount, years, return rate, compounding frequency (annual through daily), and scheduled contributions (monthly/annual, beginning/end of period). Outputs an end balance with a donut breakdown (principal / contributions / interest), a stacked growth-by-year chart with hover details, and a full accumulation schedule table.
- **Tooltips everywhere.** Every input on both calculators carries a "?" tooltip (hover, keyboard focus, or tap) explaining the field in plain language — 31 on the advanced page, 7 on the simple one.
- Shared site header/navigation and consistent design system (IBM Plex Sans/Mono, warm neutrals, blue accent, light/dark themes) across all pages.

### Changed
- The retirement simulator moved from `index.html` to **`advanced.html`** and is now titled **Advanced Simulation** (formerly "Glidepath"), per-page branding replaced by the I SHOULD SAVE site wordmark.

## [2.0] — 2026-08-19

Major engine upgrade toward advisor-grade planning: taxes and account types, guardrails spending, stress tests, and household modeling. The generator stays advisor-simple (iid normal by default).

### Added
- **Taxes & accounts.** Three buckets — taxable, tax-deferred, Roth — with a shared allocation and annual rebalance. Withdrawals gross up for tax: deferred at a user ordinary rate (default 22%), taxable at a user capital-gains rate (default 15%) assuming 50% of each withdrawal is gain, Roth tax-free. RMDs from deferred start at 73 or 75 by birth year (SECURE 2.0, auto-computed) using the Uniform Lifetime Table; excess RMD proceeds reinvest in taxable. Withdrawal order defaults to taxable → deferred → Roth, user-overridable. Savings direct to a chosen bucket (default deferred).
- **Guardrails spending rule (new default).** Guyton–Klinger-style: cut spending by the slider amount when the current withdrawal rate breaches 120% of its starting level; restore when it falls below 80%. Cuts are sticky until recovery and floor at 70% of plan. The old down-year rule remains as "Simple" mode, plus a "Fixed" mode. A new hero stat reports the share of trials that ever cut spending — the honest companion to a high success rate under adaptive rules.
- **Stress test panel.** Always-on: stock–bond correlation 0.40 (full 1,000-trial rerun), Social Security × 0.85 from a user year (default 2034, also available as a base-plan toggle), and four deterministic historical replays hitting in the first retirement years — 1966–82 stagflation, 2000–02 dot-com bust, 2008, and 2022 — using approximate real total returns.
- **Joint household.** Optional spouse with own age, plan-to age (default 90), and Social Security benefit/claim age. After the first death the survivor keeps the larger benefit check and spending drops to a user factor (default 75%). The horizon runs to the later death; a new stat reports the age through which 90% of trials stay funded.
- **Healthcare line.** User annual amount (default $7,000) added to spending from age 65, growing faster than CPI (default +1.5%/yr real). Flat line, not IRMAA brackets.
- **Fees.** Annual fee/drag (default 0.20%) subtracted from returns before cash flows.
- **Spending smile.** Optional −1%/yr real spending decline after a user age (default 75).
- **Research toggles.** Stock mean: planning 6.8%/17.2% (default, labeled as a conservative forward assumption) vs. historical arithmetic 7.8%/18%. Distribution: normal (default) vs. Student-t df 5 for fat tails.
- Collapsible input sections; honesty notes replacing the old assumptions blurb (iid caveat, stylized taxes, no LTC by default, CPI-W vs. household inflation, year-end timing).

### Changed
- Success stays "portfolio never hits $0" and failed-stays-failed; deterministic seeding and re-roll unchanged.
- Sensitivity table now runs the full engine per cell and varies base spending only (healthcare unchanged).

### Impact (default plan, now including taxes, fees, healthcare)
- Success probability ~98% with guardrails; 55% of trials cut spending at least once. A fixed-spending $110k/yr variant scores 67% and runs dry at 88 in the 1966–82 replay — the adaptive rule, not optimism, carries the plan.

## [1.1] — 2026-08-19

### Added
- **Social Security income.** Two new inputs: estimated annual benefit (in today's dollars) and claiming age (62–70, default $24,000/yr at 67). From the claiming age on, the benefit offsets retirement spending; if claimed while still working it adds to annual savings, and any surplus over spending is reinvested in the portfolio. A dotted "SS" marker on the fan chart shows when benefits begin. Set the benefit to $0 to exclude it.
- **Spending flexibility (guardrail rule).** A new slider (0–30%, default 0%) cuts retirement spending by the chosen percentage in any year the portfolio return is negative; spending returns to normal after positive years. Models the real-world behavior of trimming discretionary spending in down markets.

### Changed
- The deterministic trial seed now incorporates the new inputs, so changing Social Security or flexibility settings re-runs all 1,000 trials.
- The sensitivity table ("What moves the odds") applies both new rules in every cell, so the retirement-age × spending grid reflects the full plan.
- Assumptions section documents both rules, including that a trial that runs dry stays failed even if benefits continue.
- Chart markers stagger onto two lines when the retirement and claiming ages are close enough to collide.

### Impact (default plan: $750k, $30k/yr savings, retire 65 on $80k/yr, 60/30/10)
- Success probability: 91% → 98% with default Social Security ($24k/yr at 67).
- Typical depletion age in failed trials: 88 → 91.

## [1.0] — 2026-08-19

### Added
- Initial release of **Glidepath**, a single-file interactive Monte Carlo retirement simulator.
- **Inputs:** current age, retirement age, planning horizon ("plan through age"), portfolio value, annual savings, annual retirement spending, and stock/bond/cash allocation via sliders (cash is the remainder).
- **Simulation engine:** 1,000 randomized market trials per input change, re-run live with a 160 ms debounce. Real (inflation-adjusted) annual returns drawn from normal distributions — stocks 6.8% mean / 17.2% σ, bonds 2.0% / 6.5%, cash 0.5% / 1.0%, stock–bond correlation 0.10 — with annual rebalancing, end-of-year cash flows, and a deterministic per-input seed (mulberry32 + Box–Muller) so identical plans always produce identical results. A re-roll button samples a fresh trial set.
- **Probability of success** hero: percentage of trials that keep money through the planning horizon, with On track / Borderline / At risk status (≥85% / 70–84% / <70%), a threshold meter, median ending balance, and typical depletion age among failed trials.
- **Fan chart:** median portfolio path with 25th–75th and 10th–90th percentile bands by age, a retirement-age marker, and a hover crosshair reporting all five percentiles at any age.
- **Sensitivity table:** retirement age (±2 years) crossed with spending (80–120% of target), each cell its own 1,000-trial run, color-coded by success band with the current plan outlined.
- Full light/dark theming, IBM Plex Sans/Mono typography, and a colorblind-validated chart palette.
