<!-- sdlc:auto:start adr -->
# ADR-0004: Use AWS for Cloud

Status: Accepted  
Date: 2026-11-17

## Context and Problem Statement

Which Cloud technology does the project use? Decided in architecture v1.

## Considered Options

- AWS
- Vercel
- Netlify
- GCP

## Decision Outcome

Chosen option: AWS, because AWS serves the static-feeling single page inexpensively via S3+CloudFront and absorbs large, unexpected traffic spikes without server management (NFR-005).

## Consequences

AWS setup is more involved than a one-click static host, but it meets the approved stack and the scalability and cost goals comfortably.
<!-- sdlc:auto:end adr -->