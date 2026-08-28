# WAYFIND — Product Brief

*Source of truth for Project #1. Status: working definition, pre-prototype.*

---

## 1. Product Overview

WAYFIND is an AI-native travel product built around a single idea: the best starting point for planning a trip is a real trip someone else has already taken, not a blank page and not a trip invented from scratch by a model. Travelers can discover real, structured trips created by other travelers, then ask AI to adapt one of those trips to their own dates, budget, party, and preferences — while preserving what made the original trip worth following in the first place.

Where most AI travel tools compete on generating a personalized itinerary as fast as possible, WAYFIND treats the itinerary-generation problem as already partially solved by the person who built the original trip. The product's job is not invention — it is intent-preserving translation: taking someone else's proven judgment and re-deriving a coherent plan under a new set of constraints.

This brief describes Project #1: a small, tightly scoped prototype whose sole purpose is to test whether this idea holds up in practice. It is explicitly not a plan for a complete travel company.

---

## 2. Product Thesis

**Central thesis:** AI's most valuable role in travel planning is not generating a trip from nothing, but translating a real person's proven trip into another traveler's constraints while preserving what made it good.

**Hypothesis under test:** *A real person's proven trip is a better starting point for planning than a trip generated from scratch.*

This is a hypothesis, not a fact. Project #1 exists to produce evidence for or against it.

---

## 3. Problem

From a traveler's perspective: research is scattered across platforms, and turning inspiration into an actual, usable plan takes real, tedious effort. Fast AI-generated itineraries solve the effort problem but not the trust problem — a plan invented by a model has no track record and no accountability behind it. Meanwhile, travelers who have already done excellent planning for their own trips have no way to let that work help anyone else; it stays private in notes, spreadsheets, and chat threads. There is currently no way to say "someone already solved a version of this problem — let me start there, adapted to me."

---

## 4. Target User

**Primary MVP user:** an independent, planning-oriented traveler with a real, specific upcoming trip, evaluating whether starting from someone else's proven plan is more useful than starting from nothing.

**Who we are explicitly NOT designing for yet:**
- Travelers looking for a fully automated, zero-input plan
- Travelers wanting to book or transact inside the product
- Groups or families needing multi-person collaborative planning
- Anyone looking to find travel companions or join a stranger's trip
- Casual browsers with no upcoming trip (this may become a valuable audience later, but is not who the prototype is built to convince)

---

## 5. Job To Be Done

**When** I have a real trip to plan and don't want to start from a blank page,
**I want to** adapt a trip that a real traveler already took to my own dates, budget, and preferences,
**so that** I get a plan I can trust, without doing all the research and synthesis myself.

---

## 6. Core User Scenario

A traveler has six days set aside for a trip through northern Portugal. They open WAYFIND and browse a small set of real trips other travelers have taken, filtering loosely by region. One trip — a nine-day Porto-to-Douro-Valley route built by another traveler — resonates: the pacing feels right and the highlights match their interests. Before doing anything else, they see who made it and get a sense of why it holds together as a trip.

They tell WAYFIND their constraints: six days instead of nine, a mid-range budget, traveling as a couple, and a stronger interest in food than in hiking. Before changing anything, WAYFIND shows which parts of the original trip are fixed (a specific vineyard tour with limited dates, for example) and which are flexible (the order of towns, the pacing, the restaurant choices).

WAYFIND then produces an adapted trip: three days trimmed out, pacing tightened, food-focused stops emphasized over hiking-focused ones, and a short explanation of what changed and why. The traveler compares the adapted version against the original side by side. They recognize the shape of the original trip in what they're looking at, and they now have a plan that fits their actual six days. They decide they trust it enough to use, and save their version.

---

## 7. Core Experience

**Discover → Understand → Set Constraints → Understand Fixed/Flexible → Remix → Compare → Trust Decision → Save**

- **Discover** — Browse a small set of real trips to find one that resonates as a starting point.
- **Understand** — See what the trip is, who made it, and why it holds together, before committing to adapt it.
- **Set Constraints** — Provide the hard facts that make the trip personal: dates, budget, party, one or two preferences.
- **Understand Fixed/Flexible** — See which parts of the original trip can and cannot change, before any changes are made, so the coming adaptation is legible rather than a black box.
- **Remix** — AI produces an adapted version of the trip built around the stated constraints.
- **Compare** — View the adapted trip alongside the original to judge what was kept, what changed, and why.
- **Trust Decision** — Explicitly judge whether the adapted trip is good enough to use — the moment the core hypothesis is actually tested.
- **Save** — Keep the adapted trip as the traveler's own.

