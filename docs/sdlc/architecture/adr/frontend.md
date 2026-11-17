<!-- sdlc:auto:start adr -->
# ADR-0001: Use React 19 for Frontend

Status: Accepted  
Date: 2026-11-17

## Context and Problem Statement

Which Frontend technology does the project use? Decided in architecture v1.

## Considered Options

- React 19
- Vue 3
- Svelte
- Vanilla JS

## Decision Outcome

Chosen option: React 19, because React 19 renders the whole product in the browser: the display, a responsive button grid that reflows between phone and desktop, a keyboard listener, and the calculation state including the division-by-zero error state and negative results.

## Consequences

React is heavier than vanilla JS for a tool this small, but its component model and hooks make the keypad, keyboard handling and responsive layout clean and testable, and it is the approved stack.
<!-- sdlc:auto:end adr -->