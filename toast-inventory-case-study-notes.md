# Toast Inventory Management — Case Study Working Document

**Role targeting:** Associate Product Designer, Toast Retail
**Focus area:** Date-based stock allocation for preorder-heavy quick-service restaurants
**Status:** Pre-design phase — user interviews not yet conducted

---

## Context

This case study is being developed as a portfolio piece to support a job application to Toast's Associate Product Designer role on the Toast Retail team. The candidate brings direct domain expertise as an operator of Mamaleh's Delicatessen (three locations: Cambridge, Brookline, Somerville), with daily hands-on experience using Toast POS across regular service, catering, and wholesale operations.

The role explicitly calls out AI Integration & Judgment, fast prototyping tools (v0, Magic Patterns, Figma Make), and familiarity with inventory management workflows — all areas this case study directly addresses.

---

## Problem Framing

### Who is the user?

The primary persona for this case study is the **operations manager or experienced shift lead** at a quick-service or hybrid restaurant that accepts preorders. This is not a novice user — the scheduling interface being proposed is explicitly scoped to manager-level access, with only the 86 action exposed to floor staff.

Secondary persona: the **customer placing a preorder** for a future date, who currently faces either "item unavailable" blocks or post-order cancellations due to inventory conflicts.

### Documented Pain Points (from operator experience)

**Pain Point 1 — No date-based stock quantities**
Toast only tracks stock for the current moment. For quick-service restaurants accepting preorders, this creates an impossible tradeoff: limiting stock to prevent today's overselling blocks legitimate future-date preorders; being liberal with counts risks overselling today and losing customer goodwill. There is no mechanism to say "we have 30 of this item available for Saturday" independently of today's count.

**Pain Point 2 — Items with shared ingredients cannot share a stock limit**
Multiple menu items using the same ingredient (e.g., all turkey sandwiches) each have independent stock counts. When turkey runs out, each item must be manually 86'd individually. There is no way to tie them to a shared ingredient-level pool that auto-limits all affected items simultaneously.

**Pain Point 3 — Ordering channels have separate inventory pools**
Items sold on the regular POS/online menu and catering do not share inventory. Counts cannot limit cross-channel sales without manually splitting allocations between channels — which requires ongoing supervision and creates underselling risk when one channel sells out and the other still shows availability.

**Pain Point 4 — Fractional inventory quantities when not needed**
Quantities default to floating point numbers, adding unnecessary keystrokes when managing whole-unit items during busy service.

### Operator Wishlist

- Ability to set stock quantities for specific future dates
- Allow preorders for future dates even when an item is out of stock today

---

## Competitive Analysis

*Full report compiled from official documentation, Capterra, G2, Software Advice, and community forums.*

### Lightspeed Restaurant

**Strongest feature:** Recipe-based ingredient tracking with automatic 86-ing. When a shared ingredient depletes to zero, all menu items requiring that ingredient are automatically marked unavailable across POS and online ordering (U-Series). This directly solves Pain Point 2. Single underlying inventory feeds all ordering surfaces, largely solving Pain Point 3.

**Key limitation:** No date-based stock quantities. Identical to Toast's limitation. Order Ahead supports future pickup times but cannot accept preorders for currently out-of-stock items.

**UX notes:** Inventory management lives in a separate back-office browser module, distinct from the iPad POS. Users report it is "more complicated than it needed to be" for multi-location operators. Claims 40% fewer clicks for POS workflows but back-of-house inventory is a separate surface.

**Pricing:** $189/month (Essential) to $399+/month (Premium) for full recipe and Produce module features.

**Scorecard vs. Toast pain points:**

| Pain Point | Verdict |
|---|---|
| No date-based stock | ❌ Same limitation |
| No shared-ingredient stock limits | ✅ Solved via recipe system + auto-86 (U-Series) |
| Separate channel inventory pools | ✅ Largely solved |
| Fractional quantity friction | ⚠️ Same behavior, but contextually logical for recipe math |

---

### Square for Restaurants

**Strongest feature:** Cross-channel inventory unification. A single inventory pool feeds POS, Square Online, Kiosk, and all third-party delivery integrations (DoorDash, Uber Eats, Grubhub) in real time. Auto-86 propagates everywhere simultaneously. This is the clearest competitive advantage over Toast and directly solves Pain Point 3.

**Key limitation:** No native ingredient-level tracking. Square explicitly acknowledges its inventory tracks finished goods only and directs operators to the MarketMan add-on ($99/month) for ingredient decomposition. Date-based stock is also absent — bakery operators in community forums report losing sales when preorder quantities exceed today's count.

