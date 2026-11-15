---
name: greatui
description: Greatui turns a short UI brief into a project-specific DESIGN.md. It resolves open decisions with clickable options (1/2/3 … plus free text) and derives feeling, material, colour, motion and a single signature from empirically analysed Uiverse patterns (3,802 elements). Enforces state and accessibility gates.
allowed-tools:
  - Read
  - Write
---

# Greatui — from brief to DESIGN.md

## What Greatui is for

The user describes in one to five sentences **what kind of UI they want** — or just says "build me something". Greatui turns that into concrete design decisions and writes a `DESIGN.md` that an implementation agent can follow without asking questions.

Those decisions are not invented. They come from a complete analysis of **3,802 Uiverse elements**: technique frequencies, motion durations, easing curves, colour distribution, state definitions, archetypes and an accessibility audit. The numbers live in `uiverse-analyse.md`; Greatui uses them as a basis for decisions, not as style tips.

**Important:** the result is not a Uiverse look. Uiverse is an archive of isolated moments — loud, playful, context-free. Greatui takes the *mechanics* from it (how a state feels), not the *exaggeration* (glow nobody needs). A product needs a calm surface and exactly one loud spot.

---

## The input: ask first, then build

Greatui has two modes.

**Mode A — the user provides a brief.** Do not ask questions. Fill missing axes with defaults and document them as assumptions.

**Mode B — the user only says "build me something".** Ask the questionnaire first, before anything is written.

### How to ask

Never ask **in prose**. Use the question tool (`ask_questions`) — the user sees clickable options and can always answer freely.

- **3–6 options per question**, short labels, the recommended one first and marked with `(Recommended)`.
- **Fallback without the tool:** print the same options as a numbered list, plus the sentence "Reply with 1, 2, 3 … or your own answer."
- **The free-text field is the "own answer".** The tool adds it automatically — do not offer an "Other" option. Phrase the options so that even the last one is a real direction.
- **One question per axis.** No double questions, no matrix.
- **`multiSelect` only for the boundary question** ("What should it definitely not be?"), single select otherwise.
- **All open questions in a single `ask_questions` call.** Seven questions are one interaction, not seven rounds.
- **Seven questions maximum.** If the user already answered an axis in the brief, that question drops out.
- After the answers: summarise the brief in **five lines**, then write the DESIGN.md. Do not ask for confirmation again unless two answers contradict each other.

### The questionnaire

**F1 — What are you building?** (single)
1. Dashboard / internal tool (Recommended)
2. Landing page / marketing
3. Portfolio / editorial
4. Consumer app / mobile first
5. Shop / product page

**F2 — How should it feel?** (single)
1. Calm & precise (Recommended)
2. Trustworthy & clear
3. Warm & organic
4. Playful & curious
5. Technical & brutal
6. Premium & dark

**F3 — Which material?** (single)
1. Flat & framed (Recommended)
2. Soft / neumorphic
3. Hard edge
4. Light / glass
5. Decide for me

**F4 — Which colour?** (single)
1. Neutral + one accent (Recommended)
2. Dark + one signal accent
3. Warm paper tones
4. Monochrome + one accent
5. Existing brand colour — hex or name in the free-text field

**F5 — How much motion?** (single)
1. Calm — feedback only (2/10) (Recommended)
2. Balanced — states + reveals (4/10)
3. Lively — stagger, overshoot (6/10)
4. Cinematic — big choreography (8/10)

**F6 — What should people remember?** (single, the signature)
1. State — confirmations are drawn (Recommended)
2. Motion — one curve everywhere
3. Typography — labels behave
4. Material — light moves
5. Colour — the accent is ink
6. Decide for me

**F7 — What should it definitely not be?** (multiSelect)
1. The usual SaaS purple
2. Neon / glow
3. Playful / cartoonish
4. Cold / sterile
5. Overloaded / decorative

**Precedence:** the user's choice beats any default in this skill. If a choice contradicts the analysis (e.g. "neumorphic" plus "accessible"), take the choice and document the trade-off — for example a border and text contrast on top of the soft shadows.

### Alternative: the written brief

Anyone who prefers typing fills in this grid. Missing fields are not a blocker.

```text
UI BRIEF
Product:             (what it is, in one sentence)
What it does:        (the one task it is used for)
Audience:            (who, in what situation)
3 adjectives:        (e.g. calm, precise, expensive)
What it must NOT be: (the boundary, one sentence)
Reference:           (1 image, 1 product, or "none")
Constraints:         (stack, brand, mandatory colours, accessibility)
```

**Rules for handling the brief:**

