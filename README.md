# BLKOUTUK org-wide files

## Security sweep

`.github/workflows/security-sweep.yml` is the reusable security workflow for the estate
(adopted 13 Aug 2026 — Dreamcatcher OSS delta, wish-list item 7 rubric:
"routine code and security review as a rhythm not an event").

Each covered repo carries a small caller at `.github/workflows/security.yml`
(weekly Monday cron + pull requests + manual dispatch). What runs:

| Layer | Tool | Mode |
|---|---|---|
| Secrets in working tree | gitleaks CLI (MIT — the *action* is not MIT, so the CLI is invoked directly) | **blocking** |
| GitHub Actions workflow audit | zizmor | **blocking at high severity** |
| Dependency vulnerabilities | osv-scanner | advisory (Dependabot alerts carry notification) |
| Static analysis (js/ts/python) | opengrep + opengrep-rules, ERROR severity | advisory |

Alongside, per repo: Dependabot alerts + security-fix PRs, and CodeQL default setup.

**To add a repo:** copy `security.yml` from any covered repo (one file, no edits needed).
**To bump tool versions:** edit the pinned versions at the top of `security-sweep.yml` here —
every repo follows on its next run.

Covered as of 13 Aug 2026: blkout-community-platform, news-blkout,
black-qtipoc-events-calendar, blkout-crm, ivor-core, align, bmhwa-manifesto, comms-blkout.
