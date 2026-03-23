# 2026-03-23 — Actionable analyses: quick-create and AI-discuss

**Type:** Observation
**Status:** confirmed

## What happened

The strategic framework Analysis tab went from read-only insight display to actionable workflow surface. Every framework analysis now offers ways to act on what it reveals — either by creating model objects directly (quick-create) or by discussing findings with the AI advisor.

### Quick-create actions

Three inline form functions added to `analysis.ts`:
- `quickCreateEntity(entityType, defaultLabel?, defaultDescription?)` — creates Resource, Actor, or Result
- `quickCreateAssumption(subjectId?, subjectLabel?, defaultPredicate?)` — adds assumption with subject dropdown, confidence selector
- `quickCreateEvent(eventType, defaultLabel?, defaultDescription?)` — creates Decision or Activity

Forms appear at the top of the analysis content area (not modals — follows the existing inline form pattern from entities.ts/assumptions.ts). On submit they call `toolFetch()`, refresh model data, and reload the current analysis after a 500ms delay.

### AI-discuss integration

`discussWithAI(prompt)` switches to build mode, creates a conversation if needed, and sends a context-rich prompt. Each framework generates prompts that include the current analysis state — resource counts, assessment summaries, specific gaps. The AI gets enough context to give useful, specific advice rather than generic strategy talk.

### Per-framework action mapping

| Framework | Create actions | AI actions |
|---|---|---|
| SVIMA | + Resource (global), + Assumption (per-row for unknown dims) | Per-resource AI, global SVIMA review |
| Five Forces | + Actor, + Assumption (per-force card) | Per-force AI, global forces review |
| Activity System | + Activity | Fix isolated activities, global system review |
| Positioning | + Decision, + Positioning Assumption | Global positioning review |
| Value Chain | + Activity (per-stage), + Resource | Global chain review |
| Strategic Groups | + Competitor, + Dimension Assumption | Global groups review |
| Market Segments | + Customer Segment, + Segment Decision | Global segmentation review |

### Implementation pattern

Action buttons use `data-action` and `data-*` attributes. A single `attachActionHandlers(container)` function wires all buttons after each render. Callback infrastructure mirrors overview.ts — `setAnalysisCallbacks()` receives `createConversation`, `openConversation`, `sendMessage`, `refreshModelData` from the orchestrator.

CSS adds ~220 lines: action bar containers, buttons in 3 sizes (standard, small for table rows/card footers, extra-small for value chain stages), and the quick-create form with fade-in animation.

## Why this matters

The gap between "seeing a problem" and "doing something about it" was the main weakness of the analysis tab. A SVIMA analysis might show 3 resources with unknown dimensions, but the user had to mentally note this, switch tabs, find the right form, and create assumptions manually. Now they click "+ Assumption" right next to the unknown dimension row.

The AI-discuss feature is particularly important for the Lasse demo. It shows the tool doesn't just display framework results — it helps the user work through the implications. The context-rich prompts mean the AI starts with knowledge of the specific analysis state rather than asking generic questions.

## Commits

- `2b9abad` (bkmng-app): "feat: actionable analyses — quick-create and AI-discuss in all 7 frameworks"

## What we learned

- **Inline forms beat modals for analysis context**: The user can see the analysis result that prompted the action while filling out the form. A modal would hide that context.
- **Context-rich prompts are critical**: Sending "Help me with SVIMA" is useless. Sending "I have 5 resources, 2 with sustained advantage and 1 with unknown dimensions on S, V, I — help me formulate assumptions" is actionable.
- **The module callback pattern scales**: This is now the third module using the setter-based callback injection (overview, analysis, and the orchestrator wires them identically). The pattern works.

## Next expected events

- Test the deployed production build
- Identify the next feature priority for the Lasse demo
- Consider: enriching the model data to showcase richer analysis results
