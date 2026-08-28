# WAYFIND — UX Flow Specification

*Companion document to the WAYFIND Product Brief. Status: conceptual UX architecture, pre-visual.*

---

## A note on the proposed sequence, before the flow itself

The brief listed eleven steps. Three of them don't hold up as independent states once you ask what each one actually needs to accomplish:

- **"Start Remix"** isn't a state — it's a single tap at the end of Understand. Giving it its own screen would insert a meaningless pause between deciding and acting.
- **"Review adapted trip"** and **"Compare"** are the same moment, not two. Showing the adapted trip *without* markers for what changed, and only then offering a separate comparison, forces the traveler to hold the original in memory and reconstruct the diff themselves — exactly the synthesis work WAYFIND exists to remove. They should be one state: the adapted trip shown with change markers inline, with full side-by-side as an optional deeper view for anyone who wants it.
- **"Trust decision"** and **"Save"** are also the same moment. A separate trust-decision screen before the save action would feel exactly like the research survey the brief explicitly warns against. The save action itself *is* the trust decision — it just needs to be framed as a real choice, not a formality.

This collapses eleven conceptual steps into **seven real states**. The full reasoning for each collapse is below; Section 11 gives the resulting screen inventory.

---

## 1. Core User Flow

### Entry / Discover *(merged — see note above; "Entry" has no distinct content of its own)*
- **User goal:** find a trip worth exploring further.
- **User action:** browse a small set of real trips.
- **Information needed:** none.
- **System response:** a short list of curated trips, each with just enough signal to judge relevance — destination, duration, one line on what it's for, who made it.
- **AI behavior:** none. Pure curation at this scale; no ranking algorithm is justified for 20–50 seeded trips.
- **Decision point:** open a trip, or leave.
- **Next state:** Trip Detail.

### Understand (Trip Detail)
- **User goal:** decide whether this specific trip is worth adapting.
- **User action:** scan the trip's shape — stops, pacing, creator note.
- **Information needed:** none from the user yet.
- **System response:** the trip's sequence, an at-a-glance pacing/vibe signal, a short creator note, and a *teaser* — a count, not a breakdown — of how many elements are fixed vs. flexible.
- **AI behavior:** none. This is a static presentation of an existing object, not a generative step.
- **Decision point:** adapt this trip, or go back.
- **Next state:** Constraint Input, or back to Discover.

### Enter Constraints
- **User goal:** give WAYFIND enough to personalize credibly, with minimum effort.
- **User action:** enter duration/timing, party, budget tier; optionally, preferences.
- **Information needed:** see Section 4 — this is deliberately smaller than the brief's working list.
- **System response:** light validation only (plausible duration, etc.) — no live pricing or availability checks at MVP.
- **AI behavior:** none yet. This is data collection, not reasoning.
- **Decision point:** submit, or go back to reconsider the trip.
- **Next state:** Fixed/Flexible Review.

### Review Fixed/Flexible
- **User goal:** understand what's actually negotiable *for this specific case*, and see any direct conflicts, before committing to a remix.
- **User action:** review a short, evaluated list — not the generic teaser from Understand, but a version checked against what they just entered.
- **Information needed:** none additional.
- **System response:** locked elements with one-line reasons (e.g., "vineyard tour — only runs Tue/Thu"), a summary of what's flexible, and any conflicts flagged explicitly (e.g., their date range excludes every Tuesday/Thursday).
- **AI behavior:** the first real reasoning step — classifying fixed/flexible *relative to this traveler's constraints*, and detecting conflicts.
- **Decision point:** proceed (accepting how a conflict will be handled), or go back and adjust constraints.
- **Next state:** Remixing, or back to Enter Constraints.

### AI Remix (Remixing)
- **User goal:** none directly — this is a system-driven, passive state.
- **User action:** wait, or cancel.
- **Information needed:** none additional.
- **System response:** progressive, real disclosure of what's being reasoned about (see Section 6).
- **AI behavior:** the core computation — constraint reasoning, intent-preserving adaptation.
- **Decision point:** none for the user, beyond cancel.
- **Next state:** Remix Result.

