# AI USE DISCLOSURE — Assignment 5 (Setup Exercise: Your Search's Personal Layer)

**Tool(s) used:**
Claude Code (Claude, model Sonnet 5), and Claude (Opus 5.5, via a separate
claude.ai chat, not Claude Code and not a human reviewer) for its own
`resume.json` extraction; a review of that extraction; target-role framing
suggestions; web research behind the CPT and E-Verify wording and a suggested
publication-venue check (I did not run that check myself); and reviews of
`profile.yml`, two `gaps.md` drafts, and the `logs/RUN_LOG.md` entry.

**Portions assisted:**

- Extracting `search/resume.json` from `Pratham_Rathod_Resume.pdf` and a second,
  differently-framed resume draft I supplied, structuring prose bullets into
  typed fields (dates, titles, companies). Claude (claude.ai) separately performed
  its own extraction from the same material, but all three real attestation
  errors in the final file were ones I caught myself, directly (see "What I
  changed" below).
- Drafting `search/profile.yml` from my answers to the five required intake
  questions, including target-role framing suggestions from Claude (claude.ai).
- Researching real evidence for `search/gaps.md`: fetching Palantir's and Cursor's
  actual new-grad job postings and the official O*NET page for SOC 15-1252.00
  (Software Developers) directly, rather than relying on search-result summaries.
- Independently re-verifying one project claim in `resume.json` by directly running
  `pnpm test` against the live Sutriva repository under the Node version its own
  `package.json` requires — not by trusting the project's README or any resume
  draft's claimed test count.
- Setting up `search/`, gitignoring `search/private-notes.md`, and — after my
  explicit, informed decision to override this repository's own default privacy
  policy for this one assignment — adjusting `.gitignore` and `scripts/doctor.mjs`
  to allow `search/resume.json` specifically to be committed.

**How used:**
I supplied the real source material (my resume PDF, a second resume draft, and
direct answers to the intake questions) and made every judgment call the
assignment reserves for the human: which resume content was accurate, which of
two conflicting-looking University of Mumbai entries were actually two separate
real jobs, what my actual target role and visa situation are, which gap row to
kill and why, and how to rewrite the testing gap in my own words. Claude Code
drafted the structured files and ran the real verification work (fetching
postings, running the live test suite). Claude (via claude.ai, a separate AI
tool) did its own parallel `resume.json` extraction and suggested target-role
framing, and reviewed drafts of `profile.yml`, `gaps.md` (twice), and the
`logs/RUN_LOG.md` entry — catching real defects in those three, cited below. All
three `resume.json` attestation errors were caught by me directly, not by
either AI tool.

**What I changed:**
All three `resume.json` errors were ones I caught myself, directly, with no AI
involved in finding any of them: the chronology break (Full-Stack Developer
mis-sequenced ahead of Moonlighting), the GPA scale (Claude Code had silently
assumed "3.5/4.0" was a native figure; I caught this and supplied the actual
fact — it's my own conversion from a 10-point Indian CGPA), and the `"present"`
string sitting in a date-typed field. (A review of an earlier draft of this
disclosure incorrectly credited claude.ai with flagging the GPA scale and the
`"present"` string — I checked that claim against the actual conversation record
and it does not hold up; both were things I reported directly, in my own words,
with no claude.ai review in between. That incorrect attribution has been
corrected here.)

Separately, Claude (claude.ai) reviewed a draft of `profile.yml` and found a
three-way contradiction in the target-role scope (the primary-role sentence said
"seed-Series D" while `company_size_range` and `industry.target_sectors` both
included big tech, fintech, and consumer tech), an imprecise CPT note (it should
state the actual 12-month full-time-CPT rule and what needs DSO confirmation, not
a vague "real limits" claim), a missing STEM-extension E-Verify gate, a redundant
exclusion, and a company name (Whitespace) that belonged in
`search/private-notes.md` rather than the public file — all fixed.

Claude (claude.ai) then reviewed my own killed-row and rewritten-row edits to
`gaps.md` and found a leftover sentence fragment, a rewritten evidence cell that
had drifted from a real citation to a prediction ("every backend role I'm
targeting will ask..."), a gap/plan mismatch (a gap titled as unclosable paired
with a plan that could partially close it), and a kill-row sentence that claimed
more than the two postings actually checked — all fixed, with the evidence cell
now citing an exact quote from Cursor's own posting.

A third claude.ai review pass of the `logs/RUN_LOG.md` entry itself found that
two of the three named resume.json "errors" were formatting fixes (list order,
`"present"` vs. `null`), not errors about my actual history — only the GPA
conversion was substantive — and suggested stronger candidates to check: the
project `type`/`team_size` fields, the Moonlighting title, and the identical 15%
metric on two different University of Mumbai entries. I confirmed all three
accurate on direct review (none became new corrections), and that confirmation
is now recorded in `logs/RUN_LOG.md` rather than silently omitted.

Claude (claude.ai) flagged, in both of its `gaps.md` review passes, that the
large-org-experience row's evidence described mentorship Palantir *offers*, not
experience it *requires* — a distinction it caught twice before Claude Code
acted on it. Claude Code's own re-check, prompted by that flag, then found the
underlying cause (two different job postings conflated in the evidence cell) and
removed the row itself.

Separately, after the review above, I clarified the relationship behind the
single ambiguous publications string `"ICIET-23; Journal of Harbin Engineering
University"`: ICIET-23 is the conference it was presented at, and the journal is
where it was published. `resume.json` now carries these as two real fields
(`presented_at`, `published_in`) instead of one ambiguous string. Claude (claude.ai)
suggested cross-checking the journal against the Retraction Watch Hijacked
Journal Checker; I have not done that check as of this disclosure.

**What the AI could not do:**
Claude Code could not tell, from the resume text alone, that the two University
of Mumbai entries (Full-Stack Developer, Sep-Dec 2022; Android Developer, Dec
2023-Mar 2024) were two separate real jobs rather than one job described
inconsistently across two resume drafts — only my own memory of my history
resolved that, and it changed how the record is structured, not just a wording
choice.

Claude Code silently assumed the 3.5 was a native 4.0-scale figure; no AI could
know it was my own conversion from a 10-point CGPA — only I knew that, caught
the assumption, and supplied the actual fact directly. Neither Claude Code
nor Claude (claude.ai) could resolve the real factual question of Sutriva's
current test count on their own say-so — three different numbers (87, 98, 111)
appeared across this exercise from different sources and different points in
time, and only a direct, live `pnpm test` run against the exact repository,
prompted by me pointing at a more current copy of it, settled which one was
actually true. Claude Code also could not know the real relationship between
"ICIET-23" and "Journal of Harbin Engineering University" in my own publication
— whether one was a conference and the other a journal, or something else — and
left them as one ambiguous string until I supplied the actual answer. Separately,
when asked directly whether six listed skills (GCP, Java, Gemini, Groq, RAG,
pgvector) with no supporting bullet anywhere in `resume.json` should be removed
or defended, I chose to keep them listed as-is — a judgment call about risk
tolerance in my own job search that Claude Code could only surface, not make
for me.
