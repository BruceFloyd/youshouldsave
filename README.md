# You Should Save

**Glidepath** is a single-file, dependency-free Monte Carlo retirement simulator. Open `glidepath.html` in any browser — no build step, no server, no external libraries.

## What it does

Enter your plan (age, retirement age, portfolio, savings, spending, Social Security, and asset allocation) and it runs 1,000 randomized market histories against long-run U.S. return and volatility assumptions, reporting:

- **Probability of success** — the share of trials in which money lasts through your planning horizon
- **Fan chart** — median portfolio path with 10th–90th percentile bands, in today's dollars
- **Sensitivity table** — how success odds shift as you vary retirement age (±2 years) and spending (80–120%)
- **Spending flexibility** — an optional guardrail that cuts spending in down-market years

All figures are real (inflation-adjusted). Trials are seeded deterministically from your inputs, so the same plan always shows the same result.

See [CHANGELOG.md](CHANGELOG.md) for version history.

*Educational model, not financial advice.*
