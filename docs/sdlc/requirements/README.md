# Product Requirements

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start narrative -->
## Summary

### REQ-STACK-001 · approved · source: requirements:technology-stack

Product owner approved a specific, fixed technology stack for a stateless, browser-only calculator: React frontend, FastAPI backend for page-serving only, AWS hosting, and PostgreSQL named as the default database of record though unused.

Backend: FastAPI 0.115 -- no server-side calculation logic is needed; FastAPI only serves the web page and leaves room for future additions (e.g. usage analytics). Cloud: AWS -- chosen for cheap, reliable hosting of what is effectively a static single page, able to absorb large traffic spikes without server management. Database: PostgreSQL 16 -- no history or data is stored since sessions are stateless; PostgreSQL is named only as the default of record and would sit empty unless usage counts are added later. Frontend: React 19 -- this is effectively the entire product: a single responsive page with an on-screen button keypad, physical keyboard listening, running calculation display, and a division-by-zero error state, all handled client-side in the browser.

### REQ-SCOPE-001 · approved · source: requirements:delivery-scope

Delivery scope is lightweight, requirements version 1, approved. In-scope capabilities cover core arithmetic, percentage, input methods, responsiveness, and anonymous/free/stateless use.

In scope: four-function arithmetic (add, subtract, multiply, divide), percentage calculation, clear/reset display, decimal number entry, division-by-zero error state, negative result handling, on-screen button keypad, physical keyboard input, responsive layout for desktop and mobile, anonymous use with no login or account, free to use with no payments or billing, and stateless sessions with no calculation history stored. No out-of-scope items were listed in the input.

### REQ-FUNC-CALC · approved · source: requirements:functional:Doing calculations

Feature group covering the core arithmetic operations, percentage, decimal entry, negative results, division-by-zero error handling, and clear/reset.

- Add, subtract, multiply and divide: perform the four basic operations and show the result on equals (e.g. 7 add 5 shows 12; 20 divided by 4 shows 5).
- Calculate a percentage: apply a percentage within a calculation (e.g. 200 multiply 10 then percentage then equals shows 20) or view the decimal equivalent of a standalone percentage (e.g. 50 with percentage shows 0.5).
- Enter decimal numbers: allow decimal points in numbers; pressing the decimal key again on a number that already has one does not add a second point.
- Show negative results: display results below zero with a minus sign (e.g. 3 subtract 10 shows -7).
- Division-by-zero error state: dividing by zero shows a clear error state, the calculator keeps working, and pressing clear dismisses the error and resets the display to 0.
- Clear and reset the display: clears the current entry, removes any pending operation, clears any error, and returns the display to 0.

### REQ-FUNC-KEYPAD · approved · source: requirements:functional:Using the keypad

Feature group covering the two supported input methods: on-screen keypad and physical keyboard.

- On-screen button keypad: buttons for digits 0-9, decimal point, the four operators, percentage, clear, and equals; each press updates the display and proceeds as if typed.
- Physical keyboard input: digits and operators can be typed, Enter shows the result, and a mapped key such as Escape clears the display; behavior matches the on-screen keypad.

### REQ-FUNC-OPEN · approved · source: requirements:functional:Opening the calculator

Feature group covering anonymous, no-cost access to the calculator.

- Open without an account: anyone can open and use the calculator immediately with no login, sign-up, or account prompt, and no personal identity is ever required.
- Free to use: no payment, subscription, or billing is requested at any point when performing calculations or using any feature.

### REQ-NFR-001 · approved · source: requirements:NFR-001

Usability requirement: layout must adapt to desktop and mobile screen sizes.

The calculator must present a responsive layout: on desktop the keypad and display suit a large screen with readable, usable controls; on mobile the keypad and display reflow to fit the smaller screen with buttons large enough to tap accurately.

### REQ-NFR-002 · approved · source: requirements:NFR-002

Compatibility requirement: must run as a single-page web app in both desktop and mobile browsers.

The calculator must run as a single-page web app in a browser on both desktop and mobile devices.

### REQ-NFR-003 · approved · source: requirements:NFR-003

Availability requirement: edge cases such as division by zero must never crash the calculator.

The calculator must handle edge cases such as division by zero by showing a visible error state and staying usable, rather than crashing, so the user can clear and continue.

### REQ-NFR-004 · approved · source: requirements:NFR-004

Privacy requirement: anonymous use with nothing stored server-side and no retained history.

The calculator must be usable with no login, account, or personal identity, must keep no history of calculations, and must store nothing server-side; reloading or reopening the page starts fresh at 0 with no prior calculations retained.

### REQ-NFR-005 · approved · source: requirements:NFR-005

Scalability requirement: must remain available during large, unexpected traffic spikes without manual server management.

