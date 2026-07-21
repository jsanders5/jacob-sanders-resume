---
name: ats-resume-scoring
description: Use when asked to evaluate a resume against a job posting, compute or estimate an ATS score, check how well a resume matches a specific role, or assess keyword/requirement fit. Requires the actual job posting (URL or pasted text) — do not score without one.
---

# ATS Resume Scoring

## Overview

Score a resume against a **specific** job posting by matching it to the
posting's stated requirements and keywords, then report an honest score with a
gap analysis. ATS scoring is only meaningful against real posting text — a
number produced without the posting is fiction.

## The one hard rule

**Never produce a score without the actual job posting.** If the user hasn't
given a posting URL or pasted text, ask for it. A generic "resume quality"
opinion is not an ATS score and must not be presented as one.

## Workflow

1. **Get the posting text.** If given a URL, fetch it. Modern career sites
   (Eightfold, Workday, Greenhouse, Lever, Ashby) are JavaScript apps —
   fetching the human URL often returns site *config/JSON boilerplate*, not the
   job. When that happens, hit the platform's JSON API instead (see table).
2. **Extract requirements verbatim** into buckets: required/basic
   qualifications, preferred qualifications, knowledge/skills/abilities, and
   notable repeated keywords (titles, tools, shift/availability language).
3. **Match each requirement to resume evidence.** For every required item, find
   where the resume satisfies it (quote the line) or mark it a gap.
4. **Score** with the rubric below.
5. **Report** the score, a requirements-coverage table, keyword alignment, and
   an itemized list of what cost points — separating true ATS gaps from
   human-screen risks.

## Fetching from JS career sites

If a fetched careers page returns only theme/nav/config, extract the job/posting
id from the URL and call the platform API:

| Platform | Human URL clue | JSON endpoint |
|---|---|---|
| Eightfold | `*.eightfold.ai/careers?...pid=NNN` | `https://{tenant}.eightfold.ai/api/apply/v2/jobs/{pid}?domain={domain}&pid={pid}&microsite=1` |
| Greenhouse | `boards.greenhouse.io/{co}/jobs/{id}` | `https://boards-api.greenhouse.io/v1/boards/{co}/jobs/{id}` |
| Lever | `jobs.lever.co/{co}/{id}` | `https://api.lever.co/v0/postings/{co}/{id}` |
| Workday | `{t}.wd*.myworkdayjobs.com/{site}/job/...` | `https://{t}.wd*.myworkdayjobs.com/wday/cxs/{t}/{site}/job/{path}` |

If none apply, ask the user to paste the posting text.

## Scoring rubric (out of 100)

- **Required/basic qualifications (~60):** each unmet required item is a large
  deduction; each met item full credit. Missing a hard requirement caps the
  score low.
- **Preferred quals + KSAs (~25):** partial credit for coverage.
- **Keyword/title alignment (~15):** does the resume echo the posting's own
  language — job title, core skills, shift/availability terms?

Give a single number plus a one-word band (Strong / Solid / Weak). State the
method: keyword+requirement matching. Note that AI-based matchers (e.g.
Eightfold) score *semantic* fit, so exact-wording gaps hurt less than genuine
domain gaps.

## Report format

- **Score: NN/100 — Band**, with a one-line method/caveat note.
- **Required qualifications table:** requirement | met? | evidence line.
- **KSA / preferred coverage:** brief.
- **Keyword alignment:** which high-value terms are hit.
- **Points off:** itemized with (–N) each. **Separate** true ATS gaps from
  human-screen risks (e.g. overqualification) — the latter don't lower the ATS
  keyword score but belong in the honest picture.
- **Quick wins:** only truthful edits (see below).

## Truthfulness (non-negotiable)

Only recommend keyword additions backed by the person's real experience. Never
suggest inserting a skill, tool, or domain term they haven't done to game the
match. Reframing real experience in the posting's vocabulary is fair; inventing
it is not. If a gap can't be closed honestly, say so.

## Common mistakes

- Scoring off a fetched page that was actually site config, not the job — verify
  you have real requirements text first.
- Reporting only a number — the value is the gap analysis and truthful quick wins.
- Padding with unbacked keywords to inflate the score — forbidden.
