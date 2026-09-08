# Strategy Log — Autonomous Income Experiment

Persistent journal for the agent across sessions. Read this first on every run.

## Rules of engagement (set by user, 2026-09-08)

- Only free tools/services may be used for real. Every one is still charged against
  a notional budget as if it cost money — this forces strategy pivots instead of
  infinite free iteration.
- Each strategy gets a **$50 notional budget** (see BUDGET.md). When a strategy's
  budget hits $0, stop iterating on it, write a postmortem below, and start a new
  strategy with a fresh $50.
- Full autonomy on: coding, design, deployment, content, iteration, pivoting.
- MUST pause and ask the user before: creating any new financial/payment account,
  creating accounts on their behalf on third-party platforms, agreeing to any
  platform ToS as them, spending real money, or publishing anything that makes
  false/fabricated claims (fake testimonials, fake user counts, etc).
- No app store distribution (Apple $99/yr, Google $25 — violates free-only rule)
  unless the user explicitly opts to pay those fees.
- No spam, mass cold outreach, fake engagement, or other deceptive growth tactics.

## Strategy 01: Client-side file toolkit ("Deskline Tools")

- **Idea**: Free, no-upload, no-signup web tool — merge/split PDFs, compress
  images, images→PDF — all processed in-browser (privacy angle doubles as the
  trust/marketing hook, since files never leave the visitor's device).
- **Why this idea**: Evergreen search demand, zero backend/server cost, fully
  buildable and deployable without any account beyond GitHub Pages (already
  authenticated on this machine), clean fit for a voluntary tip jar.
- **Stack**: static HTML/CSS/JS, pdf-lib + JSZip via CDN, GitHub Pages hosting.
- **Monetization**: voluntary tip link (Buy Me a Coffee / Ko-fi — needs user to
  create the account, since it's tied to their identity/payout). No ads, no
  affiliate links yet (would need real relevance — won't bolt on generic
  affiliate spam for its own sake).
- **Status**: v1 built, verified, and deployed live 2026-09-08 at
  https://jamar-clarke.github.io/deskline-tools/ (repo:
  github.com/jamar-clarke/deskline-tools, GitHub Pages, free). All four tools
  tested end-to-end pre-deploy — merge, split (range + split-to-zip),
  compress, and images→PDF all pass.
- **Checkpoints raised to user**: (1) which GitHub account to publish under —
  resolved, using `jamar-clarke`. (2) Tip jar — user chose to create a
  Buy Me a Coffee / Ko-fi account themselves and hand me the link.
- **Open item**: waiting on the user's tip-jar URL. Once given, update the
  `#tipLink` href in `strategy-01-file-toolkit/index.html`, commit, and push
  (GitHub Pages redeploys automatically on push to `main`).
- **Next steps once tip link is wired**: no organic traffic yet since nothing
  has been submitted anywhere. Legitimate no-cost discovery channels to try:
  submitting to relevant subreddits/forums where self-promotion is allowed
  (with disclosure, not spam), a Show HN-style post, and a couple of
  "free online tools" directory listings. All of that is regular/reversible
  work I can do myself — will log attempts and results here.

## Postmortems

(none yet — first strategy in progress)
