# CLAUDE.md

Guidance for Claude Code working in this repo.

## What this repo is

A personal learning project on **trunk-based development (TBD)**. It is *not* an app —
it's a curriculum: Markdown working docs plus self-contained HTML lessons, published to
GitHub Pages at https://roytanaka.github.io/git-workflows/.

## The learner (audience for everything you write)

- **Role:** solo human **director / reviewer / release manager** — *not* the committer.
  In their real project, Claude Code does the implementation, commits, and PRs.
- **Therefore:** teach **judgment** — branch lifetime, PR size, releasability, release
  strategy — *not* git CLI incantations. Lessons should frame decisions as "as the
  reviewer, you decide X."
- **Background:** has used Git loosely, no formal flow (no GitFlow/GitHub-flow/TBD prior).
  Start from the mental model; don't assume flow vocabulary.
- **Context:** greenfield web app / SaaS, continuously deployed, per-PR preview deploys
  (Vercel/Netlify-style) as the review surface. Keep examples concrete to *this* setup.

See [`MISSION.md`](MISSION.md), [`NOTES.md`](NOTES.md), and
[`learning-records/`](learning-records/) for the authoritative context — read them before
writing or revising lessons.

## Authoring conventions

- **Lessons** live in [`lessons/`](lessons/), numbered `NNNN-kebab-title.html`.
  **Reference** material lives in [`reference/`](reference/).
- Pages are **self-contained HTML** with inline `<style>` — no build step, no external CSS/JS
  dependencies. Match the existing palette and structure (see `lessons/0001-*.html`).
- When you add a lesson or reference page, **add a matching card to [`index.html`](index.html)**
  so it appears on the published site, and update the roadmap in [`NOTES.md`](NOTES.md).
- Cite claims to the verified sources in [`RESOURCES.md`](RESOURCES.md). If you rely on a new
  source, fetch/verify it and add it there with a one-line note on what it's good for.

## Working in the repo

- `main` is the only branch and is published directly by GitHub Pages — pushes go live in ~1 min.
- `.claude/settings.local.json` is gitignored (local-only). Don't commit machine-local config.
- The repo is **public**. Don't commit anything you wouldn't publish.

## Commit messages

Per the user's global preference: **do not** add a `Co-Authored-By: Claude` trailer.
