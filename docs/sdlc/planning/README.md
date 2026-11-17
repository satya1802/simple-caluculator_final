# Planning

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start narrative -->
### EPIC-001 · approved · source: planning:EPIC-001

Covers the standard four-function arithmetic (add, subtract, multiply, divide), percentage calculation, decimal entry, and a clear/reset action.

Goal: deliver basic four-function plus percentage arithmetic with decimal support and a clear/reset action. Explicit scope note from input: no scientific functions, parentheses, or memory (M+/M-/MR) are included — this is a basic four-function plus percentage calculator only. Stories: US-001, US-002, US-003, US-004.

**Related:** US-001, US-002, US-003, US-004

### EPIC-002 · approved · source: planning:EPIC-002

Covers graceful handling of edge cases: negative results and division-by-zero, shown via a visible error state instead of a crash.

Goal: handle decimals, negative results, and division-by-zero gracefully, showing an error state rather than crashing. Input notes this surfaces the open assumption that these edge cases are handled with a visible error state. Stories: US-005, US-006.

**Related:** US-005, US-006

### EPIC-003 · approved · source: planning:EPIC-003

Covers operating the calculator via an on-screen button keypad and via physical keyboard input, on both desktop and mobile.

Goal: support both on-screen keypad interaction and physical keyboard interaction, on both desktop and mobile. Input notes this surfaces the open assumption that both input methods are supported. Stories: US-007, US-008.

**Related:** US-007, US-008

### EPIC-004 · approved · source: planning:EPIC-004

Covers delivering the calculator as a responsive single-page web app usable in a browser on both desktop and mobile.

Goal: deliver the calculator as a responsive single-page web app that works in a browser on both desktop and mobile. Input notes this surfaces the open assumption about the delivery platform. Story: US-009.

**Related:** US-009

### EPIC-005 · approved · source: planning:EPIC-005

Covers open, anonymous, free, and stateless access to the calculator with no login, no payment, and no stored history.

Goal: let anyone open and use the calculator anonymously with no login or account, free of charge with no payments or billing, and with stateless sessions — no calculation history kept and nothing stored server-side. Input notes this surfaces the open assumptions about users, payments, and data persistence. Stories: US-010, US-011, US-012.

**Related:** US-010, US-011, US-012

### SPRINT-1 · approved · source: planning:Sprint 1

First sprint of plan v1: build the core arithmetic engine (four functions, percentage, decimals, clear, negative results, divide-by-zero error state) and stand up the FastAPI page-serving endpoint.

Goal: Build the core arithmetic engine (four functions, percentage, decimals, clear, negative results, divide-by-zero error state) and stand up the FastAPI page-serving endpoint. Capacity: 20 points. Plan version 1, status approved. Note: the input's backlog item list does not explicitly assign items to Sprint 1 vs Sprint 2; the stories linked here (US-001 through US-006, under EPIC-001 Core Arithmetic Calculation and EPIC-002 Edge Case and Error Handling) are grouped by thematic match to this sprint's goal wording, not by an explicit per-sprint tag in the input.

**Related:** EPIC-001, EPIC-002, US-001, US-002, US-003, US-004, US-005, US-006

### SPRINT-2 · approved · source: planning:Sprint 2

Second sprint of plan v1: wire the on-screen keypad and physical keyboard to the calculation engine, make the layout responsive for desktop/mobile, and confirm free, stateless, anonymous use.

Goal: Wire the on-screen keypad and physical keyboard to the calculation engine, make the layout responsive for desktop/mobile, and confirm free, stateless, anonymous use. Capacity: 20 points. Plan version 1, status approved. Note: the input's backlog item list does not explicitly assign items to Sprint 1 vs Sprint 2; the stories linked here (US-007 through US-012, under EPIC-003 Input Methods, EPIC-004 Responsive Web Delivery, and EPIC-005 Open, Free, Anonymous and Stateless Access) are grouped by thematic match to this sprint's goal wording, not by an explicit per-sprint tag in the input.

**Related:** EPIC-003, EPIC-004, EPIC-005, US-007, US-008, US-009, US-010, US-011, US-012
<!-- sdlc:auto:end narrative -->
