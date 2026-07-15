# Hypotheses — Week 23, 2026

**Generated:** June 4, 2026
**Skill used:** `skill-hypothesis-generating.md` (all 3 sources + synthesis)
**Next step:** Run top candidate through `skill-hypothesis-check.md` → open DL-3

---

## Sources used this run

| Source | Input |
|---|---|
| **Market / competitors** | June 2026 market scan — cross-industry Scrum Master reporting benchmarks |
| **CustDev** | DL-2 interviews (scriptwriters, 20% sprint on fixes); DL-1 team friction signals (report maintenance, commentary); DL-0 adjacent pain (coverage gaps) |
| **Vision / product data** | DL-0 → DL-1 pattern ("generate from scratch" solved → next = "maintain existing artifacts"); DL-2b residual; DL-1 tool already in production |

**Rule of two sources:** hypotheses confirmed by 2+ sources are marked ★

---

## Priority Table

| # | Hypothesis | I | C | A | Score | Sources | Status |
|---|---|---|---|---|---|---|---|
| 1 | Scriptwriters: AI diagnoses root cause of broken scripts | 8 | 8 | 8 | **512** | CustDev ★ Vision | Start now |
| 2 | DL-1 expansion to other analyst teams in the bank | 8 | 9 | 5 | **360** | Market ★ Vision | Start now |
| 3 | Data analysts: AI auto-refreshes recurring reports | 7 | 5 | 9 | **315** | CustDev ★ Vision | Start now |
| 4 | Team leads: AI generates sprint reports + retro summaries | 7 | 6 | 7 | **294** | Market ★ Vision | Start now |
| 5 | Scriptwriters: AI detects intent coverage gaps in NLU library | 6 | 6 | 8 | **288** | Vision ★ CustDev | Start now |
| 6 | Data analysts: AI drafts commentary for stakeholder reports | 6 | 5 | 9 | **270** | CustDev ★ Market | Start now |
| 7 | Data analysts: AI creates new dashboards from data model description | 7 | 4 | 9 | **252** | Vision | Start now |
| 8 | Scriptwriters: AI auto-generates changelog after script fix | 4 | 5 | 8 | **160** | Vision | Start now |

**I** = Impact (sprint time if confirmed) · **C** = Confidence (evidence strength) · **A** = Access (path to ICP now) · all 1–10

---

## Detailed Entries

---

### #1 — Scriptwriters: Script defect root-cause diagnosis
**Score: 512** | Sources: CustDev ★ Vision | **→ Recommended for DL-3**

**Hypothesis:**
> Chatbot scriptwriters will recover ≥15% sprint capacity if AI diagnoses the root cause of a broken script from script + error log, so they spend time fixing instead of investigating.

**Why this pain is real:**
DL-2 interviews confirmed 20% sprint waste on script fixes. The majority of that time is investigation (reading code + logs to find what broke), not the fix itself. The fix is fast once the cause is known. DL-2 failed because full vibe coding requires technical judgment — but diagnosis-only is a narrower, achievable task.

**Key difference from DL-2:**
AI does NOT write the fix. It reads script + error log → outputs root cause + location. Scriptwriter still owns the fix. This avoids the DL-2 failure mode entirely.

**Main risk:**
Self-hosted open-source LLM (LLaMA/Mistral) on context-heavy JavaScript. Mitigation: test on a bounded script size first; if quality degrades, consider a RAG approach over the script codebase.

**Signals confirmed:**
- DL-2 interviews: 20% sprint on fixes (confirmed, real interviews)
- DL-2 residual (DL-2b): diagnosis angle was explicitly never tested

---

### #2 — DL-1 expansion to other analyst teams
**Score: 360** | Sources: Market ★ Vision

**Hypothesis:**
> Other analytics teams in the bank will expand sprint capacity by ~20% if they get access to the Text→SQL pipeline already running for the DL-1 team, assuming they have the same ad-hoc SQL bottleneck.

