# Official Course Map - learn-prompt-engineering-with-phoebe

Research date: 2026-07-17. All syllabi and docs fetched live (4 parallel research passes). Fast-moving area: re-verify vendor docs + changelogs before each delivery.

Two-track course (per Phoebe's directive, applies to all courses):
- **Track A - non-tech** (6 sessions): C-level, board, managers, followers. Thinking mode, asking the right question, working with data/tech people to get ideas realized.
- **Track B - practitioner** (open-ended session count): tools, tech, data. As specific as needed.

Session mapping tables get filled in after arc approval. This file first records the verified source universe, the overlap analysis, and the 2026 framing shifts.

---

## 1. Source universe (verified inventories)

### 1.1 Anthropic (~20-25 h material)

| Source | What it holds | Difficulty | URL |
|---|---|---|---|
| Docs: Prompt engineering overview | Prerequisites funnel: success criteria -> empirical evals -> draft prompt -> only then prompt-engineer | Beginner | platform.claude.com/docs/en/docs/build-with-claude/prompt-engineering/overview |
| Docs: Prompting best practices (consolidated) | ALL classic technique pages merged into one page: clear+direct ("brilliant new employee", golden rule = show prompt to colleague), context+motivation, examples (3-5, `<example>` tags), XML structuring, roles, long context (query after docs = up to +30%), prefill DEPRECATION + 5 migration patterns, tool-use steering tags, adaptive thinking + effort param, agentic systems (state tracking, multi-context-window, subagents, anti-hallucination `<investigate_before_answering>`, anti-slop `<frontend_aesthetics>`) | Int-Adv | platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices |
| Docs: model-specific pages (Fable 5, Sonnet 5, Opus 4.8) | Effort levels, instruction-following changes, grounding progress claims, subagent control, sampling params now rejected (temp/top_p 400 on Sonnet 5) | Advanced | platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-* |
| Docs: Console prompting tools | Prompt generator, templates + {{variables}}, prompt improver (4-step pipeline), test-case generator | Beg-Int | .../prompt-engineering/prompting-tools |
| Docs: Success criteria + evals | SMART criteria; grading taxonomy: exact match, cosine sim, ROUGE-L, LLM Likert/binary/ordinal; "volume over grading quality" | Intermediate | platform.claude.com/docs/en/test-and-evaluate/develop-tests |
| Interactive tutorial (GitHub, 9ch + appendix, ~5-6h) | Ch1 API anatomy, Ch2 clear+direct, Ch3 roles, Ch4 data/instruction separation, Ch5 output format + prefill (LEGACY - flag), Ch6 CoT, Ch7 few-shot, Ch8 hallucinations, Ch9 complex prompts from scratch (4 industry walkthroughs), App: chaining/tools/retrieval | Beg-Adv | github.com/anthropics/prompt-eng-interactive-tutorial |
| anthropics/courses: Real World Prompting (5 nb) | Prompt-engineering process/methodology, medical prompt, call summarizer, support bot | Intermediate | github.com/anthropics/courses |
| anthropics/courses: Prompt Evaluations (9 lessons) | Evals 101 -> code-graded -> classification -> promptfoo (5 lessons incl. model-graded + custom graders) | Int-Adv | github.com/anthropics/courses |
| Claude Cookbooks | metaprompt.ipynb, JSON mode, prompt caching, building_evals, capability + vision notebooks | Int-Adv | github.com/anthropics/claude-cookbooks |
| Anthropic Academy (Skilljar) | API course: eval module BEFORE prompt-eng module (deliberate ordering); AI Fluency 4D framework (Delegation, Description, Discernment, Diligence) - Description = prompting for non-devs | Beg-Int | anthropic.skilljar.com (lesson content login-walled, free) |
| Blog: Best practices for prompt engineering | 9 ordered practices; explicitly demotes XML tags + role prompting as "less necessary with modern models" | Beg-Int | claude.com/blog/best-practices-for-prompt-engineering |

Key verified Anthropic facts:
- docs.anthropic.com -> platform.claude.com (use new URLs); anthropic-cookbook -> "Claude Cookbooks"
- Prefill returns 400 on Claude >= 4.6. Tutorial Ch5 still teaches it - teach as legacy + 5 migration patterns.
- budget_tokens/extended thinking removed -> adaptive thinking + effort (low/med/high/xhigh/max)
- Named shipping snippets reusable as course artifacts: `<default_to_action>`, `<do_not_act_before_instructions>`, `<use_parallel_tool_calls>`, `<investigate_before_answering>`, `<frontend_aesthetics>`

### 1.2 OpenAI + Google (~11-13 h deduplicated)

| Source | What it holds | Difficulty | URL |
|---|---|---|---|
| OpenAI PE guide (rewritten - old six-strategy guide GONE, 301s) | Model selection (reasoning vs GPT), developer/user roles + chain of command, markdown+XML formatting, few-shot, RAG + static-content-first for caching, context budgeting | Beg-Int | developers.openai.com/api/docs/guides/prompt-engineering |
| OpenAI Reasoning best practices | Planners vs workhorses; DO NOT say "think step by step"; zero-shot first, few-shot can HURT reasoning models; explicit success criteria | Int | developers.openai.com/api/docs/guides/reasoning-best-practices |
| GPT-4.1 prompting guide (cookbook) | Agentic 3 reminders (persistence, tool-calling, planning); long-context instructions at BOTH ends; recommended template: Role/Instructions/Reasoning Steps/Output Format/Examples/Context; delimiter ranking (markdown > XML > JSON for long docs) | Int-Adv | developers.openai.com/cookbook/examples/gpt4-1_prompting_guide |
| GPT-5 + GPT-5.1 prompting guides | Agentic eagerness calibration, tool preambles, reasoning_effort + verbosity params, metaprompting, self-reflection rubrics, apply_patch, personality shaping | Advanced | developers.openai.com/cookbook/examples/gpt-5/* |
| Google Boonstra whitepaper (68pp, v4 Feb 2025) | 12 named techniques: zero/one/few-shot, system/role/contextual prompting, step-back, CoT, self-consistency, ToT, ReAct, APE; sampling config chapter; 13 best practices; code prompting | Beg-Adv | kaggle.com/whitepaper-prompt-engineering (LOGIN-WALLED; verified via archive.org mirror) |
| Gemini prompting docs + Gemini 3 | Completion-starter trick, few-shot pushed harder than OpenAI, prompt decomposition/chaining, data first + question LAST in long context (opposite emphasis vs GPT-4.1), "Think very hard", 9-point agentic system-instruction framework | Beg-Adv | ai.google.dev/gemini-api/docs/prompting-strategies |

Terminology divergences worth a dedicated table in the course:
- system prompt (Anthropic) = developer message (OpenAI) = system instructions (Google)
- metaprompting (OpenAI) = APE (Boonstra) = prompt improver (Anthropic Console)
- RAG (OpenAI) = grounding (Google)
- CoT-as-prompt vs thinking-as-feature: all three vendors now say don't prompt step-by-step on reasoning models
- Long-context placement: GPT-4.1 says instructions at both ends; Gemini 3 says data first question last; Claude says query after docs (+30%)
- Sampling params: whitepaper teaches temp/topK/topP; Gemini 3 says leave defaults; Claude Sonnet 5 rejects them; OpenAI reasoning models ignore them

### 1.3 DeepLearning.AI (~20 h across courses; videos login-walled free, syllabi public)

| Course | Length | Unique value | Exec-suitable parts |
|---|---|---|---|
| ChatGPT Prompt Engineering for Developers (Fulford+Ng) | 1h40 | Canonical task taxonomy (summarize/infer/transform/expand), two principles, iterative loop | Guidelines + Iterative concepts |
| AI Prompting for Everyone (Ng, NEW) | 7h04 | THE exec/non-technical prompting course: web search, deep research, thought partner, sycophancy, AI critique, no-code labs | Nearly all - Track A spine |
| Building Systems with ChatGPT API | 1h55 | Prompt -> SYSTEM bridge: chaining, inner monologue, 3-lesson eval arc | Chat format, CoT, chaining concepts |
| Building toward Computer Use with Anthropic | 1h47 | Closest DLAI has to Claude prompting: XML, templates, caching, tool use | Overview + computer use |
| Reasoning with o1 | 1h44 | Reasoning-model prompting is DIFFERENT (4 principles) + 26m metaprompting lesson | Intro to o1 |
| Evaluating AI Agents (Arize) | 2h36 | Most complete modern eval taxonomy: code/LLM-judge/human, router/skill/trajectory evals, monitoring | All non-lab lessons |
| Automated Testing for LLMOps (CircleCI) | 1h12 | Evals in CI - prompt changes as code changes | Intro lessons |
| Red Teaming LLM Applications (Giskard) | 1h29 | Adversarial prompting as eval discipline | Vulnerabilities overview |
| Quality & Safety for LLM Apps (WhyLabs) | 1h59 | Metric-level detection: SelfCheckGPT, injection/refusal monitoring | Thin |
| Building & Evaluating Advanced RAG | 2h05 | RAG Triad: context relevance / groundedness / answer relevance | RAG Triad concept |
| Prompt Eng with Llama 2&3 (Meta) | 2h03 | Open-model specifics, model choice as prompting, Llama Guard | Model overview lessons |
| Prompt Eng for Vision Models (Comet) | 1h32 | Prompting beyond text: SAM coordinates, negative prompts | Overview only |
| Prompt Compression & Query Optimization | 1h49 | Only 17m actually on compression - marginal | - |
| Claude Code: Highly Agentic Coding Assistant | 2h | Agentic-prompting practices (plan-then-act, context mgmt) | "What is Claude Code?" |

No DLAI course named "Prompt Engineering with Claude" exists - do not cite one.

### 1.4 Research + security + evals ecosystem

Foundational papers (teach as lineage, with 2026 status):

| Paper | Status in 2026 |
|---|---|
| CoT (Wei et al. 2022, arxiv 2201.11903) | PARTIAL: concept foundational (internalized into reasoning models via RL); "think step by step" counterproductive on reasoning models; still works on small/non-reasoning models |
| Few-shot / GPT-3 (Brown et al. 2020, arxiv 2005.14165) | PARTIAL: workhorse for format/style on standard models; degrades reasoning models (o1 measurably worse with examples) |
| ReAct (Yao et al. 2022, arxiv 2210.03629) | Architecture yes, prompt no: superseded by native tool calling, but every agent harness runs a ReAct loop internally |
| Self-consistency (Wang et al. 2022, arxiv 2203.11171) | Mostly historical: early test-time compute, absorbed model-side; still a cheap reliability trick |
| Tree of Thoughts (Yao et al. 2023, arxiv 2305.10601) | Largely historical for practitioners; teach as lineage of model-internal search |
| Meta-prompting (Suzgun & Kalai 2024, arxiv 2401.12954) | Evolved into orchestrator/subagent patterns + prompts-that-write-prompts. TERM COLLISION: promptingguide.ai uses "meta prompting" for structure-over-content - pick one definition, note ambiguity |

Security (canonical, current):
- OWASP Top 10 for LLM Apps **2025 edition (v2.0) still current as of Jul 2026** - no 2026 edition. LLM01 = prompt injection. genai.owasp.org/llm-top-10/
- Injection != jailbreak (Willison, Mar 2024): injection attacks the APP (trusted+untrusted concat), jailbreak attacks the MODEL's safety training
- Lethal trifecta (Willison, Jun 2025): private data + untrusted content + external comms = exfiltration; guardrails are not security
- CaMeL / six design patterns (DeepMind 2025, arxiv 2503.18813): architectural defense; consensus = no complete solution, "assume injection succeeds"
- "Add 'ignore malicious instructions' to your prompt" is explicitly NOT a defense

Eval tooling:
- promptfoo (20.6k stars, used in Anthropic's own courses) - OSS evals + red-teaming CLI
- OpenAI Evals (de-emphasized; platform Dashboard evals is current path)
- LangSmith (trace-first, LangChain stacks), Braintrust (eval-first, CI merge gates)
- Anthropic eval docs (grading taxonomy above)

Aggregators:
- promptingguide.ai (DAIR.AI): actively maintained, already has Agents + Context Engineering + Reasoning LLMs sections - structural benchmark
- learnprompting.org: partly dated (intro last updated Oct 2024) - use mainly for Prompt Hacking section

## 2. The six 2026 framing shifts (course MUST reflect)

1. **Reasoning models invert 2023 advice.** No "think step by step", few-shot can hurt, goal+constraints not procedure. New levers: reasoning effort params. Teach a "which model class am I prompting?" decision tree.
2. **Prompt engineering -> context engineering.** Anthropic canonical post (Sep 2025): curate the whole token ecosystem - compaction, note-taking, just-in-time retrieval, subagents. Techniques still work; the standalone job title died. Frame prompting as a layer inside context engineering.
3. **Agentic prompting replaced scaffold prompting.** Native tool calling killed hand-rolled ReAct; the skill is tool descriptions + system prompts for harnesses.
4. **Security is architecture, not prompt wording.** Injection/jailbreak distinction, lethal trifecta, OWASP 2025, defense-in-depth.
5. **Evals are the core practitioner skill.** Prompt changes = code changes needing regression tests. A tips-and-tricks course without evals is obsolete.
6. **Automated prompt optimization emerging** (metaprompting descendants) - a mention, not a pillar.

## 3. Overlap analysis

### 3.1 With sibling courses (cross-link, don't repeat)
- learn-claude-with-phoebe Deep dive 6.2 "Prompt engineering & evals" (~2.5k words, Claude-specific overview) - this course goes deeper; 6.2 links here as "full course"
- learn-ai-literacy-with-phoebe Session 7 "Using GenAI well" (exec: prompting-as-specification, prompt/RAG/fine-tune, eval design) - Track A builds on it; cross-link as prerequisite-ish

### 3.2 Across sources (shared core, teach ONCE + deltas)
Heavily duplicated across all vendors (teach once in fundamentals): clear+direct, few-shot, roles/system prompts, delimiters/structure, output formatting, basic CoT, iterate-empirically.
Per-source deltas worth own coverage: Anthropic (XML idioms, effort, agentic sections, prefill migration), OpenAI (eagerness, preambles, verbosity, metaprompting), Google (completion starter, data-first-question-last, 9-point agentic framework), Boonstra (12-technique naming + sampling params as history).

## 4. Login-walled / unverifiable (flagged, not guessed)
- Skilljar lesson videos/quizzes (free signup) - syllabi public
- DLAI lesson videos (free signup) - syllabi public
- Kaggle whitepaper PDF download (login) - full text verified via archive.org mirror
- OpenAI's old six-strategy guide - gone; needs Wayback if wanted
- Third-party "context engineering survey" stats (82% IT leaders etc.) - no named primary source, DO NOT cite

## 5. Honest "not covered by design" (draft - finalize after arc approval)
- Official vendor certificates/videos stay official (say so on page)
- Vision-model prompting (SAM/diffusion) - out of scope, one pointer
- Fine-tuning / prompt tuning - decision-boundary mention only
- Prompt compression - one paragraph

## 6. Session mapping tables (arc approved 2026-07-17)

Legend: ✓ = taught to the 80% bar · ◐ = partial / pointer only

### Track A - For Leaders (6 x 45 min)

| # | Session | File | Sources covered | ✓/◐ |
|---|---|---|---|---|
| A1 | Prompting is delegation, not magic words | a1-delegation-not-magic.html | AI Fluency 4D (Description module) ✓ · docs "brilliant new employee" + golden rule ✓ · "PE is dead" headlines vs context engineering ◐ | ✓ |
| A2 | Ask the right question | a2-ask-the-right-question.html | Ng Prompt Eng for Devs: two principles + task taxonomy ✓ · blog practices 1-3 (explicit, context+motivation, specific) ✓ · iterative loop ✓ | ✓ |
| A3 | AI as thought partner | a3-thought-partner.html | Ng AI Prompting for Everyone Module 2 (brainstorm, context, reasoning, sycophancy, critique) ✓ · Module 1 (search, deep research) ◐ | ✓ |
| A4 | Judge the output | a4-judge-the-output.html | AI Fluency Discernment ✓ · tutorial Ch8 hallucination concepts (no code) ✓ · blog practice 5 (permission to be uncertain) ✓ | ✓ |
| A5 | From idea to shipped: working with your data/tech team | a5-idea-to-shipped.html | Anthropic success-criteria docs (SMART, business terms) ✓ · evals-as-acceptance-tests concept ✓ · Evaluating AI Agents concept lessons ◐ | ✓ |
| A6 | Risk, safety, strategy | a6-risk-and-strategy.html | Injection vs jailbreak (Willison) plain-language ✓ · lethal trifecta ✓ · OWASP LLM01 awareness ◐ · vendor terminology map ✓ | ✓ |

### Track B - For Builders (10 x 45 min)

| # | Session | File | Sources covered | ✓/◐ |
|---|---|---|---|---|
| B1 | The 2026 map + method | b1-the-2026-map.html | Docs overview funnel (criteria -> evals -> draft) ✓ · Anthropic context-engineering post ✓ · model-class decision tree (reasoning best practices) ✓ · 6 framing shifts ✓ |
| B2 | Core techniques: clarity, structure, examples, roles | b2-core-techniques.html | Tutorial Ch2-4, Ch7 ✓ · consolidated best-practices general principles ✓ · Boonstra zero/one/few-shot + system/role/contextual ✓ · delimiter ranking (GPT-4.1) ✓ · blog demotion of XML/roles honesty ✓ |
| B3 | Output control | b3-output-control.html | Tutorial Ch5 (prefill = LEGACY flag) ✓ · prefill 5 migration patterns ✓ · JSON mode / structured outputs ✓ · verbosity + format matching ✓ · Gemini completion-starter ✓ |
| B4 | Reasoning: CoT lineage to thinking models | b4-reasoning-models.html | CoT/self-consistency/ToT papers as lineage ✓ · OpenAI reasoning best practices ✓ · Reasoning with o1 (4 principles) ✓ · adaptive thinking + effort params ✓ · Gemini "Think very hard" ✓ |
| B5 | Long context + grounding + caching | b5-long-context.html | Placement wars: Claude query-last +30% vs GPT-4.1 both-ends vs Gemini data-first ✓ · document tags + quote-grounding ✓ · RAG vs grounding ✓ · RAG Triad ◐ · prompt caching ✓ |
| B6 | Chaining + agentic prompting | b6-agentic-prompting.html | Prompt chaining + self-correction ✓ · GPT-4.1 3 reminders ✓ · GPT-5 eagerness + preambles ✓ · tool descriptions ✓ · Gemini 9-point agentic framework ✓ · ReAct as architecture ✓ · Anthropic agentic sections (state tracking, subagents, anti-hallucination tags) ✓ |
| B7 | Vendor deltas masterclass | b7-vendor-deltas.html | Terminology divergence table ✓ · model-specific pages (Fable 5 / Sonnet 5 / Opus 4.8 / GPT-5.1 / Gemini 3) ✓ · sampling params history (Boonstra chapter -> params rejected) ✓ · Llama/open-model pointer ◐ |
| B8 | Evals I: from vibes to numbers | b8-evals-vibes-to-numbers.html | Anthropic success criteria + grading taxonomy ✓ · Prompt Evaluations lessons 1-4 ✓ · promptfoo intro ✓ · Building Systems eval arc ✓ |
| B9 | Evals II: LLM-as-judge, CI, agent evals | b9-evals-judge-ci.html | Prompt Evaluations lessons 5-9 (model-graded, custom graders) ✓ · Automated Testing for LLMOps (evals in CI) ✓ · Evaluating AI Agents taxonomy (router/skill/trajectory, monitoring) ✓ · Red Teaming overview ◐ |
| B10 | Security + production | b10-security-production.html | Injection != jailbreak ✓ · lethal trifecta ✓ · OWASP 2025 top items ✓ · CaMeL/design patterns concept ✓ · metaprompting tools (Console improver, metaprompt.ipynb, GPT-5 metaprompting) ✓ · prompts-as-code versioning ✓ |

### Deliberately not covered (say so on the site)
- Official vendor certificates, videos, quizzes - stay official (links provided)
- Vision-model prompting (SAM/diffusion coordinates) - one pointer in B7
- Fine-tuning / prompt tuning - decision boundary mention in B1 only
- Prompt compression - one paragraph in B5
- Hands-on labs against paid APIs are homework-optional; sessions use copy-paste-able prompts runnable in any chat UI
