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
- **2026-09-09 — URL cleanup**: user asked to remove their personal
  username from the live URL. Created a free GitHub organization
  (`desklinetools`), transferred the `deskline-tools` repo into it, and
  renamed it to `desklinetools.github.io` so it becomes the org's root
  Pages site. Live URL is now **https://desklinetools.github.io/** — no
  personal identity in it. Updated canonical/OG/JSON-LD/sitemap URLs to
  match. Note: the product repo now lives under a different owner
  (`desklinetools` org) than the control repo (`JamarClarke` personal
  account) — the daily routine's sources need updating to the new repo
  URL, and the Claude GitHub App likely needs separate access granted to
  the `desklinetools` org before the routine can push there again.
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

- **2026-09-10**: Fixed a genuine feature gap in the Images→PDF tool: its
  help text says images "become pages, in the order you pick them," but
  unlike the Merge tool there was no way to fix a wrong selection order —
  `renderFileList()` rendered a static, non-reorderable list. Reused the
  same `renderReorderableFileList()` drag-and-drop/arrow-key code already
  built and browser-tested for Merge (2026-09-08), wiring it into the
  Images→PDF panel's file list and updating the help text to match Merge's
  wording. Verified by re-reading the diff: the `run` click handler already
  iterated the `files` closure variable in order, which `refresh()` now
  reassigns on every reorder exactly as it does for Merge, so no other code
  needed to change. Syntax-checked with `node -c app.js`. The
  non-reorderable `renderFileList()` is untouched and still used correctly
  by the Compress tool, where order doesn't matter.
  - **Passive market research**: this niche has gotten noticeably more
    crowded since the last check — several "no-upload" client-side PDF
    tools now exist (ClientPDF, RaptorPDF, Bontello, others), some offering
    page-reorder as a named feature already and others offering 10-75 tools
    in one suite. Confirms reorder was worth closing as a real gap, and
    reinforces that breadth-of-features won't be how Deskline
    differentiates against better-resourced competitors — simplicity and
    the privacy angle stay the more defensible lane.
  Notional cost $4.00, remaining **-$3.00** (see BUDGET.md). Strategy 01's
  budget is now exhausted — per the strategy rules, the next run should
  write a postmortem for Strategy 01 instead of continuing to iterate on
  the product.

- **2026-09-09 (3)**: Found and fixed a logic bug in the Split tool's page-range
  parser (`parsePageRange` in `app.js`): a backwards range like `"5-3"` (start
  page greater than end page) matched the range regex but the `for (let i =
  start; i <= end; i++)` loop never executed, so that part of the input
  silently contributed zero pages instead of erroring or extracting anything.
  If it was the only range entered, the user got a generic "Enter at least
  one page" error despite having typed a page range; if combined with other
  parts (e.g. `"5-3, 2"`), the backwards range was dropped with no
  indication anything was wrong. Fixed by swapping `start`/`end` when
  `start > end`, so a backwards range is treated the same as the forwards
  version (matching what a user almost certainly meant — a typo'd order, not
  an intentionally empty range). Verified with `node -c` (syntax) and a
  standalone test of the function covering `"5-3"`, `"3-5"`, `"5-3, 2"`, and
  a plain comma list — backwards and forwards ranges now produce identical
  output. Did not find anything worth logging from passive research this
  run. Notional cost $3.00, remaining $1.00 (see BUDGET.md). Per the
  strategy rules, once remaining hits $0 the next run will write a
  postmortem for Strategy 01 instead of continuing to iterate on it.

- **2026-09-09 (2)**: Found and fixed a memory-leak bug in the Compress
  tool: `compressOne()` called `URL.createObjectURL(file)` to load each
  image into an `<img>` element for canvas re-encoding, but never called
  `URL.revokeObjectURL()` on it. Every compressed image (and every retry)
  permanently pinned a blob in memory for the rest of the page's life —
  compressing a batch of 20+ images in one session would leak 20+ blob
  URLs. Fixed by revoking the object URL in both the `onload` and
  `onerror` handlers, right after the browser has decoded (or failed to
  decode) the image — safe because the `<img>` retains the decoded bitmap
  independently of the URL once loaded. Verified by re-reading the full
  function and syntax-checking the file (`node -c app.js`); no other
  `createObjectURL` call in the file was missing its matching revoke.
  Notional cost $3.00, remaining $4.00 (see BUDGET.md).
  - **Passive market research**: searched for how the free-PDF-tool
    landscape looks in 2026. Genuinely client-side, no-signup competitors
    exist (e.g. PDFFixy advertises the same "processed entirely in your
    browser, nothing uploaded" pitch Deskline uses), so "no upload" is
    becoming table stakes rather than a unique differentiator — it's still
    worth keeping front and center, but it alone won't be enough to stand
    out once/if this gets any real traffic. No new build work from this;
    logging for future strategy thinking.

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

**Update, 2026-09-09**: this run's scheduled push to both `deskline-tools`
and `income-agent-log` succeeded without any 403 — direct evidence the
GitHub access problem below is fixed. Leaving the original note intact for
the record, but the routine no longer needs to stay paused on this specific
concern; the user should still do their own final check before flipping it
back to unattended per the original ask.

**## AWAITING USER** (original note, 2026-09-08 — access issue below now
looks resolved per the update just above, but leaving this for the user to
close out explicitly): Please check the Claude GitHub App installation at
https://github.com/apps/claude/installations/select_target and confirm it
has access to both `jamar-clarke/deskline-tools` and
`jamar-clarke/income-agent-log` (either select them explicitly, or choose
"All repositories"). The routine is **paused** (enabled: false) until this
is confirmed, so it doesn't keep failing silently (locally) once a day and
sending push notifications about blocked runs. Once fixed, ask Claude to
re-enable the routine and it will re-verify with a test run before leaving
it unattended again.

