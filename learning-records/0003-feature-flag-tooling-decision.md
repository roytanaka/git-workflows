# Feature-flag tooling: wrapper-first, PostHog as the concrete pick

**Decided:** 2026-06-09, in response to the learner asking to evaluate flag options "including PostHog." Feeds Lesson 6 (full flags treatment); a one-line mention also lands in Lesson 4.

## The decision
Two layers, deliberately separated:

1. **The judgment skill (vendor-agnostic) is the lesson.** Own a thin, team-owned `FlagClient` wrapper and direct agents with "put this behind our FlagClient" — never let an agent scatter a vendor SDK through the codebase. Pair it with a **flag-debt discipline**: every flag gets an owner + a removal date + a rule for when a config toggle graduates to a real flag service. This is the director's responsibility and the real content. Grounded in the [LeadWise article on flags in AI-generated code](https://www.leadwise.pro/en/blog/statsig-posthog-and-launchdarkly-feature-flag-choices-in-ai-generated-code), which is the most mission-relevant flag source (AI agents default to a vendor SDK even when an env var would do).

2. **PostHog is the concrete example / recommended pick** for this greenfield SaaS — best single tool (flags + analytics + session replay + experiments), ~1M flag requests/mo free, open-source/self-host escape hatch. Alternatives to *mention* so the learner knows when **not** to reach for a vendor:
   - **Env var / config toggle** — enough when the flag only hides unfinished work and needs no runtime flip or targeting. The "do you even need a vendor?" baseline.
   - **Vercel Flags SDK** — free, provider-agnostic "flags as code," Next.js-native; can use PostHog as its backing provider (so it's not either/or). Lightest option on their Vercel-style stack.
   - **LaunchDarkly** — enterprise/governance/compliance; overkill for a solo greenfield.
   - **GrowthBook / Unleash** — OSS self-host, free but more ops burden.
   - **Statsig** — unlimited free flags + experimentation, now OpenAI-owned (strategic uncertainty for a long-lived bet).

## Why this framing
The learner is the director of AI committers (see [[0001-prior-git-experience]]). The tool choice is less important than the *control surface* over flags — which is exactly the "teach judgment, not incantations" mandate from [[MISSION.md]]. The wrapper + cleanup discipline also connects back to Lesson 3's "scope the task in the brief" ([[0002-reviewable-pr-and-task-scoping]]): "add this behind our FlagClient" is a brief instruction.

## Open thread
Sources captured in `RESOURCES.md`. Not yet decided: whether the wrapper example in Lesson 6 should be shown as concrete code (the learner doesn't commit, so probably a small illustrative snippet + the prompt-to-agent, not a deep implementation).
