# Sprint Plan

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start sprints -->
## Sprint 1: Sprint 1

Build the core arithmetic engine (four functions, percentage, decimals, clear, negative results, divide-by-zero error state) and stand up the FastAPI page-serving endpoint.

Capacity: 20 points · Committed: 20

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-001 | Story | Add, subtract, multiply, and divide numbers | 5 | frontend-agent | — |
| US-002 | Story | Calculate a percentage | 3 | frontend-agent | US-001 |
| US-003 | Story | Enter decimal numbers | 3 | frontend-agent | US-001 |
| US-004 | Story | Clear and reset the display | 2 | frontend-agent | US-001 |
| US-005 | Story | Handle division by zero gracefully | 3 | frontend-agent | US-001 |
| US-006 | Story | Show negative results | 2 | frontend-agent | US-001 |
| US-010 | Story | Use the calculator without an account | 2 | backend-agent | — |

## Sprint 2: Sprint 2

Wire the on-screen keypad and physical keyboard to the calculation engine, make the layout responsive for desktop/mobile, and confirm free, stateless, anonymous use.

Capacity: 20 points · Committed: 14

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-007 | Story | Operate the calculator with the on-screen keypad | 5 | frontend-agent | US-001 |
| US-008 | Story | Operate the calculator with a physical keyboard | 3 | frontend-agent | US-007 |
| US-009 | Story | Use the calculator on desktop and mobile browsers | 3 | frontend-agent | US-007 |
| US-011 | Story | Use the calculator free of charge | 1 | frontend-agent | — |
| US-012 | Story | Keep each session stateless with no stored history | 2 | frontend-agent | US-010 |

## Unscheduled

_Nothing unscheduled._
<!-- sdlc:auto:end sprints -->