## Postmortems

### Strategy 01: Deskline Tools (client-side PDF/image toolkit) — 2026-09-11

**Budget**: $50.00 notional, spent $53.00 over 9 sessions (2026-09-08 to
2026-09-10). Final remaining: **-$3.00**.

**What was actually built and shipped**: A real, working, free, no-upload,
no-signup client-side toolkit — merge PDF, split PDF (range + split-to-zip),
compress image, images→PDF — live at https://desklinetools.github.io/,
deployed on GitHub Pages under its own org for a clean domain. Five genuine
bugs were found and fixed over the course of the strategy (missing
drag/keyboard reorder in Merge and later Images→PDF despite help text
promising it, transparent PNGs turning solid black on compress, a blob URL
leak in Compress, and the Split tool silently dropping backwards page
ranges like "5-3"). Basic technical SEO was added (OG/Twitter tags,
JSON-LD, sitemap.xml, robots.txt), and a tip-jar link was wired into the
header. Six outreach/submission drafts were written (Show HN, r/SideProject,
r/InternetIsBeautiful, r/webdev Showoff Saturday, a free-for.dev PR, an
AlternativeTo listing) for the user to review and post themselves.

**Correction to the log**: earlier entries above (2026-09-09/10) list the
tip link as an "open item... waiting on the user's tip-jar URL." That's
stale — commit `c5c466c` ("Wire up the tip jar link", 2026-09-09) actually
wired it to `https://ko-fi.com/desklinetools`, and it's live in
`index.html` today. The open item was never updated to reflect that it
closed. Noting this here for an honest record; not treating it as new work
since it was already done.

**Real, measurable outcome**: **zero.** Zero confirmed visits, zero tip
revenue, zero signups (not applicable by design), zero external mentions.
This isn't "results were disappointing" — there is genuinely no data
either way, because:
- None of the six outreach drafts were ever posted anywhere (correctly —
  posting to third-party platforms is outside this agent's authorized
  scope without the user's explicit action). No evidence in either repo
  that the user posted them either.
- No analytics or traffic measurement of any kind was ever added to the
  site — not even GitHub's own built-in repo Traffic insights (visits/
  unique visitors/referrers), which needs no new account and would have
  been free to check. So even the one channel that *is* in scope (the live
  public URL existing at all, indexed by search engines via the sitemap)
  was never actually checked for organic hits.
- The product itself was never at fault in any bug report, review, or
  complaint, because none exist — there's no channel through which any
  would have reached this log.

**Genuine lessons learned**:
1. A well-built, well-tested, genuinely working free tool produces exactly
   zero measurable outcome without *some* distribution channel, and the
   two channels that would normally bootstrap a brand-new tool (social/
   forum posts, directory submissions) both require actions — creating
   accounts, posting as the user, agreeing to platform ToS — that this
   agent is correctly barred from doing autonomously. That's a structural
   ceiling on this strategy shape, not a one-off gap: it can get a product
   to "ready to be seen" but not to "seen."
2. Effort drifted toward what was easy and safe to keep doing (bug fixes,
   SEO metadata, code quality) rather than the actual bottleneck
   (distribution and measurement). The last few sessions fixed
   increasingly minor edge cases (a blob URL leak, a backwards page-range
   parser bug) on a product with confirmed-zero traffic — real fixes, but
   low-value ones given nobody was hitting those paths yet.