### Review + Compare + Trust Decision + Save (Remix Result) *(merged — see note above)*
- **User goal:** understand what they now have, judge it against the original, and decide whether it's theirs.
- **User action:** scan the adapted trip with inline change markers; optionally expand full comparison; then choose to save or not.
- **Information needed:** none additional — everything needed to decide should already be visible.
- **System response:** the adapted trip as a coherent whole, annotated with what was kept/changed/uncertain; a short trip-level tradeoff summary; provenance kept visible; an optional expandable full compare.
- **AI behavior:** explanation generation — what changed and why — plus explicit uncertainty flagging.
- **Decision point:** the trust decision itself — "save as my trip" or "not quite," with an optional one-line reason.
- **Next state:** Saved Trip, or remain in Remix Result / back to Enter Constraints.

### Saved Trip
- **User goal:** confirm they now have their own trip, with origin still traceable.
- **User action:** view; nothing else required at MVP (no export, share, or edit needed to test the hypothesis).
- **Information needed:** none.
- **System response:** the adapted trip, with a visible but secondary reference to its source.
- **AI behavior:** none.
- **Next state:** end of flow, or back to Discover.

---

## 2. Information Architecture

**Objects and relationships:**

- **Creator** creates one or more **Trips**. For MVP, this can be a 1:1 mapping per seeded trip — no creator accounts or multi-trip profiles are required.
- **Trip** contains an ordered set of **Stops**. A Trip is never mutated by a remix — it stays intact and independently discoverable, so multiple travelers can remix the same source trip without conflict.
- **Stop** carries: place, day/time, type, and a fixed/flexible designation *in the abstract* (its own nature — e.g., "this tour only runs certain days").
- **Traveler Constraints** is a standalone object tied to a session, not to the Trip — it doesn't modify the Trip; it's an input to a Remix.
- **Remix** is a derived object: references a source Trip + a set of Traveler Constraints, and produces a new set of Stops (the adapted structure) plus a set of **Change/Reasoning** records.
- **Change/Reasoning** is attached to individual Stops within a Remix — each one states whether the stop was kept, changed, added, or dropped, why, and (where relevant) which original Stop it derives from. This is also where fixed/flexible status becomes *concrete* rather than abstract — evaluated against actual constraints, not just the Trip's inherent nature.
- **Saved Trip** is a persisted Remix. It permanently retains its reference to the source Trip and Creator — provenance isn't a one-time discovery-stage label, it's a permanent property of the object.

The key architectural decision: **a Remix is a new object, not an edit.** This is what makes lineage possible and keeps the source trip stable for future travelers.

---

## 3. Trip Object UX — before deciding to remix

**Essential**
- What the trip is: destination(s), duration, at-a-glance route shape
- Who made it, with a minimal credibility signal (e.g., that they actually took it) — not a full profile
- Overall pace and rough budget tier
- Enough of the stop sequence to judge fit — highlights, not a full day-by-day breakdown

**Useful, not blocking**
- A short creator note on why the trip is shaped the way it is
- The fixed/flexible teaser count
- A rough cost breakdown by category

**Unnecessary for MVP**
- Full creator profile or trip history
- Photo galleries or rich media beyond what conveys the trip's shape
- Ratings, reviews, or comments
- Real-time price/availability data
- Full day-by-day detail before the decision to remix — that level of depth belongs after, in the Remix Result view, not before

---

## 4. Constraint Input — challenging the working list

The brief's list (dates, budget, party, preferences) is close but slightly over-scoped. Breaking it down:

**Truly necessary**
- **Duration and rough timing** — but not exact calendar dates by default. A day count plus an approximate month/season is enough to reason about pacing; exact dates only matter if a specific fixed element in the source trip is genuinely date-bound (a festival, a seasonal closure). Asking for precise dates unconditionally adds friction the MVP doesn't need, since there's no live booking or availability behind it.
- **Party size/type** — meaningfully changes pacing and activity suitability; no credible remix without it.
- **Budget** — necessary, but as a coarse tier (budget / mid-range / comfortable), not a number. A precise figure implies a precision the system can't actually deliver at MVP, and it's more data than the reasoning needs.

**Optional**
- **Preferences** — valuable, but should be a short list of one-tap tags the traveler can skip entirely. If skipped, the AI should default to preserving the original trip's own balance rather than guessing at unstated preferences.