1. If the 3 adjectives are missing, derive them from product + audience and write them into the DESIGN.md as an assumption.
2. If the boundary is missing, take the most obvious generic solution and declare it the anti-pattern ("not the usual SaaS purple").
3. Ask **at most three** follow-up questions, and only if two completely different UIs would follow. Otherwise decide and document the assumption.
4. Never invent numbers, clients, metrics or testimonials for the UI. Placeholders are `[value]`, not "99.9%".

---

## The method: five axes, in this order

The order matters because each axis constrains the next. Start with colour and you get a pretty slide with no behaviour.

1. **Feeling** — the temperament of the UI (determines everything else)
2. **Material** — depth, edges, surfaces (determines shadows and radii)
3. **Colour** — palette, roles, contrast (determines what may become the signature)
4. **Motion** — grammar of duration, curve, distance, stagger
5. **Signature** — the one memorable mechanic, chosen last so it does not fight the others

### Axis 1 — Feeling

Pick **exactly one** of the six temperaments. Blends are allowed, but one leads.

| Temperament | Works through | Typical for | Motion intensity |
|---|---|---|---|
| **Calm / precise** | little movement, lots of whitespace, hard edges, one accent | tools, finance, developer products | 2/10 |
| **Trustworthy / clear** | symmetry, readable hierarchy, soft corners | health, education, public sector | 3/10 |
| **Warm / organic** | irregular radii, paper tones, soft shadows | portfolios, food, community | 5/10 |
| **Playful / curious** | overshoot, stagger, surprising states | consumer apps, games, creative tools | 7/10 |
| **Technical / brutal** | hard offset shadows, monospace, visible grid | dev tools, studios, edits | 4/10 |
| **Premium / dark** | depth, little colour, precise light, slow calm | luxury, AI, night products | 3/10 |

Write the temperament as a sentence, not a list: *"Calm and precise, with exactly one playful spot."*

### Axis 2 — Material and depth

Uiverse knows four depth dialects (48% of all elements use `box-shadow`). Choose **one** as the base and at most one second for the signature.

| Dialect | Recipe | Strength | Risk |
|---|---|---|---|
| **Flat / framed** | 1px border, no shadow, radius 6–10px | clear, fast, accessible | looks cheap without good type |
| **Soft / neumorphic** | 2 shadows (light top-left, dark bottom-right), inset on press | haptic, quiet | contrast too low, often unreadable |
| **Hard edge** | `box-shadow: 4px 4px 0` with no blur, radius 0–8px | loud, charming, retro | turns into a comic fast |
| **Light / glass** | `backdrop-filter: blur(10–15px)`, `rgba(255,255,255,.05)`, 1px light edge | refined, deep | performance, contrast, trend risk |

**Rules:**

- Radii follow the dialect, not chance: flat 6–10px · soft 12–20px · hard 0–8px · glass 12–16px. A product uses **three radii at most** (S/M/L).
- Depth means hierarchy. A shadow without rank is decoration.
- Never let neumorphism be the only carrier of contrast: always add a border or text colour, or the UI falls apart for low vision.
- Glass only over content that would still be readable without the blur.

### Axis 3 — Colour

**Procedure (in this order):**

1. **Build a neutral ramp:** 7 steps from surface to text. No pure `#000` for surfaces (Uiverse does it often — in a product it is a bug); use off-black such as `#0B0B0C`, `#111214`, `#18181B`.
2. **Choose one accent.** Exactly one. Saturation below 85%. It carries: primary CTA, active state, focus ring, one data point. Not: surfaces, text and icons at the same time.
3. **Keep semantics separate:** success, warning, error, info — one colour each, always with an icon **and** text, never colour alone.
4. **Check 60-30-10:** 60% surface/neutral, 30% secondary surface/text, 10% accent.
5. **Test on three backgrounds:** `#FFFFFF`, `#0B0B0C`, brand colour. An accent that only works on one surface is not an accent.

**Tokens as RGB triplets**, so alpha variants need no new hex values (technique from the strongest Uiverse card):

```css
:root {
  --ink: 24 24 27;              /* rgb(var(--ink)) */
  --ink-soft: 82 82 91;
  --surface: 250 250 249;
  --accent: 214 58 34;          /* one accent */
  --accent-soft: 214 58 34 / .12;
}
```

**Hard gates:** text ≥ 4.5:1 · large type ≥ 3:1 · UI edges and focus ring ≥ 3:1. A focus ring is never just a colour change, always also a shape (ring, underline, outline).

**Forbidden:** more than one accent · gradient on body text · neon glow as the only proof of state · colour as the only carrier of meaning · random hex values per component.

### Axis 4 — Motion