The hosted calculator must remain available and responsive during large, unexpected spikes in visitor traffic without manual server management.
<!-- sdlc:auto:end narrative -->

<!-- sdlc:auto:start summary -->
**Requirements version:** v1  
**Delivery scope:** lightweight  
**Approved:** 2026-11-17

**Capabilities in scope:** Four-function arithmetic (add, subtract, multiply, divide), Percentage calculation, Clear / reset display, Decimal number entry, Division-by-zero error state, Negative result handling, On-screen button keypad, Physical keyboard input, Responsive layout for desktop and mobile, Anonymous use with no login or account, Free to use with no payments or billing, Stateless sessions with no calculation history stored

**Approved technology stack:**

| Layer | Choice | Rationale |
|---|---|---|
| backend | FastAPI | The calculator needs no server logic at all — every calculation happens in the browser and nothing is stored. FastAPI is included only to serve the web page and give you a place to add something later (say, usage analytics) if you ever want it. It is the lightest of the backend options to stand up for simply hosting the app. |
| cloud | AWS | A free public web tool needs cheap, reliable hosting that scales if it unexpectedly gets popular, and AWS covers that comfortably. Because the app is a static-feeling single page, it can be served inexpensively — effectively pennies — and handle large traffic spikes without you managing servers. |
| database | PostgreSQL | The product keeps no history and stores no data — every session is stateless by design, so there is genuinely nothing to put in a database. PostgreSQL is named here only as the default of record; it would sit empty unless you later decide to store something like anonymous usage counts. |
| frontend | React | This is the whole product: a single responsive page with a button keypad that also listens for physical keyboard input, and an error state for division by zero. React handles all of that — the display, the button grid that reflows between phone and desktop, and the running calculation — entirely in the visitor's browser. Since nothing is saved and there are no users, the frontend is effectively the entire application. |
<!-- sdlc:auto:end summary -->

<!-- sdlc:auto:start epics -->
## EPIC-001: Core Arithmetic Calculation

The calculator performs the standard four-function arithmetic (addition, subtraction, multiplication, division) plus percentage, supports decimal number entry, and provides a clear/reset action. Scope note: no scientific functions, parentheses, or memory (M+/M-/MR) are included — this is a basic four-function plus percentage calculator only.

### US-001: Add, subtract, multiply, and divide numbers

**Priority:** critical

> As a member of the general public using the calculator, I want to perform addition, subtraction, multiplication, and division on the numbers I enter, so that I can carry out everyday arithmetic calculations.

| ID | Given | When | Then |
|---|---|---|---|
| AC-001 | the calculator is open with a cleared display | I enter 7, press add, enter 5, and press equals | the display shows 12 |
| AC-002 | the calculator is open with a cleared display | I enter 9, press subtract, enter 4, and press equals | the display shows 5 |
| AC-003 | the calculator is open with a cleared display | I enter 6, press multiply, enter 3, and press equals | the display shows 18 |
| AC-004 | the calculator is open with a cleared display | I enter 20, press divide, enter 4, and press equals | the display shows 5 |

### US-002: Calculate a percentage

**Priority:** high

> As a member of the general public using the calculator, I want to apply a percentage to a number, so that I can work out percentages without a separate step.

| ID | Given | When | Then |
|---|---|---|---|
| AC-005 | the calculator is open with a cleared display | I enter 200, press multiply, enter 10, and press the percentage key followed by equals | the display shows the result 20 |
| AC-006 | the calculator is open with a cleared display | I enter 50 and press the percentage key | the display shows 0.5 as the decimal equivalent of the percentage |

### US-003: Enter decimal numbers

**Priority:** high

> As a member of the general public using the calculator, I want to enter numbers that include a decimal point, so that I can calculate with non-whole values.

| ID | Given | When | Then |
|---|---|---|---|
| AC-007 | the calculator is open with a cleared display | I enter 2.5, press add, enter 1.3, and press equals | the display shows 3.8 |
| AC-008 | I am entering a number that already contains a decimal point | I press the decimal point key again | no second decimal point is added and the number remains valid with a single decimal point |

### US-004: Clear and reset the display

**Priority:** high

> As a member of the general public using the calculator, I want to clear the current entry and reset the calculator, so that I can start a new calculation from scratch.

| ID | Given | When | Then |
|---|---|---|---|
| AC-009 | the display shows a number or a result | I press the clear key | the display resets to 0 and no pending operation remains |
| AC-010 | the calculator is in an error state | I press the clear key | the error is dismissed and the display resets to 0 ready for a new calculation |

## EPIC-002: Edge Case and Error Handling

The calculator handles decimals, negative results, and division-by-zero gracefully, showing an error state rather than crashing. This surfaces the open assumption that these edge cases are handled with a visible error state.