**Should be inferred, not asked**
- **Pace preference** — largely follows from the duration change itself (fewer days than the original implies tighter pacing); don't ask a separate "how intense do you want this" question unless the traveler wants to override the inferred default.
- **A first-pass interest signal** — the traveler already expressed a preference by choosing *this* trip over others. Preferences shouldn't start from a blank slate; they should default to "keep the original's emphasis" and only need adjusting, not authoring from scratch.

**What creates unnecessary friction, and should be avoided**
- Full travel-profile questions unrelated to this specific remix
- Exact calendar dates when nothing in the trip actually requires them
- Itemized budgets
- Mandatory preference selection

**Minimum required for MVP:** duration + rough timing + party + budget tier. Everything else is optional or inferred.

---

## 5. Fixed vs. Flexible Experience — conceptual model

The core idea: **fixed/flexible is not a fixed property of a Stop — it's an evaluation that only becomes meaningful once checked against a specific traveler's constraints.** A dated vineyard tour is "fixed" in the abstract sense that it has its own nature, but whether that matters *to this traveler* depends entirely on whether their dates land on a day it runs. The UX should reflect this two-layer structure:

- **Abstract layer** (shown at Understand, before constraints exist): a lightweight signal — "some elements are date-locked" — that sets expectations without pretending to be personalized yet.
- **Concrete layer** (shown at Review Fixed/Flexible, after constraints exist): the same elements, now evaluated against the traveler's actual input, with explicit flags where something conflicts.

**Communicating why something is fixed:** every fixed label must have a reason available on demand — never a bare flag. "Fixed" without a reason reads as arbitrary and undermines the transparency the whole product is built on.

**Handling conflicts:** this is the most important interaction in the whole flow, because it's where trust is made or lost. A conflict should never be resolved silently by the system in either direction — never silently dropped, never silently kept and glossed over. It should surface as an explicit small fork: keep the fixed element and adjust the traveler's dates to fit; drop it and note what will be suggested instead; or proceed with the conflict flagged and unresolved for the traveler to reconsider later. The system states the tradeoff; the traveler makes the call.

---

## 6. AI Remix Experience

**Before:** already handled — the Fixed/Flexible Review *is* the "before" moment. There's no separate pre-remix step needed; by the time the traveler confirms, they already know roughly what's about to happen and why.

**During:** avoid a generic "AI is thinking" state, but avoid the opposite failure too — decorative flavor text that doesn't correspond to anything real is just the same problem in a nicer costume, and it directly undermines the "make AI reasoning visible" principle this product is testing. Whatever is shown here needs to reflect actual stages of reasoning, e.g.: checking which stops fit the new duration → adjusting pacing for party size → reconciling the flagged fixed-element conflict → finalizing. If the real system can't report on stages like this, the honest fallback is a brief, plain state — not invented theater.

**After — the result must make five things clear:**
- **Preserved** — the default state of most stops; no heavy annotation needed, since most of the trip should visibly remain the original.
- **Changed** — each changed stop gets a visible marker with a one-line reason on tap, using the same interaction pattern established in the Fixed/Flexible Review, not a new one. Consistency here matters more than novelty.
- **Why it changed** — tied directly to the constraint that caused it ("shortened to fit 6 days," "swapped for your food preference").
- **Tradeoffs** — surfaced once at the trip level, not stop-by-stop: a short list of the real compromises made (e.g., "to fit 6 days, the Douro cruise was dropped so the vineyard tour could stay").
- **Uncertain** — anything the AI wasn't confident about needs a visibly distinct treatment from "changed," not folded into the same marker. This is the direct UX expression of "the AI should not invent details it cannot ground."

---

## 7. Compare Experience

Given the Section 1 merge, "compare" isn't a separate destination — it's two depths of the same view:

- **Default (inline):** the adapted trip itself, with kept/changed/uncertain markers built in. For most travelers, this should be enough to answer "is this still the trip I liked, adapted to me."
- **Optional (expandable):** a true side-by-side of original vs. remix, for anyone who wants to scrutinize further before deciding.

**What belongs in the comparison:**
- Overall structure/sequence — does the shape still read as the same trip
- Which stops were kept, dropped, or added
- Pacing
- Budget tier shift, if any
- What happened to the fixed elements specifically
- Provenance — visibly still the same source trip

