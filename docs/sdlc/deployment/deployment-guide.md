# Deployment Guide

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start how-it-deploys -->
Pushes to `main` run `.github/workflows/deploy.yml`, which builds the API image (if there is a backend) and deploys the SPA to AWS Amplify. Commits touching only `docs/sdlc/**` don't deploy. Deployments can also be started from the platform's Deployment tab.
<!-- sdlc:auto:end how-it-deploys -->

<!-- sdlc:auto:start environments -->
| Name | Service | Runtime | Scaling | Environment |
|---|---|---|---|---|
| SPA CDN/Static Host | AWS S3 + CloudFront | Static React 19 build | CDN edge caching, scales to large spikes automatically | dev |
| API Service | AWS (container/App Runner) | FastAPI 0.115 on Python 3.12 (Uvicorn) | Scale-to-low, auto-scale on request count | dev |
| Database | AWS RDS for PostgreSQL | PostgreSQL 16 | Single small instance; idle by design | dev |
<!-- sdlc:auto:end environments -->

<!-- sdlc:auto:start live -->
_Not deployed yet._
<!-- sdlc:auto:end live -->

<!-- sdlc:auto:start topology -->
```mermaid
graph LR
  n_SPA_CDN_Static_Host["SPA CDN/Static Host<br/>AWS S3 + CloudFront"]
  n_API_Service["API Service<br/>AWS (container/App Runner)"]
  n_Database["Database<br/>AWS RDS for PostgreSQL"]
  n_SPA_CDN_Static_Host -->|"HTTPS"| n_API_Service
  n_API_Service -->|"TCP/5432 (TLS)"| n_Database
```
<!-- sdlc:auto:end topology -->
