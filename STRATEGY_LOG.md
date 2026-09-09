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
- **2026-09-09 — account migration**: user clarified their actual GitHub
  identity is `JamarClarke`, not `jamar-clarke` (both are theirs, but
  `JamarClarke` is the one to use going forward). Transferred both repos
  (`deskline-tools` and `income-agent-log`) to `JamarClarke` via the GitHub
  API. GitHub Pages settings carried over automatically. Live URL is now
  **https://jamarclarke.github.io/deskline-tools/** (repo:
  github.com/JamarClarke/deskline-tools). `jamar-clarke` was auto-retained
  as a write collaborator on both repos post-transfer, so pushes from this
  machine kept working without needing a fresh local GitHub login.
  Control repo is now github.com/JamarClarke/income-agent-log.
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

## Maintenance log

- **2026-09-09**: Found and fixed a real bug in the Compress tool: images are
  always re-encoded as JPEG for output, but the canvas used to do the
  re-encoding was never given an opaque background first. JPEG has no alpha
  channel, so a transparent PNG (e.g. a logo or a screenshot with a
  transparent background) would come out of "compression" with its
  transparent areas turned solid black instead of staying visually
  unchanged. Fixed by filling the canvas white before drawing the source
  image — a no-op for already-opaque JPEG/PNG input, and correct for
  transparent PNGs. Also did brief passive research (see below). Notional
  cost $4.00, remaining $15.00 (see BUDGET.md).
  - **Passive market research**: free PDF tool complaints in 2026 center on
    daily usage caps, forced signups, and watermarks on "free" tools
    (per-tool limits like a 2-task/day cap are a common pain point) —
    reinforcing that Deskline's genuinely-unlimited, no-signup angle is a
    real differentiator, not just marketing copy. Also saw repeated demand
    for page thumbnails and rotate-page controls in merge/split tools, which
    Deskline doesn't have yet — worth considering as a future small
    improvement, not built today.

- **2026-09-08**: Found and fixed a real bug in Deskline Tools: the Merge
  panel's help text said "drag the list to set the order," but no
  drag-and-drop or keyboard reordering code existed — the list was static.
  Implemented a reorderable file list (HTML5 drag-and-drop + up/down arrow
  keys for accessibility), updated the help text, tested end-to-end in a
  real browser (3-file merge, reorder via keyboard, merge succeeds with the
  new order). Notional cost $6.00, remaining $19.00 (see BUDGET.md).

## Daily routine — incident (2026-09-08) and current status

The scheduled daily maintainer (routine `trig_01G9hP3jWsmC1CuUE4b7dQME`) ran
for the first time, correctly diagnosed and built the drag-to-reorder fix
above, but **failed to push to either repo**: GitHub returned a 403 with
"Claude doesn't have GitHub access to jamar-clarke/... for your
organization," even though the user had just installed the Claude GitHub
App. The routine's commits only existed inside its (ephemeral) cloud
sandbox and were not recoverable from there, so the fix was reproduced and
pushed manually from an interactive session instead (see Maintenance log
entry above) — no work was actually lost, but this cost extra manual effort
and the sandbox commits are gone.

**Root cause (likely)**: the Claude GitHub App installation didn't grant
access to these two specific repos (`deskline-tools` and
`income-agent-log`) — either "All repositories" wasn't selected, or the
repos were created *after* the App was installed and need to be added
explicitly.

**## AWAITING USER**: Please check the Claude GitHub App installation at
https://github.com/apps/claude/installations/select_target and confirm it
has access to both `jamar-clarke/deskline-tools` and
`jamar-clarke/income-agent-log` (either select them explicitly, or choose
"All repositories"). The routine is **paused** (enabled: false) until this
is confirmed, so it doesn't keep failing silently (locally) once a day and
sending push notifications about blocked runs. Once fixed, ask Claude to
re-enable the routine and it will re-verify with a test run before leaving
it unattended again.

## Postmortems

(none yet — first strategy in progress)