**Why this hypothesis is different:**
Nothing new to build. The pipeline exists, it's in production, it works. This is a rollout hypothesis, not a build hypothesis. Validation is fast: one interview with another team lead to check if the pain pattern matches.

**Main risk:**
Other teams may use different data sources, schemas, or have different security access levels. The tool may not generalize out-of-the-box without tuning.

**Signals confirmed:**
- DL-1 result validated (20% sprint recovered — team lead estimate)
- JPMorgan-scale rollouts show enterprise-wide analyst AI adoption works

---

### #3 — Data analysts: Recurring report update automation
**Score: 315** | Sources: CustDev ★ Vision

**Hypothesis:**
> Data analysts on the DL-1 team will recover 10–15% sprint capacity if AI auto-refreshes recurring reports (data pull via SQL + format preservation + anomaly flag), so they review instead of rebuild.

**Why this pain is real:**
Same team as DL-1. After SQL bottleneck is solved, report maintenance is the next visible friction: weekly/monthly reports for business units and management, same format, new numbers every cycle. Confirmed by team context — team lead estimate 10-15%.

**Main risk:**
Confidence is low (C=5) — this is a team lead estimate, not a measured sprint metric. The real interview may reveal this is smaller than expected. Also: reports go to management → quality bar is high → "I'll check every number anyway" friction (confirmed objection).

**Validation approach:**
1 interview with DL-1 team lead: "After SQL, what's the next manual task that still eats sprint time?"

---

### #4 — Team leads: Sprint ceremony documentation automation
**Score: 294** | Sources: Market ★ Vision

**Hypothesis:**
> Team leads will save 30–90 min per sprint if AI generates sprint reports and retrospective summaries from Jira data + meeting notes, without manual synthesis.

**Strategic value beyond the metric:**
Team leads approve pilots. Solving their own pain makes them champions — not just users. This is the highest-leverage relationship investment in the current access-constrained situation.

**Evidence:**
86% of Scrum Masters save 30–120 min/sprint on reporting with AI tools (2024 cross-industry case study). In this bank, team leads double as SMs — pain falls on the same person who controls the pilot decision.

**Main risk:**
Cross-industry evidence, not bank-specific. Russian bank team leads may run different ceremony formats. LLM fit is high (text summarization + templated output).

---

### #5 — Scriptwriters: Intent coverage gap detection
**Score: 288** | Sources: Vision ★ CustDev

**Hypothesis:**
> Chatbot scriptwriters will reduce production misrouting incidents if AI analyzes the existing intent library and surfaces coverage gaps before they reach production.

**Why this pain exists:**
Coverage gaps are currently found in production (misroutes → emergency fixes). The DL-0 team writes RegExp patterns but has no systematic way to check if the full intent space is covered. This is a proactive version of the DL-0 problem.

**LLM fit:**
Good — bounded dataset (the intent library), pattern analysis. Similar to DL-0 complexity.

**Main risk:**
Impact is harder to measure (preventing future incidents vs. recovering existing sprint time). Team lead may not feel pain acutely until after a production incident.

---

### #6 — Data analysts: Stakeholder commentary generation
**Score: 270** | Sources: CustDev ★ Market

**Hypothesis:**
> Data analysts will recover 5–8% sprint capacity if AI drafts the text commentary accompanying reports ("metric X changed by Y% this period due to Z"), leaving analysts to edit rather than write from blank.

**Why this works on open-source LLM:**
Text generation from structured data delta is one of the strongest capabilities of smaller open-source models. The output is formulaic enough to be reliable.

**Main risk:**
Business stakeholders and management are the audience — commentary tone and framing matter. "I'll rewrite it anyway" risk. Validate: does the analyst actually write commentary today, or skip it?

---

### #7 — Data analysts: Dashboard creation from data model
**Score: 252** | Sources: Vision