The analysis produces a clear grammar. Use it as vocabulary, not decoration.

| Role | Duration | Easing | Example |
|---|---:|---|---|
| **State change** (hover, focus, toggle) | 200–300ms | `ease-out` | background, colour, small lift |
| **Spatial movement** (card, panel, reveal) | 400–600ms | `cubic-bezier(.23,1,.32,1)` | drawer, flip, expand |
| **Confirmation** (check, success, "saved") | 250–400ms | `cubic-bezier(.175,.885,.32,1.275)` | tick, pop, small overshoot |
| **Endless loop** (loader, pulse) | 1.5–3s | `linear` / `ease-in-out` | spinner, shimmer, breathing |
| **Ambient** (background, pattern) | 6s+ | `linear` | mesh, grid, drifting light |

**Rules:**

- **One distance, one curve.** Define `--ease-out`, `--ease-space`, `--ease-pop` and use them everywhere. Uiverse has 4,965 colours and dozens of curves — that is the mistake you do not copy.
- **Stagger 50–125ms** per element, eight steps maximum. Beyond that it becomes waiting, not rhythm.
- **Negative delays** for endless loops (`animation-delay: -250ms`) so the wave starts without a run-up.
- **Animate only `transform` and `opacity`.** Never `width`, `height`, `top`, `left`.
- **At most two things moving at once.** A hover that does scale + glow + shine + text swap is a circus.
- **Exit faster than enter** (about 60–70% of the duration).
- **Motion must mean something:** origin, direction, confirmation or progress. If it is only "cool", it goes.

**Reduced motion is mandatory, not optional:**

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: .01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: .01ms !important;
    scroll-behavior: auto !important;
  }
}
```

The signature must also work **statically** (colour, form, position), otherwise it is not a signature, it is an animation.

### Axis 5 — The signature (distinctiveness)

**Definition:** a signature is **one** mechanic that recurs throughout the product, can be described in one sentence, and stays recognisable in greyscale.

Uiverse offers five signature types. Choose **exactly one**:

| Type | Mechanic | Uiverse model | Everyday use? |
|---|---|---|---|
| **Material** | light or depth behaves consistently | glass with drifting light | yes, sparingly |
| **State** | a confirmation is "written" or "pressed" | tick via `stroke-dashoffset` | very good |
| **Motion** | one curve + one distance everywhere | `0.3s cubic-bezier(.23,1,.32,1)` | very good |
| **Typography** | labels and captions behave | letters rise in sequence | good, but sparingly |
| **Colour** | one accent behaves like ink | a red reserved for "now" | very good |

**Rules:**

- **One** signature. Not two. Everything else stays quiet.
- It must sit on the most important action (the primary CTA, the check, the save), not in the background.
- It must be cheap: one CSS rule, no canvas, no library.
- **The greyscale test:** screenshot in greyscale — is the signature still visible? If not, it hangs on colour alone.
- **The reduced-motion test:** without animation — does the meaning survive? If not, it is decoration.
- **The one-sentence test:** "Ours ________." If you need two sentences, it is not a signature.

Examples of one-sentence signatures:

- "Ours draws every confirmation instead of fading it in."
- "Ours moves light only when something happens."
- "Ours treats the accent as ink: it marks only the current action."
- "Ours puts every card on a hard edge, as if it were glued on."

---

## The archetype: what gets built

Uiverse sorts by interaction, not by DOM. Use this table to derive the components the brief needs — and add what is missing.

| Need | Archetype | Required states |
|---|---|---|
| "May I?" | Button | default · hover · focus-visible · active · disabled · loading |
| "What is here?" | Card | default · hover · focus-within · selected · empty |
| "How much longer?" | Loader / skeleton | running · determinate · reduced-motion |
| "On or off?" | Switch | off · on · focus-visible · disabled |
| "Am I confirming this?" | Checkbox | off · on · indeterminate · focus-visible · disabled |
| "Which one exactly?" | Radio / segmented | off · on · focus-visible · disabled |
| "Where do I type?" | Input | empty · filled · focus · error · success · disabled |
| "What must I do?" | Form | empty · validating · error · submitting · success |
| "What is this?" | Tooltip | hidden · visible · (touch alternative!) |
| "Heads up." | Notification / toast | info · success · warning · error · dismiss |
| "Which world am I in?" | Pattern / background | static · ambient · reduced-motion |

**What Uiverse does not have and you must add:** navigation, tabs, accordion, modal, table, pagination, breadcrumbs, badge, avatar, menu, date picker. Greatui does not build a complete app — it defines the *feeling layer* and the *states* of the components that appear in the brief.

---

## Writing the DESIGN.md

Write the file `DESIGN.md` into the project folder. Language: the language of the brief. Length: as short as possible, as precise as necessary — every line must contain a decision an implementer can follow.

### Template

````markdown
# Design System: [Product name]

## 0. Brief & non-goals
**Product:** [one sentence]
**Task:** [the one action it is used for]
**Audience:** [who, in what situation]
**Non-goals:** [what it deliberately is not — 2 points]
**Assumptions:** [what was derived from the brief because it was missing]

## 1. Personality
[One paragraph, 3–5 sentences. Three adjectives in bold. One sentence describing how the UI feels, not how it looks.]
**Temperament:** [one of six] · **Motion intensity:** [x/10]

## 2. Colour
| Token | Value | Role | Contrast |
|---|---|---|---|
| `--surface` | `#......` | base surface | – |
| `--surface-2` | `#......` | cards, raised surface | – |
| `--ink` | `#......` | primary text | [x:1 on surface] |
| `--ink-soft` | `#......` | secondary text | [x:1] |
| `--line` | `#......` | 1px edges | [x:1] |
| `--accent` | `#......` | the only accent | [x:1] |
| `--ok / --warn / --error` | `#......` | semantics, always with icon | [x:1] |
**Rules:** [max. 1 accent · 60-30-10 · never colour alone · focus ring = accent + shape]
**Forbidden:** [project-specific, e.g. "no purple glow", "no gradient on text"]