3. Never instrumenting even free, no-account-needed measurement (GitHub
   Pages' own Traffic tab) was a mistake — it means this postmortem can't
   even say "nobody visited," only "we don't know." Any future strategy
   should add the cheapest available measurement on day one, before
   polishing.
4. Passive market research (logged 2026-09-09, 2026-09-10) found the
   client-side/no-upload PDF-tool niche is real but increasingly crowded
   (ClientPDF, RaptorPDF, PDFFixy, Bontello, and others already claim the
   same "nothing uploaded" pitch, some with far more tools). A brand-new,
   unpromoted entrant has a weak organic path to visibility in a category
   Google already ranks heavily, on a domain with zero age or backlinks.
5. The $50 notional-budget mechanism worked exactly as designed — it
   forced a stop instead of open-ended polishing once diminishing returns
   set in, and it's the reason this postmortem exists instead of a tenth
   small bug-fix commit.

## Proposed next strategy (awaiting review)

Both ideas below directly target the lesson from Strategy 01: pick
something where the agent's own in-scope, no-account actions (writing
code, basic on-page SEO, optionally checking GitHub's built-in repo
Traffic tab) have a plausible path to organic discovery, instead of
depending on distribution actions the agent isn't authorized to take.
Neither has been built, scaffolded, or deployed — proposing only.

**Idea A — Small developer text/data utilities** (JSON formatter +
validator, regex tester, diff checker, timestamp/unit converters), same
static/client-side/no-upload/no-signup ethos as Deskline. Rationale:
technical searchers (developers debugging something at 2am) search for and
click *very* specific long-tail queries ("json formatter online free",
"regex tester javascript"), and technical audiences routinely link such
tools directly in Stack Overflow answers, GitHub issues, and blog posts —
a form of organic distribution that happens *because* the tool is useful,
without the agent needing to post anywhere itself. Each micro-tool is an
independent SEO target, so the idea can be tested incrementally (ship one
tool, see if GitHub Pages Traffic shows any pickup, before building the
next) rather than needing a full suite before getting any signal.

**Idea B — Small business document generator** (free invoice / receipt /
quote generator, client-side PDF output, no account, no watermark).
Rationale: different search intent than either PDF-utility or dev-tool
niches (small-business owners, freelancers), plausibly less saturated by
big-budget SaaS competitors than the "PDF toolkit" or "dev tools" spaces
already are, and has natural repeat use (someone who generates one invoice
this month plausibly comes back next month) rather than Deskline's
mostly one-off usage pattern.

Either way, whichever strategy the user greenlights should have basic,
free, no-new-account measurement (GitHub Pages Traffic insights, checked
periodically) wired in from day one — not treated as a later nice-to-have.

## Strategy 02: Devline Kit (developer micro-tools)

- **2026-09-11 — user greenlit Idea A.** Built out in this interactive
  session, per the routine's own instruction that strategy pivots need
  human review before build-out.
- **Idea**: free, no-signup, no-upload client-side developer utilities —
  JSON formatter/validator, regex tester, diff checker, Unix timestamp
  converter. Same ethos as Deskline (nothing leaves the browser), aimed at
  a different, hopefully less saturated distribution path: technical
  searchers and organic links from Stack Overflow/GitHub answers rather
  than needing forum/directory submissions.
- **Naming**: intended to call it `devlinetools` (a clean echo of
  `desklinetools`), but GitHub rejected that name as unavailable even
  though it wasn't visible via the public users API — used `devlinekit`
  instead. New free GitHub org, own identity from Deskline (so a Strategy
  01 shutdown doesn't affect Strategy 02, and vice versa).
- **Stack**: static HTML/CSS/JS, zero dependencies (no CDN libraries needed
  for any of the four tools), GitHub Pages hosting at
  `github.com/devlinekit/devlinekit.github.io`, live at
  **https://devlinekit.github.io/**.
- **Verification**: all four tools were run end-to-end in a real Chrome
  browser (via a local static server) before pushing, not just
  eyeballed — this caught one real bug (JSON validator was appending its
  own computed "line, column" after V8's error message, which on current
  Chrome already includes that, producing a duplicate). Fixed and
  re-verified before commit.
- **Applying Strategy 01's lesson on measurement**: GitHub Pages' built-in
  Traffic tab (visits/uniques/referrers) is free and needs no new account —
  this should be checked periodically going forward (e.g. by the daily
  routine) instead of never looking, which is what actually happened last
  time.
- **Monetization**: same Ko-fi tip link reused from Deskline
  (https://ko-fi.com/desklinetools) — user chose to reuse rather than
  create a second account, since it's free to add a second product's
  audience to the same tip jar.
- **Daily routine updated**: the routine's sources and prompt (previously
  hard-coded to Strategy 01 / desklinetools.github.io) were updated to
  point at `income-agent-log` + `devlinekit.github.io` and describe the
  Devline Kit product, so tomorrow's scheduled run maintains the current
  strategy instead of the retired one.
- **Open risk, not yet confirmed**: when the `desklinetools` org was
  created (2026-09-09), the routine needed the Claude GitHub App granted
  access to that org separately before it could push there — this was the
  2026-09-08 push-403 incident. The same may well be true for the new
  `devlinekit` org; it hasn't been tested yet since the routine's sources
  only just changed. If tomorrow's scheduled run (2026-09-12) fails to
  push with a 403, that's the likely cause — check
  https://github.com/apps/claude/installations/select_target for the
  `devlinekit` org's access the same way it was fixed for `desklinetools`.
