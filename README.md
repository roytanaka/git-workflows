# Trunk-Based Development — Learning Path

A personal learning project for getting the Git workflow right from commit #1 on a
greenfield, continuously-deployed SaaS app — where **I direct the work and review it,
and Claude Code does the implementation, commits, and PRs.** The focus is *judgment,
review, and release decisions* as the trunk's reviewer and release manager, not git CLI
memorization.

📖 **Read it as a site:** https://roytanaka.github.io/git-workflows/

## What's here

| Path | What it is |
|------|------------|
| [`MISSION.md`](MISSION.md) | Why this exists, what success looks like, scope. |
| [`NOTES.md`](NOTES.md) | Working notes, learner context, and the curriculum roadmap. |
| [`RESOURCES.md`](RESOURCES.md) | Curated, link-verified TBD references (trunkbaseddevelopment.com, DORA, Fowler, GitHub docs). |
| [`lessons/`](lessons/) | The lessons, as self-contained HTML pages. |
| [`reference/`](reference/) | Quick-reference material (day-one checklist, glossary). |
| [`learning-records/`](learning-records/) | Captured facts about the learner that shape how lessons are written. |
| [`index.html`](index.html) | Landing page for the published site. |

## Lessons

1. [The Trunk and the Loop](lessons/0001-the-trunk-and-the-loop.html) — the core TBD loop
   (branch → PR → preview deploy → review → merge → delete) and why branches stay short-lived.
2. [Protecting the Trunk for Parallel Agents](lessons/0002-protecting-the-trunk-for-parallel-agents.html) —
   day-one branch protection, merge queues, and logical conflicts when multiple agents ship in one day.

See [`NOTES.md`](NOTES.md) for the full provisional roadmap (reviewable PRs, preview deploys,
releases, feature flags, hotfixes).

## Publishing

The site is served by GitHub Pages from `main` (root). Every push to `main` rebuilds it
(~1 min). Lessons and reference pages are plain, dependency-free HTML.
