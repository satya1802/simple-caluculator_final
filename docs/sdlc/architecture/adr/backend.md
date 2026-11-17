<!-- sdlc:auto:start adr -->
# ADR-0002: Use FastAPI 0.115 for Backend

Status: Accepted  
Date: 2026-11-17

## Context and Problem Statement

Which Backend technology does the project use? Decided in architecture v1.

## Considered Options

- FastAPI 0.115
- Flask
- Node/Express
- Static-only (no backend)

## Decision Outcome

Chosen option: FastAPI 0.115, because FastAPI 0.115 is the lightest approved way to host the built page and expose a health check, leaving a place to add optional server features such as anonymous usage counts later.

## Consequences

A backend is strictly unnecessary for calculation and sits nearly idle; the benefit is a consistent hosting surface and future extensibility at near-zero cost.
<!-- sdlc:auto:end adr -->