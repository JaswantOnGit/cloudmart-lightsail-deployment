# Incident Runbook — CloudMart on AWS Lightsail

Documented **before** go-live, so on-call response doesn't start from zero.

---

## Known Issue 1 — HTTP 429: Too Many Requests

**Symptom:** OpenRouter API returns `429 Client Error: Too Many Requests` at `https://openrouter.ai/api/v1/chat/completions`

**Root Cause:** The configured public/free model is rate-limited upstream by OpenRouter.

**Ranked Mitigations:**
1. Switch to an alternate free model with available capacity (verify current list at OpenRouter)
2. Add credit to the OpenRouter account (e.g., $10) to raise rate limits
3. Use a dedicated provider API key in `OPENROUTER_API_KEY` instead of the shared free tier

**Monitoring note:** Track usage patterns; rotate keys if abuse is suspected.

---

## Known Issue 2 — HTTP 403 / Lightsail Access Restrictions

**Symptom:** Permission or quota errors when creating Lightsail resources, typically on new AWS accounts or restricted IAM users.

**Root Cause:** Account not fully activated, missing billing setup, or IAM user lacks Lightsail permissions.

**Resolution:**
1. Confirm AWS account activation and billing configuration are complete
2. Verify IAM user has `lightsail:*` or the relevant granular permissions
3. Add/confirm a payment method if service restrictions persist

---

## Severity & Escalation

| Severity | Definition | Response |
|---|---|---|
| SEV-1 | Public endpoint fully down | Roll back to last known-good deployment version immediately |
| SEV-2 | Agent responding but degraded (rate-limited) | Apply ranked mitigation above; no rollback required |
| SEV-3 | Cost/quota warning, no user impact | Log and address at next maintenance window |