---

## 8. Core AI Behavior

**The AI is responsible for:**
- **Constraint reasoning** — taking a new traveler's dates, budget, party, and preferences and determining what a coherent trip under those constraints looks like, starting from the source trip rather than from nothing.
- **Distinguishing fixed vs. flexible elements** — identifying which parts of the source trip are structurally locked (time-bound bookings, dated events, fixed logistics) versus open to change, and treating that distinction as a constraint on its own reasoning, not a cosmetic label.
- **Preserving the source trip's intent** — maintaining the pacing, sequencing logic, and character of the original trip wherever the new constraints allow, rather than defaulting to a generic optimal plan.
- **Explaining changes** — stating clearly what was kept, what was changed, and why, in terms a traveler can evaluate and disagree with if needed.
- **Maintaining provenance** — keeping the connection to the original trip and its creator visible throughout the adapted output, not just at the discovery stage.

**The AI should NOT:**
- Generate a trip from scratch as its primary mode of operation — remix is the core behavior, not generation.
- Silently override a fixed element without flagging it.
- Invent details (opening hours, prices, availability) it cannot ground in the source trip or explicit input.
- Take autonomous action — no booking, no payment, no irreversible steps.
- Behave as a general-purpose travel chatbot; its scope is adapting a specific trip to specific constraints, not open-ended conversation.

---

## 9. Trip Object

The minimum structured representation required for the AI to reason correctly:

- **Ordered stops** — place, day, rough time, and type (lodging / food / sight / activity / transit)
- **Budget indicator** — a tier or rough total, not itemized pricing
- **Original party size/type and pace**
- **A fixed/flexible flag per element** — the single most important structural piece; without it, remix cannot know what to protect
- **Creator attribution**

No live pricing, no availability data, no booking references, and no routing sophistication beyond displaying sequence. This is a planning object, not a transactional one.

---

## 10. Community Layer

The minimum needed to make the concept believable without prematurely building a social product:

- A small, manually curated catalog of real trips (roughly 20–50), each with a visible origin
- Visibility into a trip's source before a traveler chooses to remix it

**Not included:** an algorithmic discovery feed, a follow graph, likes/ratings/comments, or an open publishing pipeline for arbitrary users. Supply is curated by hand for Project #1; the goal is a credible test, not a functioning marketplace.

---

## 11. MVP

Only what is required to test the hypothesis:

1. Browse a small, curated set of real trips
2. Select a trip and view its source and shape
3. Enter constraints (dates, budget tier, party, one or two preferences)
4. View the fixed/flexible breakdown of the source trip
5. Receive an AI-adapted trip with a clear explanation of what changed and why
6. Compare adapted vs. original
7. Save the adapted trip

Nothing beyond this list is part of Project #1.

---

## 12. Explicitly Out of Scope

- Open publishing for arbitrary users
- A follow/save social graph
- Finding companions or joining a stranger's trip
- Booking, payment, or live inventory integration
- Ingesting raw social content (screenshots, reels, videos)
- Multi-user collaborative editing
- In-trip, day-of, or disruption-handling features
- Monetization or creator payouts
- Offline or mobile-native functionality

---

## 13. Differentiation

