# Deployment Runbook — CloudMart on AWS Lightsail

## Pre-Deployment Checklist
- [ ] AWS account activated, billing/Free Tier confirmed
- [ ] OpenRouter API key generated and stored securely (not in source control)
- [ ] Latest free model confirmed via [OpenRouter model list](https://openrouter.ai/models?order=most-popular&q=free&output_modalities=text)
- [ ] Target AWS region selected

## Provisioning Steps

1. **Create container service**
   Console → Lightsail → Containers → Create container service
   - Capacity: **Micro** (1 GB RAM, 0.25 vCPU) — sized for demo-scale traffic, not defaulted to Small/Medium
   - Scale: 1 node
   - Region: selected per latency requirements

2. **Configure container**
   - Container name: `cloudmart`
   - Image: `public.ecr.aws/l4c0j8h9/acw-cloudmart-en:latest`

3. **Set environment variables**
   | Key | Value | Notes |
   |---|---|---|
   | `OPENROUTER_API_KEY` | `<redacted>` | Stored in Lightsail's native env var store only |
   | `OPENROUTER_MODEL` | `nvidia/nemotron-3-super-120b-a12b:free` | Verified against current free-model list before deploy |
   | `STUDENT_NAME` | `<redacted>` | Deployment tagging |

4. **Open ports**
   - Port `5001`, protocol `HTTP`

5. **Configure public endpoint**
   - Public endpoint container: `cloudmart`
   - Port: `5001`
   - Health check path: `/`

6. **Deploy and monitor**
   - Status progression: `Pending` → `Deploying` → `Running`
   - Confirm public domain resolves and returns expected content

## Rollback Plan
If deployment fails health checks or UAT (see [uat-evidence.md](uat-evidence.md)):
1. Roll back to previous deployment version via **Deployment versions** tab (Lightsail retains prior versions automatically)
2. If no prior version exists, disable the container service rather than deleting, to preserve configuration for troubleshooting
3. Escalate per [incident-runbook.md](incident-runbook.md) if the failure is external (e.g., OpenRouter outage)

## Post-Deployment
- Confirm functional validation (UAT) passed
- Log cost baseline — see [cost-and-decommission.md](cost-and-decommission.md)
- Schedule decommission once validation window closes
