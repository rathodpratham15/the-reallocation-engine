# search/gaps.md — Delta: Attested Record vs. Target Role Requirements

## How to read this table

- **Evidence column**: cites a real posting, an O*NET requirement for SOC 15-1252.00
  (Software Developers), or a pattern observed across what was actually checked —
  not a feeling or an industry assumption.
- **Plan column**: describes an *output* someone else could verify, not an activity
  like "take a course."
- Drafted by the agent on 2026-10-29 from `resume.json` (attested) and
  `profile.yml` (target_role); reviewed and edited by Pratham per the assignment's
  required two edits, then further corrected across two rounds of claude.ai
  review — including a weak evidence cell claude.ai flagged twice before Claude
  Code found its root cause and removed it — see below the table and
  `logs/RUN_LOG.md`.

---

| Gap | Evidence the target demands it | What I have | Plan to close it |
| --- | --- | --- | --- |
| No visible evidence of correctness testing, especially for the concurrency bugs I claim to have fixed | Cursor's New Grad 2027 posting (the same posting already cited below) asks for engineers who "blend strong engineering and AI tools as leverage without giving up correctness" and describes "raising the bar on taste and correctness while you move fast" (fetched directly from cursor.com/careers/software-engineer-new-grad-2027) — correctness, not just shipping speed, is an explicit bar, and full-stack is the actual target, not backend specifically. None of my four jobs gives me a correctness answer beyond "it worked in production." | More than the agent gave me credit for. Sutriva has 111 tests, independently run and passing, plus an eval harness that grades fixes against seeded bugs. InferMesh has 114 Go tests (self-reported, not yet re-verified). At Moonlighting I load-tested peak traffic with JMeter and Postman, which is employer-context testing, just performance rather than correctness. At Swapt I was the sole engineer and fixed a real race condition, but nothing in that bullet shows a test that would catch it coming back. | Two parts, each with its own closing condition, since I can't manufacture employer history. (1) Make the testing I already do visible: add Sutriva's real test count to its `resume.json` entry, re-verify InferMesh's 114 myself, and add a Go coverage threshold enforced in GitHub Actions. Closing condition: a public, passing CI run link on the InferMesh entry. (2) Write a concurrent-redemption test for the SELECT FOR UPDATE pattern I used at Swapt, in a personal repo, so the race-condition bullet has a reproducible test behind it. Closing condition: a public repo link to that test with its own passing CI run. |

**Removed, 2026-10-29:** "No track record inside a large engineering org's
review/design process," originally cited to "Palantir's ...posting...and related
postings describe structured mentorship from senior engineers." Claude (claude.ai)
flagged, in both of its review passes on this file, that this evidence described
mentorship Palantir *offers*, not experience it *requires* — catching the real
problem before the agent fixed anything. Claude Code's own re-check, prompted by
that flag, then found the underlying cause: the mentorship language came from a
*different* posting than the one actually fetched (jobs.lever.co/palantir), which
only lists a preferred degree, language proficiency, and graduation timing as
requirements — nothing about prior large-org experience. Worse, Pratham's real
record (MS in Computer Software Engineering, Dec 2026 graduation) appears to
*meet* what that posting actually requires. An evidence cell that doesn't support
its own gap is exactly the violation this table exists to catch, so it's removed
rather than patched with better-sounding but still-unverified evidence.

**Killed:** "Hands-on model-training / ML-research experience." The agent filled
the evidence cell with "industry assumption," the exact kind of evidence this
table bans, because it pattern-matched "AI engineer" to "ML researcher" when
neither posting I actually checked (Palantir, Cursor) asks for model training,
and my actual AI work (inference serving in InferMesh, evals and MCP in Sutriva,
LLM orchestration in Orqen) sits on the application and infrastructure side of
the stack.

## Closed gaps (move entries here when resume.json is updated with closing evidence)

| Gap | How it closed |
| --- | --- |
| No reviewable live link attached to two of three personal projects (originally cited to Cursor's New Grad 2027 posting's "an app, OSS, or shipped product we can open and review") | Closed 2026-10-29: added real, already-existing `url`/`repo`/`npm` fields to InferMesh (`github.com/rathodpratham15/infermesh`), Sutriva (`sutriva.pratham.click`, GitHub, npm), and Orqen (`orqen.pratham.click`) in `resume.json`. This was correctly flagged in review as a same-day documentation fix rather than a real skill gap — the links already existed, nothing new was built — so it's recorded here as closed rather than left as an open gap. |

---

## Required edits (Pratham) — done

1. **Killed row**: "Hands-on model-training / ML-research experience" — see the
   explanation under the table. It was drafted from an industry assumption, not
   from either posting actually checked, which is the exact evidence violation
   this table exists to prevent.
2. **Rewritten row**: the testing gap (first row) — rewritten in my own words to
   credit the real testing I already do (Sutriva's 111-test suite, Moonlighting's
   performance load-testing) instead of accepting the agent's flatter "no
   employer-context testing bullet" framing, while still being honest that none
   of it is a *correctness* test inside employer code.
