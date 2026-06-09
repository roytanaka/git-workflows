# Preview deploys as the primary review surface

**Taught in:** Lesson 0004 — The Preview Deploy as Your Review Surface (2026-06-09).

## What the learner now has
- **The three review signals** as independent proofs, each showing something different: **CI** (builds + tests pass = internal consistency), **the diff** (the approach — Lesson 3's S·S·S), **the preview deploy** (the change actually *behaves*). Approving = all three green. The preview is the one most reviewers skip and the only one that proves behavior — framed sharply for AI committers, where a clean diff + passing tests can still hide broken UX.
- **What a preview deploy is** (grounded in verified Vercel docs): auto-created on every non-prod branch push / PR, its own generated URL that updates per commit, isolated environment with its own env vars/data (so clicking around — even destructive edge cases — can't touch production), and surfaced as a link on the GitHub PR.
- **A repeatable preview checklist:** does-the-claimed-thing (uses the PR's "what to check" line) · happy path end-to-end · edge/empty/error states · nearby regressions · mobile width · hidden-work-stays-hidden (flag is off by default).
- **The reviewer's move:** preview wrong → request changes / send back, never approve unseen behavior or "merge to fix later" onto a releasable trunk.
- **First feature-flag seed:** checklist item 6 + quiz Q4 introduce "incomplete work behind a flag, confirm it's off on the preview." One-line only; full treatment deferred to Lesson 6 (see [[0003-feature-flag-tooling-decision]]).

## Connections
- Directly builds on [[0002-reviewable-pr-and-task-scoping]]: the "self-describing → what to check on the preview" line from Lesson 3 is now the entry point to the checklist; single-purpose PRs make "check nearby" cheap.

## Next zone of proximal development
- **Lesson 5 — Releases** (teased in the lesson): once a PR merges to trunk, how does it actually ship? release-from-trunk vs release branches; continuous deployment. This is a core mission success criterion still uncovered.
- **Lesson 6 — Feature flags** is now seeded and its plan is locked in [[0003-feature-flag-tooling-decision]].
- Possible learner ask: a PR-description template tuned to make previews easy to review (overlaps the brief-template idea from Lesson 3).
