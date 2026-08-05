# Cost & Decommission Log — CloudMart on AWS Lightsail

## Cost Model
| Item | Detail |
|---|---|
| Node size | Micro (1 GB RAM, 0.25 vCPU) |
| List price | $10 USD/month per node |
| Free Tier | Free for first 90 days |
| Data transfer | 500 GB/month included; overage from $0.09 USD/GB |
| Sizing rationale | Micro selected deliberately over Small/Medium/Large — demo-scale traffic does not justify 1.5x–8x the base spend |

## Cost Governance Decisions
- Verified AWS Free Tier credit balance before starting ($100 immediate + $100 activity-based, per account)
- Selected minimum viable capacity tier rather than defaulting to a larger node
- Did **not** enable autoscaling — out of scope for a demo-scale, single-session workload
- Set an internal reminder to decommission immediately following UAT sign-off, rather than leaving the service running indefinitely

## Decommission Record

| Step | Status |
|---|---|
| UAT sign-off received | ✅ Complete |
| Container service disabled/deleted | ✅ Complete — confirmed via "Delete this container service?" dialog |
| Stored container images, deployments, and containers removed | ✅ Complete |
| Final cost check (no lingering charges) | ✅ Confirmed $0 net spend, within Free Tier |

**Outcome:** Zero ongoing cost exposure post-engagement. This closes the loop on R3 in the [RAID log](raid-log.md).
