# Use Case 3: AI-Powered Lead Qualification in Workflow

> *"Automated qualification"* - Like having an intelligent gatekeeper who knows exactly who should get on the plane, train, or automobile to reach their destination.

## Business Flow

Jotform submission → AI agent qualifies and enriches lead → Qualified leads to HubSpot, disqualified leads get follow-up email

## The Scenario

A prospect fills out a Jotform on Classic Models' website expressing interest in becoming a retail partner. The watsonx Orchestrate agent embedded in the webMethods workflow automatically qualifies the lead based on business criteria and enriches it with additional data before creating it in HubSpot.

## Systems Involved

**Jotform** → **webMethods Integration** → **watsonx Orchestrate Agent** (via DataPower Interact Gateway) → **HubSpot**

## The Journey

### Phase 1: Form Submission

1. Prospect fills out Jotform with:
   - Company name: "Vintage Wheels Collectibles"
   - Contact: John Smith, john@vintagewheels.com
   - Business type: "Retail Store"
   - Annual revenue: "$500K"
   - Product interest: "Classic Cars, Vintage Cars"
   - Message: "Looking to expand our collectibles section"
2. Jotform webhook triggers on submission
3. webMethods Integration receives form data

### Phase 2: AI-Powered Qualification

4. webMethods workflow invokes watsonx Orchestrate agent via DataPower Interact Gateway
5. Agent analyzes submission against qualification criteria:
   - **Business Type**: Must be retail/hobby shop (✓ Retail Store)
   - **Revenue**: Minimum $250K annual (✓ $500K)
   - **Product Fit**: Interest in our product lines (✓ Classic & Vintage Cars)
   - **Geographic Coverage**: Check if territory available
   - **Existing Customer**: Check if already in ERP
6. watsonx Orchestrate agent uses MCP tools via DataPower Interact Gateway:
   - **check_erp_customer** - Verify not already a customer
   - **check_territory_availability** - Confirm territory open
   - **enrich_company_data** - Get additional business info (LinkedIn, company website, etc.)

### Phase 3A: Qualified Lead Path

7. watsonx Orchestrate agent determines: **QUALIFIED** ✓
8. Agent enriches lead data:
   - Company website: vintagewheels.com
   - LinkedIn profile found
   - Estimated employees: 5-10
   - Territory: Northeast US (available)
9. webMethods workflow creates contact and company in HubSpot:
   - Contact: John Smith with enriched details
   - Company: Vintage Wheels Collectibles with business intelligence
   - Lead Score: 85/100 (high priority)
   - Assigned to: Sales rep for Northeast territory
10. Workflow sends welcome email to prospect:
    - "Thanks for your interest! Our sales rep will contact you within 24 hours."
11. Workflow creates task in HubSpot for sales rep:
    - "New qualified lead: Vintage Wheels Collectibles - $500K revenue, interested in Classic Cars"

### Phase 3B: Disqualified Lead Path (Alternative Scenario)

7. watsonx Orchestrate agent determines: **DISQUALIFIED** ✗
   - Reason: Annual revenue below $250K threshold
8. Workflow sends personalized email to prospect:
   - "Thank you for your interest in Classic Models!"
   - "To better serve you, we need some additional information:"
   - "Could you provide your current annual revenue and number of retail locations?"
   - "This helps us match you with the right partnership program."
9. Email includes link to updated Jotform with additional questions
10. Lead stored in HubSpot as "Nurture" status for future follow-up
11. Workflow creates task for marketing team:
    - "Follow up with disqualified lead in 30 days"

### Phase 4: Continuous Learning

12. watsonx Orchestrate agent logs qualification decision and reasoning
13. Sales rep outcome (deal won/lost) fed back to agent
14. Agent improves qualification criteria over time based on outcomes

## Integration Technologies

- **webMethods Integration** for workflow orchestration
- **watsonx Orchestrate** for AI agent (embedded in workflow)
- **DataPower Interact Gateway** for AI agent invocation with MCP tools
- **API Connect** for HubSpot and ERP API access
- **Kafka** for lead qualification events

## MCP Tools Used by Agent

- `check_erp_customer` - Verify if already a customer
- `check_territory_availability` - Confirm sales territory open
- `enrich_company_data` - Get business intelligence from external sources
- `calculate_lead_score` - Score lead based on multiple factors
- `get_hubspot_similar_companies` - Find similar existing customers

## Qualification Criteria

- Business type: Retail store, hobby shop, museum gift shop
- Minimum annual revenue: $250K
- Product interest alignment with our catalog
- Territory availability (not oversaturated)
- Not an existing customer
- Valid business contact information

## Key Benefits

- **Automated Qualification**: AI agent qualifies leads 24/7 without human intervention
- **Enriched Data**: Agent adds business intelligence before creating in HubSpot
- **Consistent Criteria**: Every lead evaluated against same standards
- **Faster Response**: Qualified leads routed immediately to sales
- **Nurture Disqualified**: Disqualified leads get personalized follow-up, not ignored
- **Continuous Improvement**: Agent learns from sales outcomes
- **Sales Efficiency**: Reps only work qualified, enriched leads

## Related Documentation

- [Classic Models Business Overview](classic-models.md)
- [Use Case 1: Lead-to-Cash Journey](use-case-1-lead-to-cash.md)
- [Use Case 2: AI-Powered Customer Support](use-case-2-ai-support.md)