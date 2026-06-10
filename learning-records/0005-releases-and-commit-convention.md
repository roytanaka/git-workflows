# Releases from trunk + the lightweight commit convention

**Taught in:** Lesson 0005 — Shipping From the Trunk (2026-06-09).

## What the learner now has
- **Deploy ≠ release.** Two independently-controlled events: *deploy* = code running on production infra (automatic on every merge to `main`), *release* = users can see/use it (a separate decision, usually a feature-flag flip). This decoupling is what lets unfinished work deploy to production yet stay dark — the bridge into Lesson 6 (flags).
- **The two release models as a genuine fork:** *release from trunk* (production = latest trunk, no release branch, roll forward on bugs) vs *branch for release* (cut `release/x.y`, harden, cherry-pick fixes). The learner's default is **release from trunk** — grounded in their setup (one always-live SaaS, no user-installed versions, high cadence). The **only** trigger to switch is owing ongoing support to a specific shipped version you can't roll forward (e.g. an enterprise customer pinned to v2.0).
- **The roll-forward rule:** fixes always flow trunk → production, never patched sideways; even when branching for release you fix on trunk first, then cherry-pick. (Full hotfix treatment deferred to Lesson 7.)
- **The release manager's shrunk job:** not "do a release" but keep trunk releasable + decide when to flip a feature on. Heavier machinery (branches, back-ports) only when a version-to-support forces it.

## Decision recorded (user's call, 2026-06-09)
- **Adopt: lightweight Conventional Commits** — squash-merge every PR; the **PR title** is a Conventional Commit (`feat:`/`fix:`/`chore:` + one imperative line) and becomes the single trunk commit. Rationale: squash-merge makes the PR title the permanent trunk message (GitHub default), so a typed title buys a skimmable history + a free on-ramp to release notes at near-zero cost (agents write it from the brief, like the no-`Co-Authored-By` rule).
- **Reject (for now): full semantic-release / auto-versioning** (auto version bumps + generated `CHANGELOG.md`). Muted value for a single always-live SaaS with no installed versions; revisit only if a published changelog becomes a real need.
- **Declined for now:** a printable release reference card (lesson only). Easy to add later.

## Connections
- Builds on [[0004-preview-deploy-review-surface]] (three review signals → "is this trunk state one I'm happy to have live?").
- The deploy≠release decoupling is the setup for [[0003-feature-flag-tooling-decision]] — flags are the mechanism that makes "release" a separate flip. Lesson 6 next.
- The roll-forward / fix-on-trunk-first rule is the seed for Lesson 7 (hotfixes: fix-forward vs cherry-pick).

## Next zone of proximal development
- **Lesson 6 — Feature flags** (plan locked in [[0003-feature-flag-tooling-decision]]; now doubly motivated by §1's deploy≠release framing).
- **Lesson 7 — Hotfixes** (roll-forward vs cherry-pick; §3 already planted the rule).
- Possible learner ask: the exact **brief line** instructing an agent to title PRs as Conventional Commits (overlaps the brief-template idea floated in Lessons 3–4).
