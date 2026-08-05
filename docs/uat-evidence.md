# UAT / Test Evidence — CloudMart on AWS Lightsail

## Test Approach
Functional validation was performed against the live public endpoint post-deployment, using realistic multi-turn customer queries to confirm the agent behaves as expected before sign-off.

## Test Cases

| # | Query | Expected Behavior | Result |
|---|---|---|---|
| 1 | "What are your operating timings?" | Agent returns accurate store hours | ✅ Pass — returned Mon–Fri, 9:00 AM–5:00 PM |
| 2 | Follow-up: "any offer today" | Agent maintains conversation context and returns an active promotion | ✅ Pass — returned active 10% off code (`CLOUDMART10OFF`) |
| 3 | Health check on public endpoint (`/`) | Returns 200, storefront renders | ✅ Pass |
| 4 | Public endpoint accessible over HTTPS | SSL termination active via Lightsail-managed certificate | ✅ Pass |

## Evidence
Screenshots captured showing:
- Container service status: `Running`
- Live chat interaction (hours query → promotion follow-up, in-context)
- Deployment timestamp and public domain confirmation

See `/assets` for supporting screenshots.

## Sign-off
All success criteria defined in [project-charter.md](project-charter.md) were met. Deployment approved for demonstration use and scheduled for decommission per [cost-and-decommission.md](cost-and-decommission.md).