## 3. Typography
| Role | Font | Size / line-height | Weight | Use |
|---|---|---|---|---|
| Display | ... | clamp(...) | ... | once per page |
| Heading | ... | ... | ... | sections |
| Body | ... | 1rem / 1.6 | 400 | prose, max. 65ch |
| Mono | ... | ... | ... | figures, code, metadata |
**Rules:** [hierarchy through weight/colour, not size alone · max. 2 families + mono · tabular figures]

## 4. Material & depth
**Dialect:** [flat / soft / hard edge / light]
**Radii:** S [x]px · M [x]px · L [x]px · Pill [x]px
**Shadows:** [exact values, 1–3 levels, with roles]
**Rule:** [depth = hierarchy; a shadow without rank is out]

## 5. Motion
| Token | Duration | Easing | Use |
|---|---|---|---|
| `--t-fast` | 200ms | ease-out | hover, focus, toggle |
| `--t-space` | 500ms | cubic-bezier(.23,1,.32,1) | drawer, reveal |
| `--t-pop` | 300ms | cubic-bezier(.175,.885,.32,1.275) | confirmation |
| `--t-loop` | 2s | linear | loader |
**Rules:** [transform/opacity only · max. 2 things moving at once · stagger 50–125ms · exit 60–70% · reduced-motion mandatory]

## 6. The signature
**Sentence:** "Ours ________."
**Type:** [material / state / motion / typography / colour]
**Where:** [exactly one place, e.g. primary CTA + check + save]
**How:** [CSS mechanic in 1–3 lines]
**Static fallback:** [how it reads without animation]
**Proof:** [greyscale test · reduced-motion test · one-sentence test]

## 7. Components
### [Component]
**Anatomy:** [container, padding, radii, type]
**States:**
| State | Looks like | Motion |
|---|---|---|
| default | ... | – |
| hover | ... | ... |
| focus-visible | ... | ... |
| active | ... | ... |
| disabled | ... | – |
| loading | ... | ... |
| error | ... | ... |
**Do:** [...]
**Don't:** [...]

## 8. Layout & grid
[Columns, max-width, spacing on a 4/8 scale, where asymmetry sits, breakpoints]
**Rules:** [min-h-100dvh · no horizontal scroll · touch targets ≥ 44px · clamp() for type]

## 9. State matrix (mandatory)
[Table: component × default/hover/focus/active/disabled/loading/error/empty.
Each cell: defined / not needed / planned. No empty cells without a reason.]

## 10. Accessibility (gates)
- [ ] Every interactive element has `:focus-visible` with a visible ring (≥ 3:1)
- [ ] No `outline: none` without a replacement
- [ ] `prefers-reduced-motion` switches off every loop
- [ ] Inputs: `appearance: none` instead of `display: none`
- [ ] Every field has a linked `<label>`
- [ ] Touch targets ≥ 44 × 44 px
- [ ] Text ≥ 4.5:1, UI edges ≥ 3:1
- [ ] No information available on hover only
- [ ] Toasts with `role="status"` / `aria-live`
- [ ] Icon buttons have an accessible name

