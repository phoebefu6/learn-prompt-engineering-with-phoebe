# Presenter notes - Builder track (b1-b10)

Instructor-only. Shared shape: 0-3 welcome, 3-20 concepts (Live cards), 20-42 build-along, 42-45 Q&A. TriageBot is the spine - every session ends with a better TriageBot; keep a running doc with each version so late joiners can catch up.

## Preflight (every session)
- Projector zoom ON. A chat UI or API playground open. The 10 Meridian sample tickets handy (make them once, reuse all track - include one multi-issue, one rage-caps, one with an order number, one policy-gap case).
- Re-verify model-specific claims against live vendor docs if >1 month since 2026-07 (this field breaks course content fast: prefill 400s, param rejections, new model pages).

## B1 - The 2026 map
- Run: welcome (track shape + TriageBot) 4' · criteria-before-prompts funnel 5' · context engineering 5' · model-class decision tree 6' · six shifts 3' · build-along (criteria + v0 + v0.1) 18' · Q&A 4'.
- Never cut: the decision tree; writing success criteria BEFORE any prompt (the discipline the whole track stands on).
- Trap: practitioners want techniques NOW. Promise b2, hold the line on criteria first.

## B2 - Core techniques
- Never cut: data/instruction separation with delimiters; the few-shot A/B on real tickets.
- Cut if long: the OpenAI template tour (point at the card).
- Demo beat: show format-mirroring - ask the same question in sloppy vs structured form.

## B3 - Output control
- Never cut: schema vs "please return JSON" contrast; the NEEDS_HUMAN flag pattern (anti-guessing).
- Honesty beat: prefill was official Anthropic teaching, now a 400 error - "your skills need changelogs" is the session's meta-lesson.

## B4 - Reasoning models
- Never cut: the inversion table (2023 vs 2026 advice side by side); the easy/hard ticket routing decision.
- Trap: cargo-cult effort settings. Say: effort is a budget dial, measure before maxing.

## B5 - Long context + grounding
- Never cut: the three-vendor placement table; quote-grounding ("extract the policy lines first").
- Demo beat: the POLICY_GAP ticket - watching it refuse to improvise is the payoff.

## B6 - Agentic prompting
- Never cut: the three reminders (persistence, tool-calling, planning); tool descriptions ARE prompts.
- Cut if long: Gemini 9-point framework (name it, link it).
- Paper dry-run works better than a live agent here - the loop on a whiteboard beats a flaky demo.

## B7 - Vendor deltas
- Never cut: the terminology table; "models are not drop-in replacements" with one concrete delta per vendor.
- Fast-moving session: re-verify EVERY model-specific claim before presenting. If a claim died, teach the death - it proves the session's point.

## B8 - Evals I
- Never cut: golden-set assembly as a team exercise (this is the build-along, do not shortcut it); volume-over-grading-quality principle.
- Trap: perfectionism on labels. 20 ok labels today beat 100 perfect labels never.

## B9 - Evals II
- Never cut: binary-beats-Likert for judges; the simulated bad PR caught by the gate (the track's best aha).
- Cut if long: judge-bias list (keep position bias, drop the rest to self-study).

## B10 - Security + production
- Never cut: injection vs jailbreak distinction; the injection canary ticket ("ignore previous instructions...") added to the eval suite; the trifecta audit on TriageBot itself.
- Tone: honest that this is the least-solved area - "assume injection succeeds" is engineering humility, not defeatism.
- Close the track: the v0-to-shipped recap, then send leaders in their lives to a5/a6.
