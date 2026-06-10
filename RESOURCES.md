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

### Feature-flag tooling (for Lesson 6)
- [PostHog — Feature flags docs](https://posthog.com/docs/feature-flags) & [pricing](https://posthog.com/pricing)
  All-in-one: flags + product analytics + session replay + experiments. Supports boolean release toggles, % rollout, user/group targeting, kill-switches, server-side local evaluation, client bootstrap (no flicker). ~1M flag requests/mo free; open-source/self-host (MIT) escape hatch; SDKs for most languages. **Recommended concrete example for the flags lesson** — best single-tool bet for a greenfield SaaS.
- [Vercel Flags SDK](https://vercel.com/docs/flags) ([flags-sdk.dev](https://flags-sdk.dev/))
  Free, open-source, *provider-agnostic* "flags as code" library; framework-native for Next.js; flags evaluated server-side; can use PostHog as its backing provider. Use for: the lightest option on a Vercel stack, and to show flags aren't necessarily a separate vendor.
- [Feature flags in AI-generated code — LeadWise](https://www.leadwise.pro/en/blog/statsig-posthog-and-launchdarkly-feature-flag-choices-in-ai-generated-code)
  **Most mission-relevant flags source.** Argues AI agents default to a vendor SDK even when an env-var/config toggle would do; the fix is a thin team-owned `FlagClient` wrapper ("put this behind our FlagClient") plus a cleanup discipline (every flag needs an owner + removal date). Use for: the director's judgment angle of the flags lesson.
- [Best feature-flag software, compared — PostHog](https://posthog.com/blog/best-feature-flag-software-for-developers)
  Landscape survey: PostHog / Vercel / LaunchDarkly (enterprise/governance) / GrowthBook + Unleash (OSS self-host) / Statsig (unlimited free flags, now OpenAI-owned). Use for: framing the options and when *not* to reach for a vendor.
- [Vercel — Environments & Preview Deployments](https://vercel.com/docs/deployments/environments)
  How a push to a non-production branch or a PR auto-creates a preview deployment with its own URL. Use for: the preview-deploy-as-review-surface lesson. (Netlify equivalent: [Deploy Previews](https://docs.netlify.com/site-deploys/deploy-previews/).)
- [GitHub — About protected branches](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches)
  Every branch-protection setting (require PR, status checks, up-to-date, reviews, conversation resolution, no bypass/force-push). Use for: day-one repo setup.
- [GitHub — About rulesets](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/about-rulesets)
  The modern, layerable form of branch protection. Use for: how to actually apply the day-one gate.
- [GitHub — Managing a merge queue](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/configuring-pull-request-merges/managing-a-merge-queue)
  Batches ready PRs, re-tests them combined against latest base, merges only what passes together. Use for: many-PRs-per-day concurrency and logical conflicts.

### Releases & commit conventions (for Lesson 5)
- [trunkbaseddevelopment.com — Release from Trunk](https://trunkbaseddevelopment.com/release-from-trunk/) & [Branch for Release](https://trunkbaseddevelopment.com/branch-for-release/)
  The two release models and when each applies. Verified quotes: very-high-cadence teams "do not need (and cannot use) release branches at all" and "roll forward and fix the bug on the trunk as if it were a feature"; branch-for-release is "only when necessary… late, and instead of freeze," with fixes made on trunk first then cherry-picked (never the reverse). Use for: the release-from-trunk vs branch-for-release fork and the roll-forward rule.
- [GitHub — About pull request merges](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/incorporating-changes-from-a-pull-request/about-pull-request-merges)
  Squash-and-merge combines a PR's commits into one; the default commit message comes from the **PR title** (when the PR has >1 commit). The grounding for "the PR title *is* your trunk history." Use for: the squash-merge + PR-title-convention argument.
- [Conventional Commits 1.0.0](https://www.conventionalcommits.org/en/v1.0.0/)
  Spec: `<type>[optional scope]: <description>`; `feat`→MINOR, `fix`→PATCH, `!`/`BREAKING CHANGE`→MAJOR; other types (`chore`, `docs`, `refactor`, `perf`, `test`) optional. Use for: the lightweight PR-title convention. **Decision (learning-record 0005):** adopt the convention (squash-merge + Conventional PR titles), *not* the semantic-release/auto-versioning machinery — muted value for a single always-live SaaS with no installed versions.
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
