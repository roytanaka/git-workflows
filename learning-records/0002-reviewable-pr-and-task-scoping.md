# Reviewable PRs, the review ceiling, and scoping over splitting

**Taught in:** Lesson 0003 — The Reviewable Pull Request (2026-06-09).

## What the learner now has
- **The review ceiling as the master variable.** A human reviews effectively up to ~200–400 LOC in a 60–90 min sitting (70–90% defect yield; collapses past ~500 LOC/hr — Cisco/SmartBear). Past the ceiling, "approve" = unreviewed code. Framed specifically for the AI-committer trap: agents have no natural friction keeping diffs small, so the *director* must impose the limit.
- **S·S·S** as the test for a reviewable PR: **S**mall, **S**ingle-purpose, **S**elf-describing. Small is necessary but not sufficient — single-purpose is the one learners most often miss.
- **The mindset shift for their role:** you don't shrink diffs at review time; you **scope the task in the brief** (one outcome + a boundary + a flag for anything too big). The fix for a too-big PR lives in the *next brief*, not the PR.
- **Triage as a skill:** review now / split it / send back — practiced interactively.
- **Slicing across parallel agents** (their stated interest, see [[NOTES.md]]): partition by feature + files; land shared foundations first as their own PR. Explicitly tied back to the Lesson 2 logical conflict.

## Open threads / next zone of proximal development
- Feature flags were forward-referenced twice (as the escape hatch for "too big to ship whole"). Lesson 6 is now primed — learner may want it pulled earlier.
- Lesson 4 (preview deploys as the review surface) is the natural next step and is teased in the lesson's "ask your teacher" + quiz. The S·S·S "self-describing" property already plants "what to check on the preview."
- Possible practical follow-up the learner may request: a concrete reusable **brief template** for directing agents (a stub exists in the rubric reference).
