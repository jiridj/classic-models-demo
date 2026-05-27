# Use Case 1: Lead-to-Cash Journey

> *"The full trip"* - Like the complete journey in Planes, Trains and Automobiles, this scenario shows the end-to-end customer journey from initial lead capture through order fulfillment.

## Business Flow

Prospect fills out form → Lead created in CRM → Sales qualification → Deal closed → Order created → Payment → Fulfillment

## Systems Involved

- **Jotform** → **HubSpot** → **Classic Models ERP** → **Stripe** → **Classic Models ERP** → **Zendesk** (if needed)

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
12. Publish order creation message to IBM MQ queue (guaranteed delivery)
13. Order processing service consumes message from MQ
14. Create customer in Classic Models ERP (if new customer)
15. Create order in Classic Models ERP via API
16. Order status: "In Process"
17. Acknowledge MQ message (remove from queue)

### Phase 4: Payment Processing
18. Send payment link to customer via Stripe
19. Customer pays via Stripe
20. Stripe webhook confirms payment
21. Publish payment message to IBM MQ queue (guaranteed delivery)
22. Payment processing service consumes message from MQ
23. Payment recorded in Classic Models ERP
24. Order status remains "In Process" (payment received, fulfillment begins)
25. Acknowledge MQ message (remove from queue)

### Phase 5: Fulfillment
26. Warehouse picks and packs order
27. Order status updated to "Shipped"
28. Shipping notification sent to customer
29. Order delivered
30. Order status updated to "Resolved"
31. Status changes published as events via Kafka

### Phase 6: Support (if needed)
32. If issues arise at any stage, support ticket created in Zendesk
33. Support agent has access to complete order history from ERP

## Integration Technologies

- **webMethods Integration** for orchestration
- **API Connect** for ERP API management
- **IBM MQ** for guaranteed delivery of critical transactions (order creation, payment processing)
- **Kafka** for order status events and real-time notifications

### Why IBM MQ for Order & Payment Processing

- **Guaranteed Delivery**: Orders and payments cannot be lost, even during system outages
- **Transactional**: Exactly-once processing ensures no duplicate orders
- **Persistent**: Messages stored until successfully processed
- **Retry Logic**: Automatic retry with dead letter queue for failed messages

### Why Kafka for Status Events

- **High Throughput**: Handle many status change events
- **Multiple Consumers**: Many systems need order status updates
- **Event History**: Replay capability for analytics and debugging

## Key Benefits

- End-to-end automation from lead to cash
- Zero message loss for critical transactions
- Real-time visibility into entire customer journey
- Seamless handoff between marketing, sales, operations, and support

## Related Documentation

- [Classic Models Business Overview](classic-models.md)
- [Use Case 2: AI-Powered Customer Support](use-case-2-ai-support.md)
- [Use Case 3: AI-Powered Lead Qualification](use-case-3-lead-qualification.md)