# Expected ShipCheck findings

All values in this repo are FAKE. Verified against a real ShipCheck scan on 23 Oct 2026 (score 62/100, 4 issues).

| # | Severity | Finding | Where |
|---|----------|---------|-------|
| 1 | Critical | 1 secret committed in current files: Stripe access token (`sk_t***`, fake) | `.env:3` |
| 2 | Critical | `.env` file committed | `.env` |
| 3 | High | 6 known vulnerabilities in 1 dependency (3 high, 3 moderate), e.g. GHSA-35jh-r3h4-6jhm, GHSA-p6mc-m468-83gw, GHSA-r5fr-rjxr-66jc | `lodash@4.17.15` in `package-lock.json` |
| 4 | Lower | No `.gitignore` (so `.env` isn't ignored) | repo root |

## Seeded but deliberately NOT reported

- `src/config.js` contains `AKIAIOSFODNN7EXAMPLE` / `wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY`, AWS's published documentation
  example key. ShipCheck recognises it as a known example value and does not flag it as a leaked secret. That's correct
  behaviour: it shows ShipCheck doesn't cry wolf on placeholder keys.
- Git history: no extra history-only secrets (everything is in the current files).
