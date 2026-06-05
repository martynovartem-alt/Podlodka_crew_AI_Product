# CLAUDE.md

This file provides product and team context for AI-assisted hypothesis discovery work. It is not a code project — it is a product strategy document. Read it to understand who the user is, what they've already validated, and what they're trying to figure out next.

---

## Product context

**Product:** AI Augmentation Platform for bank IT teams
**What it does:** Identifies high-friction roles inside banks and ships AI tools that reduce manual time waste in those roles — without replacing people, augmenting their output.
**Stage:** Post-MVP on two shipped products; entering next hypothesis discovery cycle.
**Domain:** Russian/CIS bank IT departments — QA, analytics, business analysis, chatbot/IVR teams.

### Who I am

Product builder doing AI transformation inside banks. I find roles with measurable time waste, validate the pain, and ship lightweight AI tools (chatbots, agents, multiagent pipelines). Current focus: discovering the next role to augment after two proven cases.

**My technical profile:** Low-code / prompt engineering. I design solutions, write prompts, and configure tools — I don't write production code. Developers handle implementation.
**Tenure:** Less than a year embedded — still building trust. Interview access to new teams is not free; requires relationship effort or a warm intro.

### Target customer

**Role:** Team leads and heads of IT sub-departments inside the bank (support ops, analytics, chatbot/IVR teams).
**Context:** Teams of 5–30 people, sprint-based delivery, clear velocity metrics. Decision to try a tool is made at team lead level; budget approval goes to department head.
**Pain pattern:** Repetitive, rule-based, or lookup-heavy subtasks that consume 15–30% of sprint capacity — tasks the role considers "not real work" but has no time to automate.

### Engagement model

- **Internal team** — embedded inside one bank, not an external vendor
- **Funding:** Internal IT budget / cost center — no sales cycle, no external pricing
- **Access:** <1 year tenure — access to new teams requires trust-building; not all interview slots are easy to get
- **Team:** Product owner (me, prompt/low-code) + 1–2 developers (dedicated full-time)
- **AI stack:** Dual — external APIs (OpenAI / Anthropic) for prototyping; self-hosted open-source LLM (LLaMA / Mistral family) for production. Quality gap is real and significant. Always validate the hypothesis on the internal model before committing — structured tasks (RegExp, SQL) degrade less than reasoning-heavy or long-context tasks.

### How hypotheses are discovered

1. Market research — track how AI tools are changing specific role workflows externally (e.g. new tooling releases, role-specific AI adoption)
2. Interviews — go to the team, map their workflow, find where time is actually spent

### Hard constraints

- **No sensitive personal data** — don't build on PII, transaction data, or credit history
- **Augment, don't replace** — tools must make existing people more productive; headcount-reduction framing is off the table (see DL-2 for why this also fails technically)

---

## Shipped products (already validated, not hypotheses)

### DL-0 — RegExp Auto-Generator for chatbot scenario writers
- **Who:** Scenario writers building NLU training data for bank chatbots/IVR
- **Pain:** Writing RegExp patterns for intent matching consumed ~30% of sprint time
- **Solution:** LLM-assisted RegExp generation from natural language intent description
- **Result:** 30% sprint time recovered for scenario writers
- **Status:** Shipped ✓

### DL-1 — Text→SQL multiagent system for data analysts
- **Who:** Bank data analysts running ad-hoc queries for business stakeholders
- **Pain:** Ad-hoc SQL requests consumed ~20% of sprint time; analysts are bottleneck for business
- **Solution:** Plan-Execute multiagent pipeline — LLM writes SQL from natural language, validates, executes
- **Result:** Analytics team capacity expanded by ~20% per sprint
- **Status:** Shipped ✓

---

## Current objective

**Hypothesis discovery phase.** Find the next bank IT role where:
- There is a repetitive, measurable subtask consuming ≥15% of sprint time
- The subtask is rule-based or lookup-heavy (good AI fit)
- The team lead has pain awareness and can approve a pilot

