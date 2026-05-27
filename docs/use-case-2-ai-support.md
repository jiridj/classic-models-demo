# Use Case 2: AI-Powered Customer Support with MCP Tools

> *"Your AI co-pilot for support"* - Like having a knowledgeable travel companion, the AI agent helps customer success reps navigate through multiple systems to resolve issues quickly.

## Business Flow

Customer inquires about missing order → Rep uses AI agent to investigate and resolve

## The Scenario

A customer (Mini GT Models, a hobby shop in Chicago) contacts support saying they haven't received their order of 1:18 scale classic car models that was supposed to arrive last week. They're concerned because they have a big sale this weekend and need the inventory.

## Architecture Overview

- **Zendesk**: Ticket management and documentation (used as headless system)
- **watsonx Orchestrate**: AI agent interface for customer success rep
- **DataPower Interact Gateway**: AI Gateway with MCP tools for system access
- **Backend Systems**: HubSpot CRM + Classic Models ERP

## Systems Involved

**Zendesk** ↔ **watsonx Orchestrate** ↔ **DataPower Interact Gateway** ↔ **HubSpot** + **Classic Models ERP**

## The Journey

### Phase 1: Customer Inquiry

1. Customer emails: "Where is my order? It was supposed to arrive last week!"
2. Support ticket #12345 created in Zendesk
   - Customer: Mini GT Models (Chicago)
   - Issue: Missing order
   - Priority: High (customer has upcoming sale)
3. Customer success rep Sarah opens watsonx Orchestrate agent interface

### Phase 2: Agent-Driven Context Gathering

4. Sarah asks agent: "Show me details for ticket #12345"
5. Agent uses MCP tools via DataPower Interact Gateway:
   - **get_zendesk_ticket** - Retrieves ticket: "Missing order, customer needs for weekend sale"
   - **get_hubspot_contact** - Fetches: Mini GT Models, Chicago, contact: Mike Chen
   - **get_hubspot_company** - Gets: Long-time customer, $50K annual revenue
   - **get_erp_customer** - Customer #456, credit limit $10K, good payment history
6. Agent responds: "Mini GT Models is a valued customer from Chicago. Mike Chen reported a missing order needed for this weekend's sale."

### Phase 3: Intelligent Analysis

7. Sarah asks: "What's the status of their recent orders?"
8. Agent uses **get_erp_orders** and responds:
   - "Order #ORD-2026-1234 placed 2 weeks ago"
   - "Status: Shipped (5 days ago)"
   - "Items: 24x 1:18 scale classic car models"
   - "Tracking: Delivered yesterday to warehouse address"
9. Sarah asks: "Wait, it shows delivered? Check the shipping address"
10. Agent uses **get_erp_order_details** and responds:
    - "Order shipped to: 123 Warehouse Rd, Chicago"
    - "Customer's registered address: 456 Main St, Chicago (retail store)"
    - "Issue identified: Order delivered to old warehouse address, not current retail location"

### Phase 4: Taking Action

11. Sarah asks: "Can you check if they have multiple addresses in HubSpot?"
12. Agent uses **get_hubspot_company** and responds:
    - "Yes, two addresses on file:"
    - "Warehouse: 123 Warehouse Rd (old)"
    - "Retail Store: 456 Main St (current)"
13. Sarah says: "Update the ERP with the correct address and create a task for the sales rep to verify addresses with all Chicago customers"
14. Agent executes:
    - **update_erp_customer** - Updates primary address to retail store
    - **create_hubspot_task** - "Verify shipping addresses for Chicago customers" assigned to sales rep
    - **update_zendesk_ticket** - Logs: "Root cause: Wrong address. Corrected in ERP. Arranging redelivery."
15. Agent confirms: "Actions completed. Customer address updated."

### Phase 5: Resolution & Documentation

16. Sarah contacts shipping to arrange redelivery to correct address
17. Sarah asks agent: "Draft a response to the customer"
18. Agent generates:
    - "Hi Mike, I found your order - it was delivered to your old warehouse address. I've updated your account with your retail store address and arranged for redelivery today. You'll have your inventory for the weekend sale. Sorry for the confusion!"
19. Sarah approves and sends
20. Sarah asks: "Summarize this case"
21. Agent updates Zendesk ticket with complete resolution:
    - Root cause: Outdated shipping address
    - Actions taken: Address corrected, redelivery arranged, sales task created
    - Customer impact: Resolved before weekend sale
22. Ticket closed with complete documentation

## MCP Tools on DataPower Interact Gateway

### Read Operations

- `get_zendesk_ticket` - Retrieve ticket details
- `get_zendesk_ticket_history` - Get ticket conversation history
- `get_hubspot_contact` - Fetch contact information
- `get_hubspot_company` - Get company details
- `get_hubspot_deals` - Retrieve deal history
- `get_erp_customer` - Get customer account info
- `get_erp_orders` - Retrieve order history
- `get_erp_order_details` - Get specific order details
- `get_erp_payments` - Fetch payment history

### Write Operations

- `update_zendesk_ticket` - Update ticket status/notes
- `create_hubspot_task` - Create follow-up tasks
- `update_hubspot_deal` - Update deal information
- `update_erp_order` - Change order status
- `create_erp_payment` - Record payment

## Integration Technologies

- **watsonx Orchestrate** - AI agent interface for customer success rep
- **DataPower Interact Gateway** - AI Gateway with MCP tool server
- **API Connect** - API management for backend systems
- **webMethods Integration** - Data transformation and enrichment

## Key Benefits

- **Natural Language Interface**: Rep interacts conversationally with agent
- **Unified Access**: Single interface to all systems via MCP tools
- **Governed AI**: DataPower Interact Gateway provides security and governance
- **Action-Oriented**: Agent can read AND update data across systems
- **Complete Documentation**: All interactions logged in Zendesk
- **Faster Resolution**: No system switching, agent handles data retrieval

## Related Documentation

- [Classic Models Business Overview](classic-models.md)
- [Use Case 1: Lead-to-Cash Journey](use-case-1-lead-to-cash.md)
- [Use Case 3: AI-Powered Lead Qualification](use-case-3-lead-qualification.md)