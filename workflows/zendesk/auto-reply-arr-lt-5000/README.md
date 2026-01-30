# Zendesk Auto Reply — ARR < 5000

## Purpose
This automation handles first-level responses for new Zendesk tickets by enriching requester data, evaluating company ARR, and routing tickets appropriately.

The goal is to:
- Reduce manual workload for low-value tickets
- Ensure high-value accounts receive human attention
- Maintain consistent, policy-aligned responses

---

## High-Level Workflow Logic

1. **Trigger**
   - Fires when a new Zendesk ticket is created

2. **Sender Validation**
   - Blocks internal or restricted email domains
   - Stops execution for non-customer tickets

3. **Company Enrichment**
   - Extracts requester email domain
   - Fetches company details from HubSpot
   - Retrieves ARR and company metadata

4. **ARR Validation**
   - Stops workflow if ARR is missing or invalid
   - Prevents incorrect automated responses

5. **Routing Decision**
   - **ARR < 5000**
     - Generate AI-based response
     - Post public reply to Zendesk
   - **ARR ≥ 5000**
     - Send internal alert for manual handling

---

## Integrations Used

- Zendesk (Trigger, Ticket Update)
- HubSpot (Company lookup)
- OpenAI (AI-generated response)
- Internal Messaging Channel (alerts for high ARR tickets)

---

## Guardrails & Fail-Safes

- Internal emails are explicitly blocked
- Workflow stops if:
  - Company is not found
  - ARR is null or malformed
- AI response is validated before posting
- No credentials are stored in the workflow JSON

---

## Operational Notes

- Designed for production use with strict stopping conditions
- Requires credentials to be configured in n8n (not in JSON)
- Alert channel must be actively monitored for high ARR tickets

---

## Files in This Directory

- `workflow.json` — n8n workflow export (credentials removed)
- `docs/` — detailed node-level documentation
- `CHANGELOG.md` — version and change history

---

## Ownership

Maintained by: Automation Analyst  
Domain: Customer Support Automation  
Status: Active