**Hypothesis:**
> Data analysts will reduce dashboard creation time by ≥50% if AI generates a working dashboard draft from a natural language description of the data model and required metrics.

**Why confidence is low (C=4):**
This is vision-driven — no interview confirmation yet. Dashboard creation involves visual judgment, stakeholder taste, iterative feedback. More complex than SQL generation. May hit the "dashboards require taste" objection hard.

**Validation approach:**
Ask in the next DL-1 team interview: "After recurring reports, what else takes time — building new dashboards from scratch, or something else?"

---

### #8 — Scriptwriters: Auto-changelog after script fixes
**Score: 160** | Sources: Vision

**Hypothesis:**
> Chatbot scriptwriters will reduce documentation debt if AI generates a changelog entry and updates script documentation automatically from the git diff after each fix is committed.

**Why impact is low (I=4):**
Documentation is skipped under sprint pressure — it's pain, but it's accepted pain. Team lead may not prioritize it. However, this is a low-risk pilot: no mission-critical output, easy to validate, builds trust with the team.

**Best use:**
If #1 (defect diagnosis) pilot is in progress, this can run in parallel as a low-stakes parallel track.

---

## What this run confirmed

1. **Best immediate bet:** #1 (scriptwriter diagnosis) — highest score, confirmed pain, existing access, avoids DL-2 failure mode
2. **Fastest ROI:** #2 (DL-1 expansion) — nothing to build, one interview to validate
3. **Strategic play:** #4 (team leads) — low impact per metric but high access leverage; creates champions

## Deduplication notes

- #3, #6, #7 are all from the same DL-1 team — validate in a single interview session, not three separate ones
- #1, #5, #8 are all scriptwriter team — can be sequenced: start with #1, layer in #5 and #8 after trust is established

---

---

## Synthetic CustDev Results (run June 4, 2026)

All 10 hypotheses tested through `skill-synthetic-custdev.md` persona simulation.

| # | Verdict | Key finding |
|---|---|---|
| #1 | ✅ Confirmed | Pain split confirmed (diagnosis >> fix). Acceptance criterion discovered: test on already-fixed bugs. |
| #2 | ✅ Confirmed (amended) | Schema onboarding ~1-2 dev days per team. Not zero-build. Maintenance ownership question will come up. |
| #3 | ⚠️ Confirmed, smaller | 3-4% sprint (not 10-15%). Review step doesn't disappear. Still worth doing. |
| #4 | ❌ Dropped | "Annoying but not critical." Jira integration hard with self-hosted LLM. |
| #5 | ☠️ Killed | Needs conversation logs → PII constraint. Hard blocker. |
| #6 | ❌ Dropped | 0.6% sprint. Too small. Bundle into #3 as a feature. |
| #7 | ❌ Dropped | Pain is in stakeholder iteration, not initial build. Low frequency. |
| #8 | ❌ Dropped | Real but low impact. Bundle into #1 as background git-hook feature. |

## Top 3 for Real-World Validation

**#1 → DL-3 candidate: Scriptwriter script defect diagnosis**
Validation question: *"When a script breaks, what % of your time is diagnosis vs. the actual fix?"*
Pilot design: test on already-fixed bugs, compare AI diagnosis to real diagnosis.

**#2 → DL-3 candidate: DL-1 expansion to other analyst teams**
Validation question: *"Do business stakeholders bring ad-hoc data requests to your analysts? How often per sprint?"*
One interview confirms or kills. Tool already exists.

**#3 → DL-3 candidate: Recurring report automation**
Validation question: *"What does your Monday morning look like before you send the weekly report?"*
Frame as: eliminate copy-paste/formatting work, not "automate your reports."

---

*Generated using `skill-hypothesis-generating.md` — Sources: Market scan (June 2026), DL-2 CustDev residuals, DL-1 team signals, DL-0 adjacent patterns*
*Synthetic CustDev run: June 4, 2026*
*Next run: after next CustDev block or market scan update*
