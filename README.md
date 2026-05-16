# Synapse — Adaptive Learning System Prompt
### A ReAct-Inspired Tutor Prompt for Gemini Custom Gems

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Optimized for Gemini](https://img.shields.io/badge/Optimized%20for-Gemini%20Gems-blue)](https://gemini.google.com)
[![Inspired by ReAct](https://img.shields.io/badge/Inspired%20by-ReAct%20Framework-green)](https://arxiv.org/abs/2210.03629)

---

## What This Is

Synapse is a system prompt designed for **Gemini Custom Gems** that turns Gemini into an adaptive learning coach — not a reactive encyclopedia.

Most AI tutors answer immediately, explain everything at once, and move on. Synapse does the opposite. It reasons about what you actually need, maps the right learning path, detects misconceptions, and teaches progressively — from intuition to mastery.

It is built on two foundations:

1. **The ReAct framework** (Yao et al., 2023) — a paradigm where reasoning and acting are interleaved, rather than separated. Instead of just generating answers, the model thinks through what to do, does it, observes the result, and adapts. Applied to tutoring, this means Synapse reasons about your goal before teaching, not after.

2. **Cognitive science principles** — scaffolding, active recall, spaced repetition, deliberate practice, metacognition, and the Feynman technique inform how the prompt structures learning progression.

---

## Why It Exists

Standard AI tutor prompts have two failure modes:

- **Too passive** — they answer whatever is asked without understanding why it was asked
- **Too rigid** — they follow a fixed teaching script regardless of what the learner actually needs

Synapse was designed through multiple review and iteration cycles, cross-model critique (Claude + ChatGPT), and a deliberate merge of two independently reviewed prompts — one focused on adaptive onboarding architecture, the other on pedagogical depth.

The result is a prompt that adapts to the learner's goal, mode, and pace — not just their topic.

---

## Features

- **Confidence-based routing** — high, moderate, and low confidence in learner intent each trigger different response behaviors
- **Interaction mode detection** — concept teaching, homework help, exam prep, practice drilling, strategic thinking, brainstorming, critique, and research modes
- **Structured onboarding** — orients the learner, extracts their real goal, and suggests 2–3 relevant learning paths before diving in
- **Progressive teaching model** — intuition → mechanism → formal explanation → application → edge cases → limitations
- **Misconception handling** — detects flawed reasoning and guides correction constructively
- **Metacognitive coaching** — helps learners monitor their own understanding and choose effective study strategies
- **Escape hatch** — skips the protocol entirely for direct, specific questions
- **Execution bias** — prevents conversational deadlock by favoring forward momentum over endless alignment

---

## How to Use

1. Open [Google Gemini](https://gemini.google.com)
2. Go to **Gems** → **Create a Gem**
3. Paste the contents of `prompt.md` into the **Instructions** field
4. Name your Gem (suggested: **Synapse**)
5. Save and start a learning session

> **Tip:** Start with a broad subject ("I want to learn machine learning") to trigger the full onboarding protocol, or ask a specific question ("What is gradient descent?") to get a direct answer.

---

## Files

| File | Description |
|---|---|
| `prompt.md` | The full Synapse system prompt, optimized for Gemini Gems |
| `README.md` | This file |

---

## Theoretical Foundation

This prompt is directly inspired by the **ReAct** paradigm introduced in:

> Yao, S., Zhao, J., Yu, D., Du, N., Shafran, I., Narasimhan, K., & Cao, Y. (2023).
> **ReAct: Synergizing Reasoning and Acting in Language Models.**
> *Published at ICLR 2023.*
> [https://arxiv.org/abs/2210.03629](https://arxiv.org/abs/2210.03629)

ReAct showed that interleaving reasoning traces with actions — rather than separating them — produces more grounded, interpretable, and accurate behavior in language models. Synapse applies this principle to tutoring: the model reasons about learner intent before acting on it, and adapts based on what it observes from the learner's responses.

---

## ⚠️ Known Limitations of AI-Assisted Learning

This section is important. Understanding these limitations helps you use Synapse more effectively and set realistic expectations.

---

### 1. Context Window Degradation (~20+ Messages)

This is the most critical limitation for learning sessions.

Current LLMs — including Gemini — do not have persistent memory within a conversation the way humans do. They operate on a **context window**: a fixed-size buffer of the recent conversation that the model can "see" at any given time.

In practice, this means:

- **Early in a session (messages 1–10):** The model follows the system prompt closely. Onboarding, mode detection, and misconception handling work as intended.
- **Mid-session (messages 10–20):** Instruction adherence begins to drift. The model may start simplifying its behavior, skipping diagnostic questions, or defaulting to direct answers even when the protocol calls for guided exploration.
- **Late-session (messages 20+):** The system prompt instructions are increasingly diluted by the volume of conversation history competing for attention in the context window. The model may lose track of the learner's stated goal, repeat earlier explanations, or abandon the teaching structure entirely.

**What this means for you:** For deep learning sessions, treat each conversation as a focused sprint of roughly 15–20 exchanges. Start a new conversation for a new topic or when you feel the quality degrading.

---

### 2. Hallucination Risk Increases Over Long Sessions

As conversations grow longer, the model's grounding in factual accuracy weakens. This mirrors a failure mode documented in the ReAct paper itself — where models without external verification generate plausible-sounding but incorrect reasoning traces.

Specific risks in long learning sessions:

- **Confident wrongness** — the model may state incorrect facts with the same tone it uses for correct ones
- **Fabricated examples** — invented case studies, statistics, or citations that sound real
- **Reasoning drift** — logical chains that start correctly but gradually introduce subtle errors the learner may not catch

**What this means for you:** Treat AI-generated factual claims as a starting point, not a source of truth. Cross-verify important facts, especially in technical, scientific, or historical subjects. The model is better at reasoning *about* knowledge than reliably *storing* it.

---

### 3. Repetitive Loop Behavior

In extended conversations, LLMs can enter behavioral loops — a failure mode explicitly identified in the ReAct paper (categorized as "reasoning error"). Signs include:

- Repeating the same explanation in slightly different words
- Asking the same clarifying question multiple times
- Cycling between two approaches without making forward progress
- Restating what was already covered instead of building on it

This happens because the model loses track of what it has already done and defaults to familiar patterns from earlier in the conversation.

**What this means for you:** If you notice the session going in circles, explicitly redirect: *"We already covered that — let's move to the next concept"* or simply start a fresh conversation.

---

### 4. No True Memory Across Sessions

Gemini Gems do not retain memory between separate conversations. Every new session starts from zero — the model has no recollection of:

- what topics you have covered
- misconceptions you have previously corrected
- your demonstrated knowledge level
- the learning path you were following

This makes long-term curriculum building difficult without external note-taking on your part.

**What this means for you:** Keep a personal learning log. At the end of each session, ask the model to summarize what was covered, what your current gaps are, and what to study next. Paste that summary into your next session to restore context.

---

### 5. Instruction Drift on Weaker Models

Synapse was designed and tested with Gemini 1.5 Pro and Gemini 2.0 in mind. On smaller or less capable model variants, the multi-step protocol may not be followed reliably. Specifically:

- The escape hatch may be ignored and onboarding triggered unnecessarily
- Confidence-based routing may default to always answering directly
- Misconception detection may be skipped in favor of moving forward
- The teaching progression (intuition → formal → application) may collapse into a single explanation

**What this means for you:** Use the most capable model version available. If the protocol seems to be ignored, try explicitly naming the mode: *"Use guided learning mode"* or *"Walk me through this step by step."*

---

### 6. Cannot Replace Spaced Repetition or Retrieval Practice

A single AI conversation, however well-structured, cannot replicate the learning gains from:

- **Spaced repetition systems** (Anki, Supermemo) — revisiting material at scientifically optimal intervals
- **Active retrieval practice** — testing yourself without looking at notes
- **Interleaved practice** — mixing multiple topics to prevent over-reliance on pattern matching

Synapse can recommend these techniques and coach you toward them. It cannot implement them for you across sessions. Use dedicated tools alongside this prompt for long-term retention.

---

### 7. Socratic Method Has Limits Without Real Feedback

Synapse is designed to ask diagnostic questions and assess your understanding. But it can only evaluate what you type. It cannot:

- detect whether you truly understood or just paraphrased correctly
- observe your problem-solving process in real time
- catch reasoning errors you make silently and never express
- provide the accountability of a human tutor

The model will give you the benefit of the doubt. Push back against it. If it accepts your answer too easily, say *"Challenge me more"* or *"What's wrong with my reasoning?"*

---

## Best Practices for Long Learning Sessions

Given the limitations above, here is how to get the most out of Synapse:

**Session length** — keep focused sessions to 15–20 exchanges. Quality degrades after that.

**Session recap** — end each session by asking: *"Summarize what we covered, what my weak areas are, and what I should study next."*

**Session start** — paste your previous recap at the start of the next session to restore context.

**Fact verification** — cross-check factual claims on important subjects, especially in technical domains.

**Explicit redirection** — if the model loops or drifts, name it directly and redirect.

**Complement with tools** — use Anki for spaced repetition, a notebook for concept maps, and practice problems from external sources.

---

## Version History

This prompt was not designed in one sitting. It went through multiple review cycles across different AI models, each round exposing new failure modes and architectural gaps.

### v0.1 — Original Draft (Prompt Engineer via ChatGPT)
The first version was built with ChatGPT as a general-purpose adaptive learning and reasoning system. It introduced the core idea of goal-before-explanation and a 6-phase onboarding protocol (ASOP). Solid philosophy, but architecturally rigid — no escape hatch, no execution bias, no handling for direct questions or mid-conversation topic shifts. The protocol ran the same way regardless of whether the user's intent was clear or ambiguous.

### v0.2 — First Review (Claude)
Claude reviewed v0.1 and identified the main structural problems:
- No escape hatch for users who just want a direct answer
- Phases 4 and 5 overlapped and caused redundancy
- Phase 3 listed 10+ learning paths, creating the same overload it was designed to prevent
- No mid-conversation handling for follow-up questions vs. genuine new topics
- Style goals (concise, no filler) conflicted with the protocol's verbosity

### v1.0 — First Rewrite (Claude)
Claude rewrote the prompt with all review fixes applied:
- Escape hatch added as the first instruction
- Phases reduced from 6 to 5 by merging exploration and confirmation
- Learning paths capped at 2–3 options
- XML-style semantic phase tags added for clearer boundaries
- Mid-conversation handling explicitly defined
- Execution bias introduced to prevent alignment loops

### v1.1 — Second Review (Prompt Engineer via ChatGPT)
The v1.0 rewrite was submitted to ChatGPT for critique as part of a cross-model evaluation. The prompt engineer reviewed the output, assessed which findings were valid, and identified the remaining weaknesses worth addressing:
- "Intent is unclear" still underspecified — no explicit trigger conditions
- Binary onboarding (either run it or don't) too crude — needed confidence tiers
- No formal interaction mode architecture (factual, tutoring, strategic, brainstorming, etc.)
- No in-session learning state tracking
- Weak misconception handling — exploration-oriented but not diagnostic
- Risk of conversational deadlock from over-cautious alignment behavior
- Tone adaptation too loose — risk of mimicry reducing clarity

Not all of ChatGPT's critique was accepted. Points around mastery loops and retrieval architecture were evaluated and set aside as out of scope for a system prompt — a judgment call made by the prompt engineer, not the model.

### v1.2 — Gemini Gems Prompt Review (Claude)
A separate Gemini-specific tutor prompt was submitted for review. Claude assessed it independently and found:
- Stronger pedagogical depth than v1.0 — better teaching progression, feedback system, and metacognitive coaching
- Weaker onboarding architecture — no escape hatch, no confidence routing, no execution bias
- "Hidden learning roadmap" instruction unreliable — models ignore or partially surface it
- No formatting guidance for Gemini's markdown rendering
- Goal inference too passive — would cause Gemini to proceed on assumptions

### v2.0 — Merged Final Version (Claude) — *Current*
Claude merged the onboarding architecture from v1.0 with the pedagogical intelligence from the Gemini prompt, applied all fixes from v1.1, and optimized the entire system for Gemini Custom Gems:
- XML tags removed, replaced with plain markdown for Gemini compatibility
- Confidence-based routing added (high / moderate / low)
- Explicit ASOP trigger and skip conditions defined
- Formal interaction mode table added
- Teaching progression model integrated (intuition → mechanism → formal → application → edge cases → limitations)
- Misconception handling given its own dedicated section
- Feedback system and metacognitive coaching merged in from Gemini prompt
- Learning roadmap made visible to the learner instead of silent
- Periodic state surfacing added instead of silent tracking
- Tone constraint tightened — adapts to learner but maintains professionalism
- Execution bias strengthened throughout

---

## License

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

This project is licensed under the MIT License — free to use, modify, and share with attribution. See the [LICENSE](LICENSE) file for details.

---

## Contributing

Issues, improvements, and alternative versions are welcome. If you test this on other models (Claude, GPT-4, Mistral) and find meaningful differences in behavior, open an issue describing what changed and why.

---

## Acknowledgements

Prompt architecture inspired by the ReAct framework (Yao et al., 2023). Pedagogical structure informed by cognitive science literature on scaffolding, deliberate practice, and metacognitive learning. Iterative design and review conducted with Claude (Anthropic) and ChatGPT (OpenAI).
