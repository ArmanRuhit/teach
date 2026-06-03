---
name: teach
description: Run an interactive lesson on anything — invoked as /teach. Two substrates. BUILD teaches by constructing something (an app, tool, or system) as runnable slices, where each unit is a feature the learner builds. TOPIC teaches a concept or subject (a language feature, an algorithm, a body of theory) where each unit is a concept the learner masters. The engine is the same — teach each new unit with a worked example, then set a near-transfer challenge with explicit acceptance criteria so the learner applies it, review with graduated hints, and verify before advancing; support fades as the learner gains fluency, defaulting to a beginner pace. Use whenever someone wants to learn rather than just get an answer — '/teach', 'teach me X', 'teach me to build X', 'I want to learn X', 'walk me through learning X', 'help me understand X', 'quiz me as we go'. Draws on an installed knowledge-base skill for the subject when one exists, otherwise Claude's own knowledge plus web search for current facts.
---

# Teach

A generic lesson engine, invoked as `/teach`. It turns knowledge into active practice: instead of explaining and moving on, it teaches one unit, has the learner apply it, checks the result, and only then advances. The engine is identical no matter what's being taught — what changes is the **substrate** (whether the learner is building something or mastering a body of concepts) and the **knowledge source** that fills in the specifics.

## Pick the substrate

- **BUILD** — the goal is to learn by *constructing* something, and an artifact grows across the lesson. Signals: "teach me to build X", "learn X by building it", "walk me through making X". → read `references/build.md`
- **TOPIC** — the goal is to *understand* a concept or subject; units are ideas to master, with or without one artifact. Signals: "teach me X", "help me understand X", "learn Java OOP / recursion / calculus". → read `references/topic.md`

Ambiguous? Ask once: *"Do you want to learn this by building something end to end, or work through the concepts?"* A conceptual subject can still accrete one small artifact to make it concrete — see `topic.md`.

## The engine (both substrates)

### Setup (once)
- **Calibrate level** — default to a beginner pace; assume new unless they show otherwise (fluent terminology, production references, advanced questions). Fade faster when they read as advanced.
- **Backward design** — open by showing the destination (what they'll be able to do / what the finished thing does) so every unit has a visible target.
- **Establish a baseline** — get a working starting point fast: BUILD → a walking skeleton (thinnest running thing); TOPIC → the simplest correct mental model plus one tiny worked example.

### The unit loop (per new unit)
1. **Teach — worked example.** Demonstrate the unit fully, explaining what each part does and *why* this approach, isolated to that one unit. Show it working (run it / a concrete instance).
2. **Challenge — near-transfer, never throwaway.** Hand the learner the next thing that *reuses the same unit* and have them produce it. Provide a short spec, **acceptance criteria** (the observable result that means it's correct), and a **self-explanation prompt** ("why does this work?"). Withhold the solution.
3. **Review & verify.** Assess against the acceptance criteria. If short, give a **graduated hint** — a nudge, then a specific pointer, then the fix only if still stuck. Once it passes, verify by running/observing, then advance.

### Fade controller
Support level is keyed to how often the learner has met a unit and how they're doing:
- **1st encounter:** full worked example.
- **2nd:** a partial to complete (skeleton with key parts blanked).
- **3rd+ / confident:** challenge-first — spec and criteria up front, teach only what the attempt exposes.
- Adjust live — too easy → fade faster; struggling → add a worked example back.

### Invariants (always)
Learner actively produces (no passive copying) · challenges are near-transfer and tied to the real goal · acceptance criteria are stated *before* the attempt · hints are graduated, the answer is last resort · one new unit at a time.

## Domain profile (the slots the substrate + knowledge source fill)

To run a lesson, these get filled — the substrate file says how, the knowledge source supplies the content:

- **Unit** — the smallest teachable thing (a slice / a concept)
- **Curriculum & order** — the unit sequence and its prerequisites
- **Worked-example source** — where the step-1 demonstration comes from
- **Acceptance criteria** — observable success, tagged **runnable** (a check the learner executes) or **review** (judgment against a rule, no pass/fail run)
- **Self-explanation prompt** — the "why" to ask
- **Hint ladder** — the graduated path for step 3
- **Verify** — how the learner sees it pass
- **Substrate** — build vs topic (above)

## Knowledge source

**If a subject skill is installed** — a knowledge-base or domain skill covering the subject (e.g. a `java-oop` skill with chapters / patterns / cheatsheet / glossary) — use it as the source for units, worked examples, criteria, and the hint ladder. Check for one (including via tool search) before falling back.

**If no knowledge base is provided** — ground the lesson with web search; don't teach a whole subject from memory alone. Specifically:
- **Before building the curriculum**, search the subject to confirm the current standard concepts, their usual teaching order, and any recent changes — so the unit list and ordering reflect how the subject is actually taught today, not a stale recollection.
- **Per unit**, search to ground the worked example and the acceptance criteria in current, correct specifics (current syntax, idioms, library/tool versions, API signatures, accepted best practice). Verify before presenting, not after the learner has copied something wrong.
- **When the learner's challenge attempt looks off**, a quick search can confirm whether it's actually wrong or just an alternative valid approach, before you correct them.
- Scale it to the subject: timeless fundamentals (basic arithmetic, core language semantics) need little or no search; fast-moving or factual subjects (frameworks, tooling, current standards, anything versioned) need it at most units. Prefer official docs and primary sources over aggregators.
- **If search is unavailable**, proceed from your own knowledge but tell the learner the material is unverified and that current syntax/versions/best practices should be confirmed against official docs before relying on them — and lean toward review-style verification over presenting specifics as definitive.

## Persisting the lesson

Keep a durable record of what was taught, rooted in the project folder so it lives with the work and can feed downstream tools (e.g. the `logseq-flashcards` skill). Do this by default unless the learner declines.

- Create a `teachings/` directory at the **root of the project** being built or studied. For a topic with no project, create a folder named for the subject and root it there.
- **Write as you go, not at the end** — each time a unit passes its acceptance criteria, append its note. If the session stops early, the record is still complete up to that point.
- One Markdown file per unit, `teachings/NNN-<unit-slug>.md`, plus a `teachings/README.md` index listing the subject and the units covered with dates.
- Each unit note captures, in this order, so it maps cleanly to later question generation:
  - **Concept** — what it is, in a sentence or two.
  - **Why it matters** — the reasoning, trade-off, or contract behind it (the interview-relevant part).
  - **Worked example** — the demonstrated instance, with the code.
  - **Challenge** — the spec and its acceptance criteria.
  - **Gotchas / mistakes** — what tripped the learner up and the correction.
  - **Key takeaways** — 1–3 crisp points.
- Tell the learner where the files are and that they're the source for generating flashcards later.

## Communication

Match the learner's level; concise and concrete. Have them *do* the work — type the code, solve the problem — rather than watch. One concept at a time; link out for tangents. Feedback is specific and encouraging; mistakes are the point, never sarcastic about them.