**Validation timeline:** 2–4 weeks per hypothesis — 1–2 synthetic CustDev sessions first, then 3–5 real interviews to confirm or kill.

**Candidate roles — ranked by evidence × access (market scan done June 2026):**

| Role | Access | External evidence | Key metric | Rank |
|---|---|---|---|---|
| Data analysts (same team as DL-1) | **Have access** | DL-1 already shipped here | SQL pain solved; remaining pain = dashboards, Excel reports, analysis commentary | **#1** |
| Chatbot scriptwriters | **Have access** | None external — DL-2b internal signal | 20% sprint waste confirmed | **#2** |
| QA engineers | No access yet | Strong — named pain "script fatigue" | State Street: 67% cut; DBS: 20 days → 1 | **#3** |

*Ranking logic: access is the binding constraint at <1 year tenure. QA has the strongest external evidence but no relationship — needs trust-building first. BA and scriptwriters can be interviewed now.*

**Note on Scrum Masters:** Removed — they don't exist as a distinct role in this bank. Team leads double as SMs. The sprint reporting pain (30–120 min/sprint) is real but falls on team leads, not a separate role. Could surface as a secondary pain during team lead interviews.

**Market scan findings (June 2026):**
- QA "script fatigue" is a documented, named pain across Citi, HSBC, NatWest, Lloyds, Wells Fargo, DNB. AI-generated code is outpacing QA validation — 70–80% of devs use AI coding tools, QA adoption under 50%.
- Data analysts (DL-1 team): "Business analyst" in this bank = analytics role (SQL, dashboards, Excel) — NOT a requirements-writing BA. Same team as DL-1. SQL pain is already solved. Remaining pain is dashboard creation, Excel report generation, analysis commentary writing. This is an extension hypothesis, not a fresh role.
- Chatbot scriptwriter augmentation has zero published case studies externally. Either untapped or not yet done publicly.
- Roles out of scope: Data engineers (context-heavy, same failure mode as DL-2), Security/Antifraud (different department).

**→ Next actions:**
- **Done:** Market signal scan (June 2026)
- **Next:** Pick data analysts (DL-1 extension) or scriptwriters → run `skill-hypothesis-check.md` → open DL-3
  Suggested: Data analysts — existing relationship, SQL solved, now find the next bottleneck (dashboards / Excel / commentary)

**Out of scope:** DevOps/SRE/infrastructure roles; Security/Antifraud — separate department, no access.

See `## Decision Log` below for DL-2 (killed) and DL-2b (parked residual signal).

---

## Workflow (the core loop)

**One-time setup** *(already done for this product):*
- Fill in `CLAUDE_template.md` for a specific product → save as `CLAUDE.md`

**Per hypothesis cycle:**
0. **Generate candidates** using `skill-hypothesis-generating.md` — pull signals from market, CustDev, and product data → get a ranked list of 5–10 candidate hypotheses
1. Run the top candidate through `skill-hypothesis-check.md` → get a structured hypothesis + ICE score
2. Run a synthetic CustDev session using `skill-synthetic-custdev.md` → surface objections before real interviews
3. **Targeted market scan** using `skill-market-scan.md` → deep report on the specific hypothesis: TAM, players, trends, gaps — all with sources (different from step 0 — this is narrow, not broad)
4. Record the outcome in `skill-decision-log.md` → one `DL-N` entry per hypothesis cycle
5. Paste the DL-N entry into the `## Decision Log` section of `CLAUDE.md` → so the next session inherits context

One full cycle is ~3 hours. The loop is closed when the DL entry lives in `CLAUDE.md`.

## Files and their roles

