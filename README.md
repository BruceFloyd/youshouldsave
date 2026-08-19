# I Should Save

The source for [ishouldsave.com](https://ishouldsave.com) — free, dependency-free financial tools that run entirely in the browser. No build step, no server, no external libraries; every page is a single self-contained HTML file.

## Pages

- **`index.html`** — landing page that routes visitors to the right tool.
- **`simple.html`** — Simple Investment Calculator: compound growth with scheduled contributions, an end-balance breakdown, growth chart, and accumulation schedule.
- **`advanced.html`** — Advanced Simulation: a Monte Carlo retirement model running 1,000 randomized market histories with taxes and account types (taxable / tax-deferred / Roth, RMDs), Social Security scenarios, guardrails spending, healthcare, joint-household survivor modeling, and historical stress replays (1966–82, 2000–02, 2008, 2022).

Every input on both calculators has a plain-language tooltip. All simulation figures are real (inflation-adjusted); trials are seeded deterministically so the same plan always shows the same result.

Deployment: rsync to DreamHost via GitHub Actions on push to `main` (see `.github/workflows/deploy.yml`; requires `DEPLOY_HOST`, `DEPLOY_USER`, `DEPLOY_KEY` secrets).

See [CHANGELOG.md](CHANGELOG.md) for version history.

*Educational tools, not financial advice.*
