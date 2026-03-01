---
id: TASK-1.5
title: Build interactive prototype
status: To Do
assignee: []
created_date: '2026-02-26 21:34'
updated_date: '2026-03-01 04:30'
labels:
  - design
  - prototype
dependencies:
  - TASK-1.4
parent_task_id: TASK-1
priority: medium
ordinal: 5000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Create a clickable prototype covering the core date-based stock scheduling flow. This can be a Figma prototype or a working React prototype — choose based on what best demonstrates the interaction model.

The prototype should cover the primary happy path:
1. Manager opens the scheduling interface
2. Selects one or more menu items
3. Navigates to a future date
4. Sets a stock quantity for that date
5. Sees the event reflected on the calendar
6. Views how the quantity propagates forward

Secondary flows to include if feasible:
- 86-ing an item for a specific date
- Setting a perishable date range (quantity on start date, auto-86 on end date)
- Preorder scenario where future-date quantity decrements

The prototype will be used for operator validation in the next phase, so it needs to be realistic enough to elicit meaningful feedback.

AI tools (v0, Figma Make, Claude artifacts) can and should be used for generation, which is directly relevant to the role's AI Integration & Judgment requirement.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 Core scheduling flow is interactive end-to-end (select items, pick date, set quantity, see result)
- [ ] #2 Prototype is realistic enough for operator validation testing
- [ ] #3 At least one secondary flow (86, perishable range, or preorder) is interactive
- [ ] #4 AI-assisted generation is documented for the case study's AI workflow narrative
<!-- AC:END -->
