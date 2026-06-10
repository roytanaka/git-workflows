# Flags as the long-branch replacement: types, the wrapper, debt, the ladder

**Taught in:** Lesson 0006 — Hiding Work Behind Flags (2026-06-09).

This is the "what the learner now has" consolidation for Lesson 6. The forward-looking *tooling decision* it rests on was made earlier — see [[0003-feature-flag-tooling-decision]]; this record captures what actually landed in the lesson.

## What the learner now has
- **The flag is the move you make *instead of* a long-lived branch.** A long branch and a feature flag solve the same problem — "this isn't ready to show anyone" — but only the flag is compatible with everything in Lessons 1–5 (small PRs, daily integration, an always-releasable trunk, deploy≠release). So when a feature is too big for one reviewable PR, the director's instruction is **"land it in pieces behind a flag,"** never "keep working on a branch." This is the mechanism that pays off Lesson 5's deploy≠release promise.
- **Four toggle types, sorted by lifespan** (Hodgson/Fowler taxonomy): *release* (hides in-progress work; days–weeks, remove after launch) and *experiment* (A/B or % split to decide; lives for the test, then remove) are **temporary scaffolding** → candidates for debt. *Ops* (kill switch / circuit breaker; long-lived, sometimes permanent) and *permissioning* (plan/user gate — a product rule in flag's clothing; permanent) are **legitimately long-lived → not debt**. Same mechanism, opposite removal expectations.
- **The one architecture rule: own the wrapper.** Every flag check goes through a thin team-owned `FlagClient`; the vendor's name appears in exactly one file behind it. This is the fix for the AI-committer failure mode where an agent scatters `posthog.isFeatureEnabled(...)` across components and welds the codebase to a vendor. Payoff: swappable backend (even vendor→env-var), one place to force **default-off** (a missing flag can't expose unfinished work), trivially testable off-state. Costs the director one line in the brief — the same "set the boundary in the instruction before code exists" skill as scoping in Lesson 3.
- **Flag-debt discipline.** A temporary flag gets an **owner + a removal date at the moment it's created**, and the **cleanup PR that deletes the flag and the dead `if` branch is part of the definition of done** (a `chore:`/`refactor:` PR in Lesson 5's vocabulary). Review tells: a PR adding a flag for a feature that shipped weeks ago, or a flag with no owner/removal date — both are debt created in front of you; the fix is one sentence asking when it comes out and who owns it. Ops/permissioning are exempt.
- **The decision ladder (when *not* to reach for a vendor).** Rung 1 = **env var / config toggle** (deploy-time flip, no targeting/measurement) — the default, and the rung agents skip past. Rung 2 = **a flag service** the moment you need any of: runtime flip without deploy, % rollout, plan/user targeting, a real kill switch, or an experiment. Director's move: **default new "hide this" requests to rung 1 and make the agent prove it needs rung 2.** Because everything sits behind `FlagClient`, the choice is a reversible one-file change, not a vendor marriage.

## Decision recorded
- No *new* user decision was made in this lesson. The tooling call it builds on (wrapper-first; **PostHog** as the rung-2 pick; Vercel Flags SDK / LaunchDarkly / GrowthBook+Unleash / Statsig as the when-*not*-to options) was made on 2026-06-09 and is recorded in [[0003-feature-flag-tooling-decision]]. Lesson 6 taught that decision rather than re-opening it.

## Connections
- Pays off the deploy≠release decoupling from [[0005-releases-and-commit-convention]] — flags are the mechanism that makes "release" a separate flip from "deploy."
- Realizes the plan in [[0003-feature-flag-tooling-decision]] (wrapper + flag-debt + rung ladder).
- The `FlagClient`-in-the-brief move is the same architectural-boundary-in-the-instruction skill as task scoping in [[0002-reviewable-pr-and-task-scoping]].
- "Hidden work stays hidden / flag off by default" is checklist item 6 from [[0004-preview-deploy-review-surface]] — the preview is where the director verifies the flag is actually dark.

## Next zone of proximal development
- **Lesson 7 — Hotfixes** (roll-forward vs cherry-pick). Lesson 6's closing question already plants the bridge: when a *flagged* feature has a production bug, is the fix still just roll-forward (Lesson 5)? The fastest mitigation for a flagged feature is often flipping the flag off (an ops-toggle instinct), before any code fix.
- Likely learner asks surfaced in the lesson's "ask your teacher": the exact **brief line** that puts a feature behind `FlagClient` with owner + removal date; a real `FlagClient` that starts as an env var and later swaps to PostHog without touching call sites; how to **track open flags** so an overdue one gets noticed.
