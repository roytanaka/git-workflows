# Working Notes

## Learner context (from kickoff 2026-06-09)
- **Role in the workflow:** Solo human director. Claude Code (AI) does all implementation, commits, and PRs. → Teach *judgment, review, and release decisions*, not git CLI memorization.
- **Project:** Greenfield web app / SaaS, continuously deployed.
- **Preview model:** Per-PR preview deploys (Vercel/Netlify-style) — this is the learner's review surface.
- **Prior knowledge:** Has used Git "loosely," never a formal flow (no GitFlow / GitHub-flow background). Start from mental model.

## Teaching preferences
- Mission says: focus on judgment over CLI incantations. Frame lessons around "as the reviewer/release manager, you decide X."
- Lessons should be concrete to *their* project (web app, AI committers, preview deploys), not generic.

## Learner's stated extra interest (2026-06-09)
- Wants to understand **multiple AI agents working multiple features simultaneously, all pushing PRs in one day.** Folded into lesson 2 (parallel branches + merge queue + logical conflicts). Likely wants a future lesson on *partitioning work across agents* so branches don't collide.

## Curriculum roadmap (provisional)
1. ✅ The Trunk and the Loop — core mental model (lesson 0001)
2. ✅ Protecting the Trunk for Parallel Agents — day-one branch protection + merge queue + logical conflicts (lesson 0002)
3. ✅ The Reviewable Pull Request — S·S·S (small/single-purpose/self-describing), the Cisco review ceiling, triage (review/split/send-back), scoping the brief, and slicing work across agents (lesson 0003).
4. ✅ The Preview Deploy as Your Review Surface — three review signals (CI / diff / preview), what a preview is, and a checklist of what to do on the preview URL before approving (lesson 0004). One-line feature-flag mention seeded here (checklist item 6).
5. ✅ Shipping From the Trunk — deploy ≠ release (decoupled via flags); release-from-trunk vs branch-for-release (your default = release from trunk; the *only* switch trigger is a version you must support); the roll-forward rule; and the lightweight commit convention (lesson 0005). **Convention decision (user, 2026-06-09):** adopt squash-merge + Conventional-Commit *PR titles* (`feat:`/`fix:`/`chore:`); **not** semantic-release/auto-versioning. Recorded in learning-record 0005.
6. ✅ Hiding Work Behind Flags — the flag as the replacement for a long-lived branch; the four toggle types (release/experiment/ops/permissioning) and their lifespans; the team-owned `FlagClient` wrapper (one line in the brief, agents otherwise scatter the vendor SDK); flag-debt discipline (owner + removal date, cleanup PR is part of "done"); and the rung-1-vs-rung-2 decision ladder (env-var config toggle by default → **PostHog** when you need runtime flip / % rollout / targeting / kill switch / experiment; Vercel Flags SDK / LaunchDarkly / GrowthBook+Unleash / Statsig mentioned as the when-*not*-to options). Plan was locked in learning-record 0003 (lesson 0006).
7. ✅ When Production Breaks — a hotfix as the roll-forward rule under a stopwatch; the **two clocks** (mitigation = stop the bleed fast / remediation = fix the cause calmly on trunk); the flag **kill switch** as fastest, code-free mitigation (pays off Lesson 6's ops toggle); **revert-on-trunk as roll-forward** (a new commit forward, not a redeploy-old-build rollback — GitHub Revert creates a new PR reverting the merge commit); the **four-rung decision ladder** (flag off → revert on trunk → roll forward a fix → cherry-pick to a release branch for the rare supported-version case); reviewing under fire (mitigate first so the fix PR keeps the three-signal bar) and the GitFlow `hotfix/` branch you're *not* cutting (lesson 0007). **Closes the core curriculum path.** New verified source added to RESOURCES: GitHub Docs — Reverting a pull request.

### Possible next lessons (post-core)
- **Partitioning work across agents** so parallel PRs never collide (the learner's early stated interest, 2026-06-09; seeded in Lessons 2–3, flagged again in Lesson 7's closing asks).
- **Detecting** production bugs: monitoring/alerting for a greenfield SaaS (Lesson 7 assumes you *notice* the break).
- **Blameless incident retro** — what the post-fire review should produce.
