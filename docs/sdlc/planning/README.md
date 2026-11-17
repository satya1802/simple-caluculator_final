# Planning

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start narrative -->
### EPIC-001 · approved · source: planning:EPIC-001

Delivers standard four-function arithmetic plus percentage, decimal entry, and clear/reset. Explicitly excludes scientific functions, parentheses, and memory operations -- basic four-function plus percentage only.

Goal: provide the core arithmetic engine (add, subtract, multiply, divide, percentage), decimal number entry, and a clear/reset action, with no scientific functions, parentheses, or memory (M+/M-/MR).

**Related:** US-001, US-002, US-003, US-004

### EPIC-002 · approved · source: planning:EPIC-002

Covers graceful handling of edge cases: division by zero and negative results, with a visible error state rather than a crash.

Goal: handle decimals, negative results, and division-by-zero gracefully, showing an error state rather than crashing. Surfaces the open assumption that these edge cases are handled with a visible error state.

**Related:** US-005, US-006

### EPIC-003 · approved · source: planning:EPIC-003

Covers both supported input methods -- on-screen keypad and physical keyboard -- across desktop and mobile.

Goal: let users operate the calculator via an on-screen button keypad and via physical keyboard input, on both desktop and mobile. Surfaces the open assumption that both input methods are supported.

**Related:** US-007, US-008

### EPIC-004 · approved · source: planning:EPIC-004

Covers delivery as a responsive single-page web app that works in a browser on both desktop and mobile.

Goal: deliver the calculator as a responsive single-page web app that works in a browser on both desktop and mobile. Surfaces the open assumption about the delivery platform.

**Related:** US-009

### EPIC-005 · approved · source: planning:EPIC-005

Covers anonymous, free, and stateless access -- no login, no payment, and no server-side storage of calculation history.

Goal: allow anyone to open and use the calculator anonymously with no login or account, free of charge with no payments or billing, and with stateless sessions where no calculation history is kept and nothing is stored server-side. Surfaces the open assumptions about users, payments, and data persistence.

**Related:** US-010, US-011, US-012
<!-- sdlc:auto:end narrative -->
