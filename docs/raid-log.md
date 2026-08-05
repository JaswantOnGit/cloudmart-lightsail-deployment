# RAID Log — CloudMart on AWS Lightsail

## Risks

| ID | Risk | Likelihood | Impact | Mitigation | Owner |
|---|---|---|---|---|---|
| R1 | Public model rate-limiting (OpenRouter HTTP 429) under load | Medium | Medium — degraded UX, agent unresponsive | Fallback model configured; documented BYO API key path; see [incident-runbook.md](incident-runbook.md) | PM / Dev |
| R2 | New AWS account IAM/quota restrictions blocking Lightsail resource creation | Low | High — blocks deployment entirely | Verified account activation and billing setup before start; confirmed `lightsail:*` IAM permissions | PM |
| R3 | Container service left running post-validation, incurring drift charges past Free Tier | Medium | Low — $10/mo per node after 90 days | Decommission scheduled and logged immediately after UAT sign-off | PM |
| R4 | API key exposure via hardcoding or accidental commit | Low | High — credential compromise | Enforced environment-variable-only secrets handling; no `.env` committed to any repo | PM / Security |

## Assumptions

- Container image and application code are pre-built and provided (not developed as part of this engagement)
- Single-region deployment (ap-south-1 for lab); production would require region selection aligned to end-user latency requirements
- Free Tier credits available and sufficient to cover deployment + validation window

## Issues

| ID | Issue | Resolution |
|---|---|---|
| I1 | Lightsail account hit "quota for container services" limit on first attempt | Acknowledged quota notice; confirmed service quota via AWS Service Quotas console before retry |

## Dependencies

- AWS account with billing activated and Free Tier credits available
- OpenRouter API key (external dependency, third-party service availability)
- Public container image hosted on Amazon ECR Public Gallery
