# Use Case 1: Lead-to-Cash Journey

> *"The full trip"* - Like the complete journey in Planes, Trains and Automobiles, this scenario shows the end-to-end customer journey from initial lead capture through order fulfillment.

## Business Flow

Prospect fills out form → Lead created in CRM → Sales qualification → Deal closed → Order created → Payment → Fulfillment

## Systems Involved

- **Jotform** → **HubSpot** → **Classic Models ERP** → **Stripe** → **Classic Models ERP** 

## The Complete Journey

### Phase 1: Lead Capture
1. Prospect visits Classic Models website and fills out Jotform
2. Jotform webhook triggers on form submission
3. webMethods Integration receives form data and validates
4. Create contact and company in HubSpot CRM
5. Assign to sales rep based on territory/product line

### Phase 2: Sales Process
6. Sales rep qualifies lead in HubSpot
7. Creates deal and moves through sales stages
8. Deal reaches "Closed Won" stage
9. HubSpot webhook triggers on deal stage change

### Phase 3: Order Creation
10. webMethods Integration receives deal closed webhook
11. Extract deal details (customer, products, pricing)
12. Create customer in Classic Models ERP (if new customer)
13. Create order in Classic Models ERP via API
14. Order status: "In Process"

### Phase 4: Payment Processing
15. Send payment link to customer via Stripe
16. Customer pays via Stripe
17. Stripe webhook confirms payment
18. webMethods Integration processes payment confirmation
19. Payment recorded in Classic Models ERP
20. Order status remains "In Process" (payment received, fulfillment begins)

### Phase 5: Fulfillment
21. Warehouse picks and packs order
22. Order status updated to "Shipped"
23. Shipping notification sent to customer
24. Order delivered
25. Order status updated to "Resolved"

## Integration Technologies

- **webMethods Integration** - Workflow orchestration and data transformation
- **webMethods Connectors** - Connectivity to Jotform, HubSpot, and Stripe
- **REST APIs** - Integration with Classic Models ERP

## Key Benefits

- End-to-end automation from lead to cash
- Seamless integration across multiple systems (Jotform, HubSpot, ERP, Stripe)
- Real-time visibility into entire customer journey
- Seamless handoff between marketing, sales, and operations
- Reduced manual effort and human error

## Related Documentation

- [Classic Models Business Overview](classic-models.md)
- [Use Case 2: AI-Powered Customer Support](use-case-2-ai-support.md)
- [Use Case 3: AI-Powered Lead Qualification](use-case-3-lead-qualification.md)