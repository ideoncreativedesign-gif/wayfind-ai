# WAYFIND — Visual Design Direction (v3)

*Companion document to docs/product-brief.md and docs/ux-flow-spec.md. Supersedes the previous draft. Status: creative direction, pre-screen-design.*

---

## 0. Starting position

The previous pass borrowed Partiful's structure (clean canvas, reserved color, black actions) and applied it to WAYFIND's sections. This pass does the reasoning in the other direction: start from what WAYFIND needs people to *feel*, then pull from Partiful's toolkit only where it actually serves that feeling — and name explicitly where it doesn't. The governing test is unchanged: **AI should feel like a translator of human judgment, not the author of the trip.**

---

## 1. The integration logic — psychology × Partiful

This table is the backbone of everything below. Read it before the rest of the document; every later section is an application of a row in this table, not a new decision.

| WAYFIND needs the person to feel | Partiful technique that serves it | Partiful technique that threatens it | Resulting rule |
|---|---|---|---|
| **Trust** — this will actually work | Color reserved for meaning, never decoration — a form of honesty, not just style | Gradient/color used everywhere would read as hype rather than information | Saturated color always means something specific. If it doesn't, it's not there. |
| **A real person's judgment is present** | "Hosted by" — active, ongoing stewardship, not a static credit | — (a clean win, no real tension) | Host identity is structural to the object, not a caption on it. |
| **AI translated, didn't author** | Consistent black action buttons — no AI-coded color, glow, or gradient near AI's own output | Bold display type, if used everywhere, starts to feel like "the system's voice" | Bold display type is reserved for the host's material — the trip's own title and words — never for AI-generated text. |
| **A clear head at the trust decision** | — | Bounce, spring motion, loud gradient, celebration energy | Explicitly, deliberately dialed back at Remix Result and Save. The one screen this document asks for restraint on purpose. |
| **Wants to explore, feels travel desire** | Full-bleed photography, tilted collage, gradient bands, energetic entrance motion | — | This is where all the borrowed energy concentrates — Discover and Trip Detail, and nowhere else. |
| **Low effort entering constraints** | Clean, quiet white sections | Tilt, collage, decorative looseness | Constraint Input and Fixed/Flexible Review stay visually calm even while the rest of the app isn't. |
| **This is now mine** | Confident black actions signal a real, completed choice, not a tentative one | — | Saved Trip uses the same decisive visual register as any completed action — no separate "congratulations" treatment that would feel manufactured. |

**One principle that falls out of this table and deserves to be named on its own:** there are two different kinds of "not polished," and only one of them belongs in WAYFIND. Partiful's tilted photo stacks are *decoratively* imperfect — the looseness is in how already-clear objects are arranged, and it reads as personal and human. That's welcome anywhere WAYFIND is showing photography or browsing content. But the fixed/flexible legend, the change explanations, and the constraint form are *informational* — precision there isn't corporate stiffness, it's the actual mechanism the trust decision depends on. Decorative looseness never bleeds into the layer that's doing the reasoning.

---

## 2. Brand personality

Each attribute now carries the psychological job it's actually doing, not just a style description.

**Vivid** — visually alive at the browsing layer. *Job: makes exploring a trip feel like desire, not homework.*
- Avoid: saturation with no hierarchy, or vividness bleeding into the reasoning layer.

**Unfussy** — polished but not stiff. *Job: signals "a real person made this, casually," reinforcing provenance.*
- Avoid: unfussy tipping into actually unclear where clarity is load-bearing.

**Discerning** — a small, curated catalog. *Job: the opposite of an algorithmic feed — protects the sense that someone with taste chose this.*

**Confident, not loud** — bold only where it's earned. *Job: keeps the one loud moment per screen legible instead of competing with itself.*

**Social-native** — feels like a friend shared it. *Job: this is the actual mechanism of trust transfer — people trust friends' plans more than institutions' plans.*

**Grounded** — real photography, real places, real hosts. *Job: the thing that makes vividness safe — energy applied to something real doesn't feel like hype.*

**Loud about its sources** — host identity never shrinks. *Job: the provenance principle has to survive contact with a louder visual system, or the thesis quietly erodes.*

---

## 3. Visual positioning

| Tension | Position | Psychological reasoning |
|---|---|---|
| Editorial ↔ Utility | Mode-shifts: social/photographic at Discover, utility-clear from Constraints onward | Desire and decision-making are different mental modes; the interface should match the mode, not fight it. |
| Human ↔ Technological | Human, emphatically | Every technological signifier (glow, AI badge, synthetic color) reads as "the system made this," directly undermining the translator-not-author thesis. |
| Minimal ↔ Expressive | Expressive, but allocated to Row 5 of the integration table only | Expressiveness spent everywhere loses its meaning; expressiveness spent on "wanting to explore" specifically reinforces the right feeling at the right time. |
| Calm ↔ Energetic | Energetic surface, clear-headed core | Directly Row 4 of the table — this is the one tension the whole document exists to resolve correctly. |
| Premium ↔ Accessible | Accessible | A host you'd trust is a peer, not a concierge — luxury signaling would work against "a friend shared this." |
| Personal ↔ Systematic | Systematic underneath, personal on the surface | The fixed/flexible logic is genuinely systematic; showing that as warmth (a host's judgment) rather than mechanism (a system's rules) is the entire provenance strategy. |

---

## 4. Visual metaphor

**Primary: the hosted trip.** This survives from the previous pass, now justified directly by Row 2 of the integration table: a host is someone whose judgment you're trusting *by definition* of the role, which does more psychological work for provenance than a magazine byline ever could. "Hosted by" isn't a style choice — it's the metaphor that makes the whole trust mechanism legible without explanation.

