# RACI Matrix — CloudMart on AWS Lightsail

**Legend:** R = Responsible · A = Accountable · C = Consulted · I = Informed

| Activity | AI Implementation PM | Dev / Container Owner | Security |
|---|:---:|:---:|:---:|
| Project charter & success criteria | A/R | C | I |
| Container image selection | I | A/R | I |
| Container service provisioning (capacity, region) | A/R | C | I |
| Environment variable configuration | A | C | R |
| IAM / access permissions review | A | I | R |
| Public endpoint & port mapping | A/R | C | I |
| UAT / functional validation | A/R | C | I |
| Go/no-go decision | A | C | C |
| Incident response (rate-limit, downtime) | A | R | I |
| Cost monitoring | A/R | I | I |
| Resource decommission | A/R | I | I |

## Notes

In this self-directed engagement, the AI Implementation PM role executed the Dev and Security functions directly for demonstration purposes. The matrix above reflects how responsibility would be distributed across a real delivery team, and is the structure this deployment was governed against.