**What doesn't belong, and would add complexity without adding insight:**
- Line-by-line price comparison
- Minute-by-minute schedule diffing
- Granular map/route overlays

---

## 8. Trust Decision

The decision should be embedded in the save action itself, not staged as a separate screen or a rating scale — both would read as research instrumentation rather than product.

- **The decision:** framed as a real, binary-leaning choice — "Save this as my trip" vs. "Not quite."
- **Possible responses:**
  - *Save* → proceeds to Saved Trip, lineage recorded. This is the strongest positive signal the prototype can capture.
  - *Not quite* → an optional, single, open-text prompt ("what's off?"), not required — then returns to the Remix Result view, not back to the start, so the traveler can keep inspecting or go back and adjust constraints.
- A three-way "partial trust" state was considered and rejected for MVP — it adds interaction complexity without adding much signal beyond what an optional free-text reason on "not quite" already captures. Simpler is more testable here.
- **Information needed before deciding:** nothing new — everything relevant should already be visible from the Remix Result view. If the traveler needs more information at this point to decide, that's itself a signal the Remix Result view under-communicated something.

---

## 9. Save / Remix Lineage

On save, the persisted object is a Remix with a permanent reference to its source Trip and Creator — not a one-time citation shown only at discovery. The Saved Trip view should keep this visible but secondary: present enough that the traveler always knows where their plan came from, without it dominating the sense that this is now *their* trip.

Because a Remix never mutates the source Trip, the lineage stays clean in both directions: the original remains untouched and independently discoverable by others, and the traveler's saved version remains clearly theirs while still traceable. This is the direct product expression of two Brief principles at once — provenance as part of the product, and keeping the traveler in control.

---

## 10. Edge Cases — prioritized by relevance to the hypothesis

Not all of these deserve equal design effort. Prioritizing by what could actually produce a false result on the core hypothesis:

**High priority — directly test the hypothesis**
- **Constraints conflict with a fixed element.** The single most important edge case in the whole flow — this is exactly where trust is made or broken. Already addressed structurally in Section 5; it needs to work well, not just exist.
- **Almost nothing from the original can be preserved.** If a traveler's constraints are extreme enough (wildly different dates, budget, or party), the honest response is to say so plainly — "your constraints are very different from this trip's; most of it will need to change" — rather than dress up a near-total rebuild as a light remix. This matters because if the UX pretends otherwise, it contaminates the hypothesis test: a bad result here would look like "remix isn't valuable" when the real story is "this pairing was a bad match to begin with."
- **AI cannot confidently adapt something.** Must surface as explicitly uncertain (Section 6), never guessed at silently.
- **Source trip contains incomplete information.** With a small, hand-curated catalog, this is largely preventable at the content stage rather than needing heavy runtime handling — but where it does occur, the system should flag the gap rather than invent a plausible-sounding fill.

**Lower priority — real, but shouldn't consume MVP design effort**
- **Mid-remix constraint changes.** Reasonable to just require restarting the remix step rather than building live re-editing — an intentional simplification, not an oversight.
- **Very different dates, budget, or party, treated individually.** These are largely subsumed by the "conflict" and "near-total rebuild" cases above and don't need separate handling paths.

---

## 11. MVP Screen / State Inventory

Seven states, following the collapses argued for above:

**1. Discover**
- Purpose: let the traveler find a trip worth exploring
- Entry condition: app opened
- Primary action: select a trip
- Secondary actions: none required at this scale
- Key content: curated trip list (destination, duration, one-line description, creator)
- AI behavior: none
- Exit states: → Trip Detail

**2. Trip Detail**
- Purpose: let the traveler judge whether to remix
- Entry condition: trip selected
- Primary action: "Adapt this trip"
- Secondary actions: back to Discover
- Key content: stop sequence overview, pace/vibe signal, creator note, fixed/flexible teaser
- AI behavior: none
- Exit states: → Constraint Input, or back to Discover

**3. Constraint Input**
- Purpose: collect the minimum for a credible remix
- Entry condition: "Adapt this trip" tapped
- Primary action: submit duration, party, budget tier (+ optional preferences)
- Secondary actions: skip preferences; back to Trip Detail
- Key content: minimal form per Section 4
- AI behavior: none
- Exit states: → Fixed/Flexible Review

