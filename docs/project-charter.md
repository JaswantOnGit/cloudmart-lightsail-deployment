# Project Charter — CloudMart on AWS Lightsail

## Business Scenario
Deploy CloudMart, a containerized GenAI shopping assistant, for a training/demo environment using a lightweight, low-cost container service. The end goal is a publicly accessible demo running on port 5001, configured entirely through environment variables at deployment time.

## Objectives
- Deploy the CloudMart container image to AWS Lightsail Container Service
- Expose a public, SSL-terminated endpoint on port 5001
- Configure application secrets and model settings via environment variables, not hardcoded values
- Validate functional behavior against real conversational queries before sign-off
- Decommission all resources post-validation to prevent cost drift

## Success Criteria
| Criterion | Target |
|---|---|
| Endpoint availability | Public URL returns 200 on health check path (`/`) |
| Functional accuracy | Agent correctly answers multi-turn queries (hours, promotions) |
| Secrets handling | Zero credentials committed to source or hardcoded in image |
| Cost exposure | Deployment stays within AWS Free Tier; resources torn down after UAT |
| Response latency | Sub-2s response time on standard queries |

## Scope
**In scope:** Container service provisioning, environment configuration, public endpoint setup, functional validation, resource cleanup.
**Out of scope:** Application code changes, custom domain/DNS setup, CI/CD pipeline, autoscaling configuration (deferred — see RAID log).

## Stakeholders
| Stakeholder | Role |
|---|---|
| AI Implementation PM | Delivery owner, governance, go/no-go decision |
| Dev / Container Owner | Image build, application logic |
| Security | Secrets and access review |

## Timeline
Single-session deployment (lab-scale). In a production engagement, this would map to a 1-2 day sprint: provisioning (Day 1 AM), configuration + UAT (Day 1 PM), sign-off + decommission scheduling (Day 2).
