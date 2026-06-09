# Trunk-Based Development Resources

All URLs below were fetched and verified live on 2026-06-09.

## Knowledge

- [trunkbaseddevelopment.com — Paul Hammant](https://trunkbaseddevelopment.com/)
  The canonical TBD reference. Defines the trunk, short-lived feature branches, "small team" (commit straight to trunk) vs "scaled" (short-lived branch + review) TBD, release branches cut just-in-time from trunk, and fix-forward vs cherry-pick. **Primary spine for the whole curriculum.**
  - Key sub-pages: [/short-lived-feature-branches/](https://trunkbaseddevelopment.com/short-lived-feature-branches/), [/branch-for-release/](https://trunkbaseddevelopment.com/branch-for-release/), [/release-from-trunk/](https://trunkbaseddevelopment.com/release-from-trunk/).
- [DORA — Trunk-based development capability](https://dora.dev/capabilities/trunk-based-development/)
  Google's DevOps research. The evidence that TBD *predicts* higher delivery performance. Concrete thresholds: ≤3 active branches, merge to trunk at least daily, no code freezes / integration phases, branches live hours not days. Use for: "why TBD, not just how."
  - Underlying book: *Accelerate* — Forsgren, Humble, Kim (IT Revolution, 2018).
- [Martin Fowler — Patterns for Managing Source Code Branches](https://martinfowler.com/articles/branching-patterns.html)
  Rigorous pattern catalog: mainline, healthy branch, integration frequency, feature-branching-vs-CI tension, release branch. Use for: precise definitions and trade-off framing.
- [Martin Fowler — Continuous Integration](https://martinfowler.com/articles/continuousIntegration.html)
  The practice TBD operationalizes: everyone integrates to mainline at least daily, automated self-testing build. Use for: *why* branches must stay short.
- [Feature Toggles (a.k.a. Feature Flags) — Pete Hodgson, on martinfowler.com](https://martinfowler.com/articles/feature-toggles.html)
  Canonical taxonomy (release, experiment, ops, permissioning toggles) and managing toggle debt. The mechanism for hiding incomplete work on trunk. Use for: the releases/flags lessons.
- [Vercel — Environments & Preview Deployments](https://vercel.com/docs/deployments/environments)
  How a push to a non-production branch or a PR auto-creates a preview deployment with its own URL. Use for: the preview-deploy-as-review-surface lesson. (Netlify equivalent: [Deploy Previews](https://docs.netlify.com/site-deploys/deploy-previews/).)
- [GitHub — About protected branches](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches)
  Every branch-protection setting (require PR, status checks, up-to-date, reviews, conversation resolution, no bypass/force-push). Use for: day-one repo setup.
- [GitHub — About rulesets](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/about-rulesets)
  The modern, layerable form of branch protection. Use for: how to actually apply the day-one gate.
- [GitHub — Managing a merge queue](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/configuring-pull-request-merges/managing-a-merge-queue)
  Batches ready PRs, re-tests them combined against latest base, merges only what passes together. Use for: many-PRs-per-day concurrency and logical conflicts.
- [SmartBear — Best Practices for Peer Code Review](https://smartbear.com/learn/code-review/best-practices-for-peer-code-review/)
  Summarizes the Cisco study (the largest code-review study run): a reviewer is effective up to ~200–400 LOC in a 60–90 min sitting, yielding 70–90% defect detection; detection collapses above ~500 LOC/hr. **The hard number behind "keep PRs small"** — use for the reviewable-PR and review-quality lessons.
- [Do Small Code Changes Merge Faster? (arXiv 2203.05045)](https://arxiv.org/pdf/2203.05045)
  Multi-language empirical study confirming smaller changes merge faster. Pair with [LinearB — the PR paradox](https://linearb.io/blog/the-pull-request-paradox-merge-faster-by-promoting-your-pr) on smaller PRs reviewing/merging faster and reverting more easily. Use for: the downstream payoff of small PRs.

## Wisdom (Communities)

- [DORA community](https://dora.community/) — research-grounded DevOps practitioners; best for "is our TBD setup sane?" discussion.
- [r/ExperiencedDevs](https://www.reddit.com/r/ExperiencedDevs/) — higher-signal branching-strategy trade-off threads.
- [r/git](https://www.reddit.com/r/git/) — mechanics of branching, cherry-picking, rebasing when you need the how.

## Gaps
- No source yet specific to **AI-agent-driven** TBD (humans reviewing, agents committing). This is an emerging area; for now we adapt scaled-TBD review practices. Worth revisiting as material appears.
- The Cisco/SmartBear review-ceiling numbers come from human-reviewer studies; whether the same ceiling holds when the *committer* is an AI (and the reviewer reads AI-generated diffs) is untested. Treating the human limit as the binding constraint is the conservative call.
