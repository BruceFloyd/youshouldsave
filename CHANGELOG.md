# Changelog

All notable changes to Glidepath, the Monte Carlo retirement simulator.

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
