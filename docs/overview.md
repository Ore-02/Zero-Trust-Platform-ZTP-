# ZTP Overview

## Purpose
Build a Zero Trust AWS reference platform demonstrating:
- Dev vs Prod environment isolation (two-account model)
- Identity + network defense in depth
- Guardrails and auditability (CloudTrail + SCP)
- Public entry + private compute + private database pattern

## Primary Implementation Model (Option A)
- AWS Organization with two accounts:
  - ztp-dev
  - ztp-prod

## Workload (DB-lite)
- ALB (public) -> EC2 Docker app (private)
- App exposes:
  - /health/live (liveness)
  - /health/ready (readiness checks DB connectivity: SELECT 1)
- RDS Postgres (private DB subnet, no public access)

## Definition of Done
- Only ALB is publicly reachable
- App EC2 has no public IP; access via SSM
- RDS has no public endpoint; accepts traffic only from App SG
- DevRole cannot access Prod (tested and documented)
- SCP blocks disabling CloudTrail (tested and documented)
- Evidence pack exists (screenshots + CLI outputs + CloudTrail samples)
