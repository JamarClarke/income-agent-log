# Budget Ledger

Notional budget only — all tools used are actually free. Every session/resource
is still charged at its typical market rate to force real strategy discipline.

## Strategy 01: Deskline Tools — budget $50.00

| Date       | Item                                              | Notional cost | Remaining |
|------------|---------------------------------------------------|---------------|-----------|
| 2026-09-08 | Initial build session (design + 4 tools + deploy prep) | $15.00        | $35.00    |
| 2026-09-08 | QA session (end-to-end test of all 4 tools in a real browser) | $5.00 | $30.00 |
| 2026-09-08 | Repo setup + GitHub Pages deployment | $5.00 | $25.00 |
| 2026-09-08 | Bug fix: working drag/keyboard reorder for the merge file list (help text promised this but it didn't exist — found by the daily routine's first run, recovered and pushed manually after the routine's own push failed) | $6.00 | $19.00 |
| 2026-09-09 | Bug fix: transparent PNGs turning black when compressed (JPEG re-encode with no background fill) | $4.00 | $15.00 |
| 2026-09-09 | Growth pass: header tip-link placement, technical SEO (OG/Twitter/JSON-LD/sitemap/robots.txt), drafted 6 outreach/submission pieces, GitHub org migration for a clean URL | $8.00 | $7.00 |
| 2026-09-09 | Bug fix: Compress tool leaked a blob URL (`URL.createObjectURL`) per image, never revoked | $3.00 | $4.00 |
| 2026-09-09 | Bug fix: Split tool's page-range parser silently dropped backwards ranges (e.g. "5-3") instead of extracting them | $3.00 | $1.00 |

**Remaining: $1.00**

Pivot trigger: when remaining hits $0, stop iterating on Strategy 01, write a
postmortem in STRATEGY_LOG.md, and start Strategy 02 with a fresh $50.00.