**Secondary: the photo dump.** Casually-curated, real, specific — serves Row 5 (exploration desire) without threatening Row 1 (trust), because a photo dump is still fundamentally documentary. This is where "vivid" and "grounded" have to coexist, and the metaphor is what lets them.

**Structural: "hosted by → remixed by you."** Unchanged — the lineage thread, now expressed in language everyone already understands from event culture.

---

## 5. Color direction

- Background: near-white (`#FFFFFF` primary, `#FCFBFA` for content-dense screens)
- Primary text: warm near-black (`#17161A`)
- Secondary text: neutral gray (`#6B6870`)
- Signature gradient (Discover and Trip Detail only): coral-pink (`#FF6F61`) into violet (`#8C6FE0`)
- Primary actions: solid ink-black fill (`#17161A`) — never the gradient, never a colored accent

**Reserved semantic colors** — the direct application of Row 1's honesty principle:
- Preserved: vivid green (`#2FBE5C`)
- Changed: vivid coral-orange (`#FF7A45`)
- Uncertain: soft violet (`#A78BFA`)
- Fixed: solid ink-black, full weight
- Flexible: light gray outline (`#D8D5DA`)

The rule is stricter than "these colors have a job" — it's that **using them anywhere else is a trust violation, not just an inconsistency.** If coral shows up on a marketing banner instead of a "changed" stop, the color has been spent on hype instead of information, and the whole reserved-color trust mechanism stops working the next time the user actually needs to read it.

---

## 6. Typography

**Display: Clash Display** (Fontshare) — reserved for the host's own material: trip titles, trip names. Per Row 3, this typeface is doing identity work for a real person, so it never appears on AI-generated text.

**UI / Body: General Sans** (Fontshare) — carries everything AI explains: reasoning, change descriptions, constraint labels. Deliberately neutral, because neutral is what "translated, not authored" looks like typographically.

**Metadata / tags: IBM Plex Mono** — budget tier, duration, day counts. Precision-coded, reinforcing Row 6 (low-effort, quiet clarity) wherever it appears.

The pairing itself encodes the thesis: bold personality for what a real person made, quiet neutrality for what AI is doing with it.

---

## 7. Layout philosophy

- White canvas by default; color and photography concentrated exactly where Row 5 applies (Discover, Trip Detail).
- Tilted photo collages for browsing only — never for the fixed/flexible legend, the constraint form, or the remix result. This is the decorative-vs-informational rule from Section 1, applied directly.
- Full-bleed photographic hero at Trip Detail, gradient-overlaid for host credit and title.
- Clean, quiet sections for Constraint Input and Remix Result — Row 6 and Row 4 both land here.
- Shadow-based elevation for card separation on the white canvas.

---

## 8. Shape language

- Larger, friendlier corner radius (16–20px on cards, full pill on buttons/tags) — approachability, doing different psychological work than color or fill.
- Buttons: filled black pills. The roundness signals approachable; the solid black fill signals decisive. Both are needed at once — a sharp black button would feel cold, a soft colored button would feel indecisive.
- Tags/chips: rounded pills, color strictly reserved per Section 5.

---

## 9. Imagery

Dominant, not secondary — real trip photography carries most of the visual weight at Discover and Trip Detail. This is the highest-leverage place the "grounded" attribute has to hold: the more visual weight photography carries, the more damage a generic or stock-feeling image does to the entire trust proposition. Never stock. Never staged "adventure" photography. If a real photo isn't available for a seeded trip, that trip's imagery is simpler and quieter — never substituted with something generic.

---

## 10. AI visualization

Unchanged in principle, and Row 3 makes the stakes explicit: the louder the surrounding visual system, the easier it is for an AI-coded visual tell to slip in unnoticed. No assistant icon, no glow, no AI-specific color. Fixed/flexible uses the reserved semantic colors and pill shapes from Sections 5 and 8. Processing is shown as real, named reasoning steps, in General Sans — never Clash Display, per Section 6's rule that bold display type is reserved for the host's own words.

---

## 11. Provenance language

- **"Hosted by [Name]"** — structural, not a caption, per Section 4.
- **"Remixed from [Name]'s trip"** — same information as "adapted from," in the vocabulary the metaphor already established.
- Host credit uses Clash Display at meaningful size, persisting through Saved Trip — the one place bold display type appears outside the trip's own title, because the host's name is, functionally, part of the trip's own material.

---

## 12. Motion

Directly Row 4 and Row 5, applied:

- **Discover**: real personality — tilt, settle, a touch of spring on card entrance.
- **Trip Detail**: a confident photographic reveal.
- **Constraint Input / Fixed-Flexible Review**: quiet, fast, no personality — motion here should be invisible, not expressive.
- **Remix Result / Trust Decision**: settling only, never bouncing. The one place this document asks for restraint on purpose, and the reason the whole table in Section 1 exists.

---

## 13. Overall recommendation

**The hosted trip — vivid where it earns your interest, quiet where it earns your trust.**

Every choice in this document traces back to a single row in Section 1's table: energy is real and earned at Discover and Trip Detail, where the job is making someone want to explore a real person's trip. Precision and restraint are just as real and just as deliberate at Constraint Input, Fixed/Flexible Review, and Remix Result, where the job is earning a genuine trust decision. The two registers aren't in tension by accident — they're doing two different psychological jobs, and the document's only real discipline is never letting one bleed into the other's territory. Reserved color, black actions, and the host metaphor are what make that boundary legible without ever having to explain it.
