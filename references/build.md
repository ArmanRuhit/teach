# BUILD substrate

Use when the lesson goal is to learn by *constructing* something — an app, tool, or system — where one artifact grows across the lesson. This is a **compact** build method, sized for learning, not shipping.

## How the slots get filled

- **Unit** — a vertical slice: one feature taken end-to-end (entry point → logic → data → result).
- **Curriculum & order** — start with a **walking skeleton**, then slices ordered by *visible capability*, not by horizontal layer. Earliest slices are the most important path.
- **Baseline (setup)** — the walking skeleton: the thinnest end-to-end thing that runs. Web app → a page loads; API → one endpoint returns stubbed JSON; CLI → one command prints something; mobile → one screen on the simulator. Running from minute one; everything after only *thickens* a slice.
- **Worked example (step 1)** — build the first instance of a pattern *with* the learner (e.g. the first endpoint, the first DB write), explaining what and why, then run it together.
- **Challenge (step 2)** — the next slice that reuses that pattern (built `GET /tasks` together → they write `POST /tasks`).
- **Acceptance criteria** — almost always **runnable**: perform the action and see the real, persisted result. State the exact command and expected output.
- **Self-explanation prompt** — why this slice touches the layers it does, or why a key line is needed.
- **Hint ladder** — point at the analogous part of the worked example → name the specific layer/line to revisit → show the fix.
- **Verify** — run the app; the new capability is visible alongside the ones already working.

## Notes

- Keep production concerns light — auth, deployment, observability, scaling are usually out of scope for a lesson. If the learner wants production depth or stack-specific guidance, point them to the **build-your-own-x** skill, which exists for shipping.
- Web-search current scaffolding commands and library versions before using them — teaching stale syntax is worse than not teaching it.
- Each slice ends runnable; never leave the artifact broken between units.