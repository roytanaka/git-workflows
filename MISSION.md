# Mission: Trunk-Based Development

## Why
I'm starting a greenfield web app (SaaS) and want the Git workflow right from commit #1, instead of the loose, ad-hoc Git habits I've used before. The twist: **I direct the work, but Claude Code does the implementation, commits, and PRs.** So my real job is to run a clean trunk-based workflow as the *reviewer and release manager* — keeping `main` always releasable and deciding what ships.

## Success looks like
- I can draw and explain the core TBD loop (branch → PR → preview deploy → review → merge → delete) and why branches stay short-lived.
- I can set up a greenfield repo on day one with the right branch protection, so AI-produced work flows through small PRs onto a trunk that's always deployable.
- I know how releases work in a continuously-deployed web app under TBD (release-from-trunk vs. release branches) and can pick the right one for my project.
- I understand per-PR preview deployments and use them as my primary review surface.
- I can hide incomplete work on trunk with feature flags instead of long-lived branches.

## Constraints
- Solo human; AI agents do the hands-on Git work. Lessons should focus on *judgment and review*, not on me memorizing git CLI incantations.
- New to formal Git flows entirely — start from the mental model, don't assume GitFlow/GitHub-flow knowledge.
- Stack leans modern web (per-PR preview deploys, e.g. Vercel/Netlify-style).

## Out of scope (for now)
- GitFlow and other heavyweight branching models (only as a contrast, not to adopt).
- Monorepo-specific tooling and release orchestration.
- Deep git-internals (rebase strategy, reflog surgery) beyond what review/release needs.
