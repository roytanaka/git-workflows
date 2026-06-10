# Hotfixes: the two clocks and the decision ladder

**Taught in:** Lesson 0007 — When Production Breaks (2026-06-10). **Closes the core curriculum path.**

## What the learner now has
- **A hotfix is not a special process** — it's the roll-forward rule (Lesson 5 §3) under a stopwatch. For a release-from-trunk team, trunk *is* production, so a fix just goes on trunk, fast. The GitFlow `hotfix/`-branch-off-a-tag ceremony is named only as a contrast you're *not* adopting.
- **The two clocks** (the lesson's signature frame): **mitigation** = stop the bleed, seconds→minutes, can be temporary/ugly/code-free; **remediation** = fix the cause on trunk, calm + reviewed, no stopwatch. The classic disaster is conflating them — shipping a rushed unreviewed root-cause fix under fire, which causes the *second* incident. Mitigate first to buy time, then remediate through the normal CI + diff + preview gate.
- **Fastest mitigation needs no code:** the **flag kill switch** (Lesson 6's ops toggle). First question in any incident: "is the broken thing behind a flag we can flip?" If yes, a sev-1 becomes a calm Monday fix. This is the explicit payoff of having put risky features behind a flag.
- **Revert is roll-forward, not rollback.** Redeploying an old build leaves the bug on trunk (next merge re-ships it — the Lesson 5 trap). The TBD move is GitHub **Revert** → a *new PR reverting the merge commit*, history preserved, flowing trunk → production. A revert is a commit *forward* that undoes an old one.
- **The four-rung decision ladder** (ordered fastest/lowest-risk first; take the highest rung you can reach):
  1. **Flag off** — broken feature behind a flag → kill-switch it. Seconds, no deploy.
  2. **Revert on trunk** — no flag but you can name the bad change → ship the revert. Minutes.
  3. **Roll forward a fix** — can't simply remove it (shared code / bug predates one PR) → fix on trunk fast. Also where *remediation* lives after mitigating on 1–2.
  4. **Cherry-pick to a release branch** — *rare*; only a supported pinned version you can't roll forward (the one Lesson 5 trigger). Fix on trunk first, then cherry-pick — never the reverse.
- **Reviewing under fire:** mitigating first is what lets the fix PR keep the three-signal bar (Lesson 4) and the S·S·S rubric (Lesson 3) — smallest diff, single purpose, easy to revert — exactly when stakes are highest. Watch-fors: "skip CI/preview because it's urgent," SSH patch to prod, redeploy-old-build "rollback."

## Source added (verified 2026-06-10)
- **GitHub Docs — [Reverting a pull request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/incorporating-changes-from-a-pull-request/reverting-a-pull-request)**, added to `RESOURCES.md`. Verified quote grounds "a revert creates a new PR reverting the merge commit; history preserved." The roll-forward and fix-forward-vs-cherry-pick claims reuse the two trunkbaseddevelopment.com pages already cited in Lessons 5.

## Connections
- Direct payoff of [[0005-releases-and-commit-convention]] (roll-forward rule; fix-on-trunk-first then cherry-pick) and Lesson 6's ops/kill-switch toggle (plan in [[0003-feature-flag-tooling-decision]]).
- Reuses Lesson 3's S·S·S reviewability and Lesson 4's three review signals as the "review under fire" bar.

## Next zone of proximal development (post-core)
The core path (Lessons 1–7) is complete. Candidate follow-ons, in priority order:
- **Partitioning work across parallel agents** so PRs never collide — the learner's *original stated extra interest* (2026-06-09, NOTES), seeded in Lessons 2–3 and re-surfaced in Lesson 7's closing asks. Strongest candidate.
- **Detecting** the break: monitoring/alerting for a greenfield SaaS (Lesson 7 assumes you notice).
- **Blameless incident retro** — what the post-fire review should produce.