**4. Fixed/Flexible Review**
- Purpose: set expectations and surface conflicts before committing to a remix
- Entry condition: constraints submitted
- Primary action: proceed
- Secondary actions: adjust constraints; resolve a flagged conflict
- Key content: locked elements + reasons, flexible summary, conflicts and resolution options
- AI behavior: constraint-specific fixed/flexible classification, conflict detection
- Exit states: → Remixing, or back to Constraint Input

**5. Remixing**
- Purpose: keep the traveler informed with real reasoning stages, not a spinner
- Entry condition: proceed confirmed
- Primary action: none (passive); optional cancel
- Key content: staged, real progress signals
- AI behavior: the actual remix computation
- Exit states: → Remix Result

**6. Remix Result**
- Purpose: let the traveler evaluate the adapted trip and decide whether it's theirs
- Entry condition: remix complete
- Primary action: "Save as my trip" / "Not quite"
- Secondary actions: expand full compare; expand reasoning on any stop; go back and adjust constraints
- Key content: adapted trip with inline kept/changed/uncertain markers, trip-level tradeoff summary, provenance, optional full compare
- AI behavior: change explanation, uncertainty flagging
- Exit states: → Saved Trip, or remain / back to Constraint Input

**7. Saved Trip**
- Purpose: confirm the traveler has their own trip, with origin traceable
- Entry condition: saved from Remix Result
- Primary action: view (no further action required at MVP)
- Key content: adapted trip, visible-but-secondary source reference
- AI behavior: none
- Exit states: end of flow, or back to Discover

---

## 12. Prototype Strategy

**Must be real** — faking any of these means the prototype tests nothing:
- Constraint-aware reasoning over the actual source trip's structured data, producing an actual adapted output
- Fixed/flexible classification and conflict detection, computed per case — not scripted per trip
- The change/reasoning explanations — generated from the real diff, not pre-written copy

**Can be simulated or hardcoded** — a portfolio prototype, not a production platform:
- The trip catalog itself: hand-curated, static, 20–50 trips, matching the Brief's manual seed approach
- Creator identity: minimal placeholder data, no real accounts or publishing flow
- Pricing/availability: stays a budget tier throughout, never live data
- Persistence: session or local state is sufficient to demonstrate save — no auth or backend database needed
- Discovery ranking: a static or lightly filtered list is fine; no algorithm required

**Guiding rule:** simulate anything that doesn't touch the hypothesis; keep real anything that does. The one thing that can never be faked is the remix reasoning itself — that's the entire point of building this.

---

## 13. UX Risks

- **Constraint-entry friction.** Even a "minimal" form can start to feel like a booking form if it's not disciplined — real risk of scope creep under the guise of "just a couple more fields."
- **Cognitive load at Fixed/Flexible Review.** Over-explaining every stop's status before the traveler has seen any payoff risks front-loading complexity before value is demonstrated. Keep this terse by default, expandable on demand.
- **AI opacity, disguised as transparency.** If the "during remix" messaging is decorative rather than tied to real reasoning stages, it undermines the exact principle it's meant to demonstrate.
- **Provenance going visually quiet.** Because Trust Decision and Save are merged into Remix Result, there's a real risk that provenance gets crowded out by the adapted content itself. This needs active protection — it's central to the hypothesis, not a footnote.
- **Remix reading as indistinguishable from generation.** If too much changes, or kept elements aren't clearly marked, the traveler may not perceive any difference from a cold-generated itinerary. This is a specific and serious risk: it would produce a false negative on the hypothesis — the UX failing to *show* the difference, not evidence that no difference exists — and the two are easy to conflate when reading results.
- **Comparison overreach.** If full side-by-side becomes the default instead of an optional expansion, it buries the one question that matters — "is this still that trip, but mine" — under detail nobody asked for.
- **Illegible change markers.** If seeing what changed requires too many taps, travelers will skim past the very thing being tested.

---

## 14. Final UX Principle

WAYFIND's UX should make the traveler feel like they've **inherited someone else's good judgment and made it their own** — not that they received an answer from a machine. Every screen should reinforce recognition over invention: this is still recognizably a real person's trip, now unmistakably shaped around them.
