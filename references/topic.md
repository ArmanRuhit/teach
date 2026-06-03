# TOPIC substrate

Use when the goal is to *understand* a concept or subject — a language feature, an algorithm, a body of theory. Units are concepts to master, not features to build.

## How the slots get filled

- **Unit** — one concept or item (e.g. `dynamic dispatch`, `equals/hashCode` contract, `recursion base case`).
- **Curriculum & order** — a prerequisite chain: **mechanics before judgment** (how something works before when to use it well). If a knowledge-base skill exists, its chapter/topic index usually *is* the order.
- **Baseline (setup)** — the simplest correct mental model of the subject plus one tiny worked example, so the learner has a frame to hang units on.
- **Worked example (step 1)** — a demonstrated instance of the concept. If a knowledge-base skill ships a patterns/examples file, draw the demonstration from it.
- **Challenge (step 2)** — apply the same concept to a fresh, sibling case.
- **Acceptance criteria — tag each unit:**
  - **runnable** — a check the learner can execute: compile/run a snippet, an assertion, a test. (e.g. two equal objects collide correctly in a `HashMap`.) Prefer this whenever the concept *can* be made executable.
  - **review** — judgment against a rule or contract where there's no pass/fail run. (e.g. "your design avoids the fragility this rule warns about.") Here the learning is verified in step-3 review rather than by running.
- **Self-explanation prompt** — the reasoning behind the rule ("why can't return type distinguish overloads?", "why does omitting this break the contract?").
- **Hint ladder** — with a knowledge base: a nudge → its glossary → its cheatsheet → the specific chapter. Without one: graduated conceptual hints from general to specific.
- **Verify** — run the check (runnable units) or assess against the rule (review units).

## Notes

- **Optional artifact.** A conceptual subject becomes more concrete and motivating if one small running model accretes across units (e.g. a tiny banking or library domain that each new concept extends). When useful, borrow the BUILD baseline idea — a minimal running thing — and grow it concept by concept.
- **Example wiring — a `java-oop` knowledge-base skill:** units from its chapter index (mechanics `ch06`→`ch09`, then judgment `ej-ch03`→`ej-ch04`); worked examples from its `patterns.md`; acceptance criteria from its `cheatsheet.md` and the documented contracts, each tagged runnable (e.g. `equals`/`hashCode`) or review (e.g. "prefer composition over inheritance"); hint ladder glossary → cheatsheet → chapter; verify by running a small class for runnable units, or reviewing the design for review units.
- Web-search current/version-sensitive facts when no knowledge base covers them.