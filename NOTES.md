# Working Notes

## Learner context (from kickoff 2026-06-09)
- **Role in the workflow:** Solo human director. Claude Code (AI) does all implementation, commits, and PRs. → Teach *judgment, review, and release decisions*, not git CLI memorization.
- **Project:** Greenfield web app / SaaS, continuously deployed.
- **Preview model:** Per-PR preview deploys (Vercel/Netlify-style) — this is the learner's review surface.
- **Prior knowledge:** Has used Git "loosely," never a formal flow (no GitFlow / GitHub-flow background). Start from mental model.

## Teaching preferences
- Mission says: focus on judgment over CLI incantations. Frame lessons around "as the reviewer/release manager, you decide X."
- Lessons should be concrete to *their* project (web app, AI committers, preview deploys), not generic.

## Learner's stated extra interest (2026-06-09)
- Wants to understand **multiple AI agents working multiple features simultaneously, all pushing PRs in one day.** Folded into lesson 2 (parallel branches + merge queue + logical conflicts). Likely wants a future lesson on *partitioning work across agents* so branches don't collide.

## Curriculum roadmap (provisional)
1. ✅ The Trunk and the Loop — core mental model (lesson 0001)
2. ✅ Protecting the Trunk for Parallel Agents — day-one branch protection + merge queue + logical conflicts (lesson 0002)
3. ✅ The Reviewable Pull Request — S·S·S (small/single-purpose/self-describing), the Cisco review ceiling, triage (review/split/send-back), scoping the brief, and slicing work across agents (lesson 0003).
4. Preview deploys as the review surface — what to check on each PR's preview URL.
5. Releases in continuously-deployed web apps — release-from-trunk vs release branches; pick one.
6. Feature flags — hiding incomplete work on trunk instead of long-lived branches.
7. Hotfixes — fix-forward vs cherry-pick onto a release branch.