### US-005: Handle division by zero gracefully

**Priority:** high

> As a member of the general public using the calculator, I want a clear error message when I divide by zero, so that the calculator does not crash and I understand the operation is invalid.

| ID | Given | When | Then |
|---|---|---|---|
| AC-011 | the calculator is open with a cleared display | I enter 8, press divide, enter 0, and press equals | the display shows an error state indicating the operation is not valid, and the calculator does not crash |
| AC-012 | the display is showing a division-by-zero error | I press the clear key | the error clears and the display resets to 0 ready for a new calculation |

### US-006: Show negative results

**Priority:** medium

> As a member of the general public using the calculator, I want negative results to be displayed correctly, so that I can trust the calculator when a result is below zero.

| ID | Given | When | Then |
|---|---|---|---|
| AC-013 | the calculator is open with a cleared display | I enter 3, press subtract, enter 10, and press equals | the display shows -7 |

## EPIC-003: Input Methods

Users can operate the calculator using an on-screen button keypad and using physical keyboard input, on both desktop and mobile. This surfaces the open assumption that both input methods are supported.

### US-007: Operate the calculator with the on-screen keypad

**Priority:** critical

> As a member of the general public using the calculator, I want to tap or click on-screen buttons for digits and operations, so that I can use the calculator with a mouse or touchscreen without a keyboard.

| ID | Given | When | Then |
|---|---|---|---|
| AC-014 | the calculator is open | I click or tap the on-screen digit and operator buttons to enter a calculation | each pressed button updates the display and the calculation proceeds as if typed |
| AC-015 | the calculator is open | I view the keypad | buttons for digits 0-9, decimal point, the four operators, percentage, clear, and equals are all present |

### US-008: Operate the calculator with a physical keyboard

**Priority:** high

> As a member of the general public using the calculator on a device with a keyboard, I want to type numbers and operators on my physical keyboard, so that I can calculate faster without clicking on-screen buttons.

| ID | Given | When | Then |
|---|---|---|---|
| AC-016 | the calculator is open | I type digit keys, an operator key, and the Enter key | the display updates as with the on-screen keypad and the result is shown on Enter |
| AC-017 | the calculator is open | I press the keyboard key mapped to clear (such as Escape) | the display resets to 0 ready for a new calculation |

## EPIC-004: Responsive Web Delivery

The calculator is delivered as a responsive single-page web app that works in a browser on both desktop and mobile. This surfaces the open assumption about the delivery platform.

### US-009: Use the calculator on desktop and mobile browsers

**Priority:** high

> As a member of the general public, I want the calculator layout to adapt to my screen size, so that I can use it comfortably on either a desktop or a mobile device.

| ID | Given | When | Then |
|---|---|---|---|
| AC-018 | I open the calculator in a desktop browser | the page loads | the keypad and display are shown in a layout suited to a large screen with readable, usable controls |
| AC-019 | I open the calculator in a mobile browser | the page loads | the keypad and display reflow to fit the smaller screen with buttons large enough to tap accurately |

## EPIC-005: Open, Free, Anonymous and Stateless Access

Anyone can open and use the calculator anonymously with no login or account, it is free to use with no payments or billing, and sessions are stateless — no calculation history is kept and nothing is stored server-side. This surfaces the open assumptions about users, payments, and data persistence.

### US-010: Use the calculator without an account

**Priority:** critical

> As a member of the general public, I want to open and use the calculator without signing in or creating an account, so that I can calculate immediately without any barrier or identity.

| ID | Given | When | Then |
|---|---|---|---|
| AC-020 | I navigate to the calculator in a browser | the page loads | the calculator is immediately usable with no login, sign-up, or account prompt |
| AC-021 | I am using the calculator | I complete calculations | no personal identity or login is ever required to continue |

### US-011: Use the calculator free of charge

**Priority:** medium

> As a member of the general public, I want to use the calculator without any payment, so that there is no cost or billing barrier to using it.

| ID | Given | When | Then |
|---|---|---|---|
| AC-022 | I am using the calculator | I perform any calculation or use any feature | no payment, subscription, or billing is requested at any point |

### US-012: Keep each session stateless with no stored history

**Priority:** medium

> As a member of the general public who values privacy, I want the calculator to keep no history and store nothing about my calculations, so that my activity is private and each session starts fresh.

| ID | Given | When | Then |
|---|---|---|---|
| AC-023 | I have performed several calculations | I look for a history of past calculations | no history is shown because none is kept |
| AC-024 | I have performed calculations and then reload the page or reopen the calculator | the page loads again | the display starts at 0 with no prior calculations retained, confirming nothing was stored server-side or carried across sessions |
<!-- sdlc:auto:end epics -->