| File | Role |
|---|---|
| `CLAUDE_template.md` | Product context template — fill this in per product and rename to `CLAUDE.md` |
| `skill-hypothesis-generating.md` | Generates hypothesis candidates from 3 sources (market, CustDev, product data) → prioritized list ready for hypothesis-check |
| `Hypotheses_WW_YY.md` | Output of each hypothesis-generating run — one file per week (e.g. `Hypotheses_23_26.md`). Latest: `Hypotheses_23_26.md` |
| `skill-hypothesis-check.md` | Structures a raw idea into a testable hypothesis + ICE (1–10) + go/pivot/stop criteria |
| `skill-synthetic-custdev.md` | Turns Claude into a specific ICP persona for a practice interview session |
| `skill-market-scan.md` | Produces a structured market report: TAM, players, trends, gaps — all with sources |
| `skill-decision-log.md` | Template for recording what was tested, what was learned, and what the next step is |

## Using the skill files

Each `skill-*.md` contains a ready-made prompt block (marked with ` ``` `). Copy the prompt, fill in the `{placeholders}`, and paste into Claude. No installation required.

`skill-synthetic-custdev.md` works best when you give the persona 3–5 concrete personal details and an explicit pain. If the persona agrees with everything, the role is underspecified — add more friction.

`skill-market-scan.md` requires a tool with web search (Perplexity, Claude with web search, EXA, or Tavily). Without live search, AI will hallucinate market figures.

## Decision Log convention

Entries follow the format `DL-{N}`. Each entry must include a citation (quote or data point) — entries without evidence are not valid. **Exception:** parked hypotheses (not yet tested) may appear without evidence but must be labeled as untested. After each cycle, paste the new `DL-N` entry into the `## Decision Log` section below so future sessions see what was already tested.

---

## Decision Log

### DL-0 — RegExp Auto-Generator for chatbot scenario writers (Shipped)
**Hypothesis:** Scenario writers will recover ≥15% sprint capacity if given LLM-assisted RegExp generation from natural language intent descriptions.
**Test method:** Production deployment + sprint velocity measurement with full scenario-writing team.
**Evidence:** "30% sprint time recovered for scenario writers" — team lead estimate post-ship, not formally tracked. Directionally reliable, not independently verified.
**Decision:** Green — shipped and running. ✓

### DL-1 — Text→SQL multiagent system for data analysts (Shipped)
**Hypothesis:** Data analysts will expand sprint capacity if ad-hoc SQL requests are handled by a Plan-Execute LLM pipeline instead of manual query writing.
**Test method:** Production deployment + capacity measurement with full analytics team.
**Evidence:** "Analytics team capacity expanded by ~20% per sprint" — team lead estimate post-ship, not formally tracked. Directionally reliable, not independently verified.
**Decision:** Green — shipped and running. ✓

### DL-2 — Vibe coding tool for chatbot scriptwriters (Killed)
**Hypothesis:** Giving scriptwriters a vibe coding tool (Kilo Code) lets them stop writing code manually → non-technical hires replace expensive code-savvy people.
**Test method:** Several in-depth interviews + live pilot with one scriptwriter on Kilo Code.
**What we learned:**
1. Vibe coding tools perform poorly on context-heavy codebases, writing new functions, and consistent output quality.
2. Catching tool mistakes still requires understanding code — the skill requirement doesn't disappear.
3. Core assumption (non-technical person can own the output) is false with current tooling.
**Evidence:** "Catching tool mistakes still requires understanding code" — confirmed in live pilot.
**Decision:** Red — killed. Headcount-replacement angle is invalid with current AI tooling.

### DL-2b — Augment scriptwriters on script fixes (Parked — not yet tested)
**Hypothesis (untested):** Existing scriptwriters can recover the confirmed 20% sprint waste on script fixes if given AI augmentation tools adapted to their codebase context — without requiring non-technical replacement hires.
**Why parked:** After DL-2 was killed, focus shifted to discovering new roles. The augmentation (not replacement) angle was never tested.
**Residual signal:** 20% sprint waste on script fixes is confirmed real (from DL-2 interviews).
**Reactivate if:** No high-signal new role is found in current discovery cycle, or scriptwriters surface this pain unprompted in follow-up contact.
