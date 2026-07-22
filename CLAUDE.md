# CLAUDE.md — jacob-sanders-resume

Context for Claude Code (or any Claude session) working in this repo.

## What this repo is

Jacob "Jake" Sanders's resume, as a single LaTeX source file
(`jacob_sanders_resume.tex`), plus a compiled PDF and a GitHub Pages preview.

## Target role

Positioned for **Forward Deployed Engineer / Applied AI Engineer** — not generic
"software engineer." Anthropic uses "Applied AI Engineer" for the role other AI
labs (OpenAI, Palantir, Databricks) call Forward Deployed Engineer; Jake applies
across both titles.

Why this role: 13+ years of end-to-end shipping across wildly different domains
(embedded audio firmware → blockchain → SaaS founder → LLM apps) is unusually
close to the FDE ideal profile — breadth over narrow depth, fast domain ramp,
comfortable shipping in ambiguity. The market data behind this call (as of
mid-2026): FDE/Applied AI postings up ~800–1000% YoY, comp $300K–$550K+ at
frontier labs, and hiring concentrated at Palantir, OpenAI, Anthropic, Databricks,
plus a long tail of Series A/B AI startups.

## Evidence base — three real projects, described accurately

Don't inflate these with buzzwords not backed by the code. Accurate framing:

- **sentics** (github.com/jsanders5/sentics) — the flagship piece. A
  *multi-agent pipeline*, not an autonomous tool-using agent: a deterministic
  technical-analysis stage owns the directional call, a Claude Sonnet stage
  writes rationale under a strict output whitelist (can't override the
  ground-truth classification), and a Claude Haiku stage classifies news into
  structured sentiment. Has a genuine leak-free forward-tracking eval harness
  (`eval_calls.py`) — logs every call to an immutable ledger, scores against
  realized returns with edge/hit-rate/Sharpe/t-stat. Model-tiered for cost
  (~88% run-cost reduction documented in `docs/COST-OPTIMIZATION-SUMMARY.md`).
  If asked in an interview to "walk through the agent's tool use": be honest
  that it's an orchestrated pipeline, not an autonomous agent — the guardrail
  design is the actual strength to highlight.
- **resumi** (github.com/jsanders5/resumi) — LLM job-matching app. Claude API
  for structured JSON scoring (skills/experience/domain/requirements
  breakdown), Voyage embeddings for semantic search, prompt caching, Sentry
  observability, deployed on Vercel.
- **PySando** (github.com/jsanders5/PySando) — interactive Python tutorial
  platform. FastAPI backend runs learner code in a sandboxed subprocess graded
  against hidden pytest suites; a Claude-powered tutor is grounded in the live
  lesson/exercise/learner code and guardrailed to never reveal solutions.
  Async multi-turn conversation state, provider abstraction, graceful
  degradation without an API key.

## Writing / editing preferences

- Brevity, no filler phrases ("passionate about," "proven track record").
- Technical specificity over generic claims — name the actual stack/pattern.
- Natural first-person voice in cover letters; resume bullets stay in the
  standard resume idiom (no "I").
- Don't claim skills or experience not backed by the repos/work history.

## Build

```
pdflatex jacob_sanders_resume.tex   # run twice — hyperref needs a second pass
```

Requires `texlive-fonts-extra` for the `sourcesanspro` and `fontawesome5`
packages used in the header/icons.

## GitHub Pages

**Every new resume variant must be published to the GitHub Pages preview
(`index.html`) as part of creating it — not a separate, later step.** Add it
to the `resumes` object in the inline script (label, subtitle, PDF filename,
accent color) so it appears as a tab in the switcher alongside the existing
resumes. Verify the wiring (e.g. a quick DOM-shim test) before committing.
