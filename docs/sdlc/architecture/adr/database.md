<!-- sdlc:auto:start adr -->
# ADR-0003: Use PostgreSQL 16 for Database

Status: Accepted  
Date: 2026-11-17

## Context and Problem Statement

Which Database technology does the project use? Decided in architecture v1.

## Considered Options

- PostgreSQL 16
- No database
- SQLite

## Decision Outcome

Chosen option: PostgreSQL 16, because PostgreSQL 16 is named as the default database of record even though the stateless, history-free design (NFR-004) means it stores nothing today.

## Consequences

It runs empty and adds hosting cost with no current use; it is retained only so future optional storage (e.g. anonymous counts) has a home without a stack change.
<!-- sdlc:auto:end adr -->