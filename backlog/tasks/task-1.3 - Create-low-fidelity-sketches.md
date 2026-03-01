---
id: TASK-1.3
title: Create low-fidelity sketches
status: To Do
assignee: []
created_date: '2026-02-26 21:33'
updated_date: '2026-03-01 04:30'
labels:
  - design
  - human-only
dependencies:
  - TASK-1.2
parent_task_id: TASK-1
priority: medium
ordinal: 3000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Produce rough hand-drawn wireframes that answer the open design questions identified during problem framing. The focus is on thinking and exploration, not polish.

Open design questions to resolve:
1. Left panel structure: flat item list, category-grouped, or menu-level drill-down?
2. Multiselect pattern: checkboxes, tag selection, or another pattern?
3. Calendar event display: dot indicator, colored bar, quantity label, or range indicator?
4. Input form: what fields appear when a user clicks a date?
5. Timeline/overview view: is a Gantt-style row-per-item view needed for reviewing the week's state, separate from the calendar editing view?
6. Cold-start onboarding: what does a first-time user see and what action is most obvious?

The proposed feature is a two-panel interface: menu item selector on the left, calendar on the right. Core interactions include selecting items, navigating to a date, and inputting stock events (in stock, specific quantity, or 86). Stock events propagate forward until overridden.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 Each of the 6 open design questions has at least one sketched solution
- [ ] #2 Two-panel layout (item selector + calendar) is explored in multiple variations
- [ ] #3 Core stock event input flow is sketched end-to-end
- [ ] #4 Perishable use case (date range with auto-86) is represented
- [ ] #5 Preorder use case (future-date quantity decrementing) is represented
- [ ] #6 Sketches are documented (photos or scans) for reference in later phases
<!-- AC:END -->
