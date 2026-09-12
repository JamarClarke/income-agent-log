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
| 2026-09-10 | Feature gap fix: Images→PDF panel promised page order follows "the order you pick them" but had no way to fix a wrong selection order (Merge already had this); wired the existing tested drag/keyboard reorder code into Images→PDF and updated its help text | $4.00 | -$3.00 |

**Final: -$3.00 (exhausted — postmortem written 2026-09-11, see STRATEGY_LOG.md)**

## Strategy 02: Devline Kit — budget $50.00

User reviewed the Strategy 01 postmortem and picked Idea A (developer
micro-tools) on 2026-09-11. Built and shipped in an interactive session per
the routine's own note that pivot build-out needs human review first.

| Date       | Item                                              | Notional cost | Remaining |
|------------|---------------------------------------------------|---------------|-----------|
| 2026-09-11 | Initial build (new org + repo, design, 4 tools: JSON formatter, regex tester, diff checker, timestamp converter; SEO basics; deploy). Verified all 4 tools end-to-end in a real browser before pushing; fixed one bug found in testing (duplicated line/column in JSON error messages). | $16.00 | $34.00 |

**Final: $34.00 (not exhausted — user redirected the strategy before the
budget ran out; see STRATEGY_LOG.md for why. Devline Kit stays live and
deployed, just no longer being actively iterated on.)**

## Strategy 03: QuoteMint — budget $50.00

User-directed pivot on 2026-09-11: change niche and distribution channel
to something that works on Facebook/Instagram/TikTok/YouTube, since
Strategy 02's dev-tools niche has no video-demoable hook and its
realistic distribution channels (SO/Reddit) turned out to be both
hard for this agent to research and more crowded than assumed. User
picked "fun generators" as the niche and a quote/caption card maker as
the specific product, and will own/post to the social accounts himself
while this agent builds the product and drafts content.

| Date       | Item                                              | Notional cost | Remaining |
|------------|---------------------------------------------------|---------------|-----------|
| 2026-09-11 | Initial build (new org + repo, design, canvas-based card renderer: 4 styles × 4 palettes × 4 social-format sizes, auto-sizing text layout, author attribution, toggleable credit line, PNG export; SEO basics; deploy). Verified end-to-end in a real browser — all 4 styles, size switching, author field, a long-text auto-size edge case, and the actual downloaded PNG file (not just the on-page preview). | $17.00 | $33.00 |

**Remaining: $33.00**

Note (2026-09-12): a font-loading bug fix was found, made, and verified
against Google's live font API this run, but the push to
`quotemint/quotemint.github.io` was rejected with a 403 (Claude GitHub App
has no access to the `quotemint` org) — see STRATEGY_LOG.md. Not deployed,
so not charged against the budget, per the precedent set by the identical
2026-09-08 incident on Strategy 01 (only charge for work that actually
ships).

Pivot trigger: when remaining hits $0, stop iterating on Strategy 03, write a
postmortem in STRATEGY_LOG.md, and start Strategy 04 with a fresh $50.00.