**Notable:** Square's community forums document the exact same preorder problem Mamaleh's experiences. One bakery owner: a customer wants 24 cupcakes for next Friday but today's inventory is 4 — the system blocks the order. A moderator workaround (separate "advance order" items set to sell when out of stock) was acknowledged as "potential to get super messy."

Square does support **scheduled inventory restocks** — setting a future date/time when a sold-out item becomes available again. This is the starting-point concept for date-based allocation but stops well short of per-date quantity limits.

**UX notes:** Praised universally for ease of use and ease of staff training. However, inventory management is primarily a desktop/Dashboard experience with limited mobile functionality, and item availability can only be adjusted one item at a time — no bulk editing.

**Pricing:** Free plan covers basic availability and auto-86. Plus plan ($49/month/location) adds purchase orders, vendor management, COGS reports. MarketMan add-on $99/month/location additional.

**Scorecard vs. Toast pain points:**

| Pain Point | Verdict |
|---|---|
| No date-based stock | ❌ Same limitation — operators explicitly report lost sales |
| No shared-ingredient stock limits | ❌ Same natively; $99/month add-on solves it |
| Separate channel inventory pools | ✅ Strong advantage — best in class cross-channel sync |
| Fractional quantity friction | ⚠️ More configurable via stock conversion feature |

---

### MarketMan

**Strongest feature:** Deepest ingredient-level intelligence available. Full sub-recipe nesting, modifier-level deduction (extra cheese, substitutions all tracked), real-time recipe costing that updates when supplier prices change, and theoretical vs. actual food cost reporting. AI recipe creation from uploaded ingredient photos. Integrates with 28+ POS platforms including Toast.

**Critical limitation:** POS integration is **one-way only**. Sales data flows from POS → MarketMan, but MarketMan cannot push data back to the POS to auto-86 items. MarketMan can alert an operator that turkey is running low, but cannot automatically disable all turkey sandwiches on the POS or online ordering. The operator must still manually 86 each item — the same workflow Toast operators find painful. No date-based stock functionality.

**UX notes:** Capterra 4.7/5 across 112 reviews. Interface is praised as beautiful and well-organized. However, initial setup is universally described as time-consuming (G2 Ease of Setup: 7.4/10). Recurring complaints: unreliable invoice scanning, slow feature development, difficult cancellation. One Toast operator noted: "Toast is a great POS for in-store use but terrible as an administrator. Marketman helps a lot since it uses the sales data from Toast."

**Pricing:** $199/month (Starter), $249/month (Growth). $500 one-time setup fee. Square partnership rate: $99/month, no setup fee.

**Scorecard vs. Toast pain points:**

| Pain Point | Verdict |
|---|---|
| No date-based stock | ❌ Not supported |
| No shared-ingredient stock limits | ✅ Best ingredient tracking but ❌ cannot auto-86 due to one-way integration |
| Separate channel inventory pools | ⚠️ Unified visibility, no bidirectional control |
| Fractional quantity friction | Insufficient data |

---

### Key Finding: Industry-Wide Market Gap

**Date-based preorder inventory allocation is unsolved across the entire restaurant technology market.** Lightspeed, Square, MarketMan, Revel, Apicbase, BlueCart, Restaurant365, Rezku, Craftable, CrunchTime, Oracle Simphony, and KORONA POS were all evaluated. None offer the ability to set stock quantities tied to specific future dates.

BentoBox (by Fiserv) comes closest — its Pre-Order & Catering product allows menu visibility to change based on fulfillment date — but it is unclear whether it supports per-date quantity limits vs. only date-based menu availability.

**This is a genuine whitespace opportunity for Toast**, particularly as the platform expands into retail and hybrid restaurant/retail models where date-based batch production and preorder inventory are common operating patterns.

### UX Patterns Worth Borrowing

- **Lightspeed's ingredient-to-stock cascade** — auto-86 triggered by shared ingredient depletion, not manual item-by-item action
- **Square's unified channel architecture** — single inventory pool feeding all ordering surfaces simultaneously
- **Square's scheduled restock interaction** — the conceptual starting point for date-based availability; needs extension to per-date quantity limits
- **MarketMan's modifier-level deduction** — tracks ingredient cost at the modification level, not just the base item
- **Rezku's countdown warnings** — surfacing "3 remaining" before an item hits zero, allowing proactive front-of-house management

---