## 11. Anti-patterns (project-specific)
- [the most likely pattern for this project, e.g. "no SaaS purple gradient"]
- [what the analysis shows as the most common failure: hover-only, glow stacks, 1.5s flips]
- [what the brief explicitly rules out]

## 12. Implementation
```css
:root { /* tokens: colour, motion, radii, shadows */ }
```
[Order: tokens → reset → type → layout → components → states → reduced-motion]
**Definition of done:** [3 checkable points, e.g. "every button has 6 states", "signature readable in greyscale", "no contrast below 4.5:1"]
````

---

## Quality gate: the self-test

Before you write the DESIGN.md, answer these ten questions with yes. One no means: fix it, do not phrase it.

1. Is the temperament **one**, not a list?
2. Is there **exactly one** accent?
3. Does every colour have a **role**, not just a hex value?
4. Are all contrasts **measured**, not guessed?
5. Does the product use **at most three** radii and **one** shadow logic?
6. Does every component define at least **five** states?
7. Is the motion table **complete** (duration, curve, role)?
8. Is the signature describable in **one sentence**?
9. Does the signature work **without colour** and **without animation**?
10. Does the file contain **no** invented number and **no** placeholder that could be mistaken for content?

Plus the "Uiverse test": place an element from the DESIGN.md on `#080808` and on `#e8e8e8` — does it look like the same product on both? If not, the design hangs on the stage.

---

## Anti-patterns from the analysis

These patterns are measurably frequent in the corpus and measurably bad in a product. Forbid them explicitly in every DESIGN.md:

| Anti-pattern | Evidence in the corpus | Better |
|---|---|---|
| Hover-only interaction | 27.5% of all elements | always `:focus-visible` + a touch path |
| Removing the focus ring | 12.5% `outline: none` | ring in accent + shape |
| Endless animation with no exit | 0.2% `prefers-reduced-motion` | media query, loops off |
| Hiding the input | 80% of checkboxes | `appearance: none` |
| Effect stacks (glow + shine + scale) | many buttons | one movement per interaction |
| 1.5s flip cards | cards | 400–600ms, or no flip at all |
| Decorative loaders without progress | 718 loaders | skeleton that matches the layout |
| Invented notifications | 23 "notifications", mostly scenes | real toasts with `role="status"` |
| No token system | 4,965 hex values | 7 neutral steps + 1 accent + semantics |
| "Hover me" copy | 133 occurrences | a real action label |
| Tooltip as the only explanation | 62 tooltips, 4× `aria-describedby` | visible helper text + tooltip as a bonus |
| Colour as the only state | many toggles | colour + shape + text/icon |

---

## Two compact examples

### Example A — "Fintech dashboard, calm, precise, dark"

**Decisions:**
Feeling *calm/precise* (motion 2/10) · Material *flat + framed*, one soft shadow only for floating panels · Colour off-black `#0B0B0C`, neutral ramp, one accent `#C6F24E` only for "current" · Motion 200ms ease-out, 500ms for panels, no bounces · **Signature: typography/motion** — "Ours counts every number up in 40ms steps on appearance, without a bounce."

**DESIGN.md core:**
```
--surface: #0B0B0C · --panel: #141518 · --line: #26282D
--ink: #F2F3F5 · --ink-soft: #9A9DA5 · --accent: #C6F24E
--t-fast: 200ms ease-out · --t-panel: 500ms cubic-bezier(.23,1,.32,1)
Radii: 8 / 12 / 16px · Shadows: panel only `0 12px 32px rgb(0 0 0 / .35)`
```

### Example B — "Illustrator's portfolio, warm, playful, handmade"

**Decisions:**
Feeling *warm/playful* (motion 6/10) · Material *hard edge* (4px offset, no blur) · Colour cream `#F6F2E9`, ink `#1B1A17`, one accent tomato `#D63A22` · Motion 300ms with overshoot for confirmations, 450ms for cards · **Signature: state** — "Ours draws every check mark instead of fading it in."

**DESIGN.md core:**
```
--paper: #F6F2E9 · --ink: #1B1A17 · --accent: #D63A22
--shadow-sticker: 4px 4px 0 rgb(27 26 23 / 1)
--t-pop: 320ms cubic-bezier(.175,.885,.32,1.275)
Radii: 2 / 8 / 999px · Focus: 3px accent outline + 4px offset
```

---

## What Greatui deliberately does not do

- It does not invent content, metrics or testimonials.
- It does not build a full component library — it defines the system and the states of the components that appear in the brief.
- It does not copy a Uiverse look. An element with glow that looks good on `#080808` is not a design system.
- It does not make product decisions (navigation, information architecture, data model). The DESIGN.md describes *how* it feels, not *what* it can do.