- **ChatGPT** — can generate itineraries and, through app integrations, search live travel inventory conversationally. What it does not have is a persistent, structured, forkable trip object with lineage to a real person's original plan; each conversation produces a disposable output rather than an adaptation of an existing one.
- **Google Maps** — a strong tool for saving places and navigating between them, but it does not reason about a trip as a coherent whole with pacing, budget, and intent to preserve.
- **Social travel/inspiration platforms** (Instagram, TikTok, Pinterest, Xiaohongshu) — excellent for discovering inspiration, but the output is content to be manually synthesized by the traveler, not a structured plan that can be adapted directly.
- **Wanderlog** — offers a large library of browsable, shareable itineraries and templates and strong collaborative organization tools. It does not offer AI-personalized adaptation of a specific existing trip to a new traveler's constraints with explicit preservation of the original's intent.
- **Komoot / AllTrails** — the closest structural proof that "publish, discover, and customize" works as a pattern; users can save another person's route and adapt it. That pattern is proven for single-activity route geometry, not for multi-day trips with interdependent lodging, budget, and pacing decisions.
- **AI itinerary generators** (e.g., Faroway, Wanderlog's AI planner) — can produce a complete, personalized itinerary from a prompt in under a minute, for free. What they do not offer is a human-vetted source behind the output — there is no real trip being adapted, and no provenance to evaluate.

WAYFIND's position is specific: none of the above combine a real person's structured, provenance-carrying trip with AI-driven, intent-preserving adaptation to a new traveler's constraints.

---

## 14. Product Principles

1. **Start from human judgment, not a blank page.** The default input to planning is a real trip, not an empty form.
2. **Preserve intent before optimizing.** A technically efficient adaptation that discards what made the original trip distinctive has failed, even if it is otherwise correct.
3. **Make AI reasoning visible, before and after it acts.** Show what is fixed and flexible before adapting; show what changed and why afterward.
4. **Keep the traveler in the trust decision.** The product's job is to earn a "yes, I trust this," not to make the decision on the traveler's behalf.
5. **Provenance is part of the product, not metadata.** Knowing whose judgment shaped a trip is core to why the trip is useful, not a footnote.
6. **Prove the hypothesis before scaling the network.** No community, discovery, or growth investment is justified until remix is shown to outperform generation from scratch.
7. **Small and testable beats broad and impressive.** Project #1 succeeds by producing a clear answer, not by looking like a complete product.

---

## 15. Success Criteria

**Product behavior**
- The AI reliably distinguishes fixed from flexible elements in a source trip and does not silently override fixed elements.
- The AI produces an adapted trip that visibly reflects the stated constraints (dates, budget, party, preferences).
- The explanation of what changed and why is accurate and traceable to real differences between source and output.

**User experience**
- Travelers can complete the full flow — discover, set constraints, review the adaptation, compare, decide, save — without confusion about what the AI did or why.
- Travelers can articulate, in their own words, what was kept from the original trip and what was changed for them.

**Hypothesis validation**
- In direct comparison, a meaningful share of travelers prefer or trust the remixed trip over an equivalent cold-generated trip, and can explain why.
- Travelers specifically credit preserved elements of the original trip as reasons they value the adapted plan.

---

## 16. Failure Criteria

The central thesis should be considered unsupported if:
- Travelers prefer or rate a cold-generated plan equal to or higher than a comparable remix.
- Travelers abandon the constraint-entry step at a high rate, suggesting "start from someone's trip" does not reduce perceived effort.
- Travelers edit the remixed trip so heavily that little of the source trip's character survives, and say a generic plan would have served them equally well.
- Provenance and attribution have no observable effect on stated trust or satisfaction.
- The AI cannot reliably protect fixed elements, causing trust to collapse within a session.

---

## 17. Open Questions

- How much constraint input is the minimum needed for a remix to feel credible, versus enough to feel like a chore?
- How should the fixed/flexible breakdown be communicated so it informs the traveler without overwhelming them?
- How far can party size, budget, or pace shift from the original before "remix" stops being meaningfully different from generation?
- How should the "what changed and why" explanation be structured to be genuinely evaluable rather than just reassuring?
- How should a credible seed catalog of 20–50 real trips be sourced quickly without compromising quality?
- Is testing against travelers' real upcoming trips (slower, higher signal) or hypothetical/past trips (faster, weaker signal) the right validation method for Project #1?
- How much of the original trip's narrative voice or personal texture should be preserved in the adapted output, versus rewritten for clarity?

---

## 18. North Star Experience

A traveler discovers a real trip that resonates with them, and sees who made it and why it holds together before doing anything else. They understand its shape — its pacing and highlights — well enough to decide it's worth adapting. They tell WAYFIND their own constraints: dates, budget, party, and what matters most to them. Before anything changes, WAYFIND shows them what in the original trip is fixed and what is flexible, so the adaptation that follows is legible rather than a black box. WAYFIND then produces their version, explaining clearly what it kept, what it changed, and why. They compare their adapted trip against the original, decide whether they trust it enough to use, and save their version.

---

**WAYFIND exists to test one fundamental idea: a real trip someone else has already taken and vouches for is a better starting point for AI-assisted planning than a trip invented from nothing.**