## Proposed Feature: Date-Based Stock Scheduling

### Scope decision

**MVP focus:** Date-based stock allocation at the menu item level. Ingredient-level cascading (auto-86 triggered by shared ingredient depletion) is deferred to a future phase due to dependency on xtraCHEF data connectivity.

**Rationale for deferral:** The date-based scheduling problem is valuable enough on its own to justify the feature. Ingredient cascading adds an infrastructure dependency outside the scope of this UX redesign. Solving one thing completely is more defensible than solving two things partially.

### Concept overview

A manager-level scheduling interface consisting of two panels: a menu item selector on the left, and a calendar on the right. The interface sits behind a permission gate — manager or experienced employee access only. Floor staff retain access to the standard 86 action.

**Core interaction model:**
- Select one or more menu items from the left panel
- Navigate to a date on the calendar
- Input a stock event for that date: mark as in stock (no quantity limit), set a specific quantity, or 86 (mark unavailable)
- Stock events propagate forward to future dates until overridden by a later event on the same item

**Default state:** When no stock events have been set, the calendar mirrors the item's current stock status across all dates. This ensures zero behavior change for operators who never use the scheduling tool, preserving existing workflows.

**Perishable use case:** A date range can be set with a quantity on the first day and an auto-86 on the final day (item expiration). This is a novel feature with no equivalent in any competing platform, directly addressing the food-and-beverage-specific challenge of perishable batch items.

**Example workflows:**
- Soda restock every Friday: multiselect all soda items, navigate to Friday, set "in stock." No end date needed — they remain in stock until manually 86'd for unforeseen circumstances.
- Limited-run holiday item: set quantity of 50 on the first available date, set auto-86 on the sell-by date. Between those events, the quantity decrements with each sale.
- Preorder for Saturday pickup: manager sets Saturday's turkey sandwich count to 40. Preorders placed Thursday and Friday decrement against Saturday's count, not today's.

### Open design questions (to resolve during sketching)

- Left panel structure: flat item list, category-grouped, or menu-level drill-down?
- Multiselect pattern: checkboxes, tag selection, or another pattern?
- Calendar event display: dot indicator, colored bar, quantity label, or range indicator?
- Input form: what fields appear when a user clicks a date?
- Timeline/overview view: is a Gantt-style row-per-item view needed for reviewing the week's state, separate from the calendar editing view?
- Cold-start onboarding: what does a first-time user see and what action is most obvious?

---

## Case Study Structure (To Be Built)

### Steps remaining before design

1. **User interviews** (3-5 operators, 20-30 min each) — highest priority, cannot be delegated to AI
   - Discussion guide topics: current workarounds for preorder stock, last time they lost a sale due to inventory conflict, last time they had to 86 something mid-service, how they currently plan stock for future days
   - Goal: capture direct quotes that anchor the problem statement in real operator experience

2. **Synthesis** — affinity map interview findings, finalize "How might we" problem statement, confirm MVP scope against user feedback

3. **Low-fi sketches** — rough hand-drawn wireframes answering the open design questions above; focus on thinking, not polish

4. **Mid-fi Figma wireframes** — apply Toast's design system; annotate key decisions

5. **Prototype** — clickable Figma prototype or working React prototype covering the core scheduling flow

6. **Validation** — walk 1-2 operators through the prototype; document findings

7. **Write-up** — assemble into a case study with problem framing, research, synthesis, design decisions, prototype, and reflection

### Narrative arc for the case study

> As an operator of a three-location delicatessen running Toast POS, I identified a recurring inventory problem that cost us real revenue: there was no way to accept preorders for future dates without either blocking today's sales or risking overselling. I researched how every major competitor handles this problem and discovered that **no platform in the restaurant tech market has solved it**. I then designed a solution.

This narrative combines operator credibility, research rigor, and design initiative in a way that directly maps to Toast's stated design tenets: founder's mentality, building strong perspectives, and driving action through influence.

---

## Notes on AI-Assisted Workflow

This case study is being developed using an AI-augmented design process, which is directly relevant to the role's "AI Integration & Judgment" requirement. Specific uses:

- Competitive research synthesis (Claude)
- Case study structure and design thinking frameworks (Claude)
- UI generation for prototyping (v0, Figma Make, or Claude artifacts)
- Case study writeup drafting (Claude, with operator-supplied details and quotes)

User interviews, low-fi sketching, and design critique are intentionally not delegated to AI — these steps require operator judgment and human observation that strengthen rather than replace the design rationale.
