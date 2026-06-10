# Classic Models Demo Use Cases

> *"We're going the wrong way!"* - Not anymore! These integration scenarios show how Classic Models can modernize their journey to the cloud.

## Overview

This document provides an index to the Classic Models demo use cases, showcasing integration and AI capabilities across the technology stack.

## System Architecture

Classic Models uses the following systems for their business operations:

### Core Systems

1. **Classic Models ERP** (Legacy Home-Grown System)
   - MySQL database with Django REST Framework
   - Manages: Products, Orders, Customers, Employees, Offices, Payments
   - API: https://jiridj.be/classic-models/api/docs/
   - Repository: https://github.com/jiridj/classic-models-api

2. **Jotform** (Lead Capture)
   - Web forms for lead generation
   - Captures: Contact info, product interests, company details
   - Integration: Webhooks, REST API

3. **HubSpot** (CRM)
   - Customer relationship management
   - Manages: Contacts, Companies, Deals, Sales pipeline
   - Integration: REST API, Webhooks

4. **Stripe** (Payment Processing)
   - Online payment processing
   - Handles: Credit cards, subscriptions, invoices
   - Integration: REST API, Webhooks

5. **Zendesk** (Service Desk)
   - Customer support ticketing
   - Manages: Support tickets, customer inquiries, knowledge base
   - Integration: REST API, Webhooks

## Technology Stack

- **webMethods Integration** - Workflow orchestration and data transformation
- **DataPower Interact Gateway** - AI Gateway with MCP tools
- **watsonx Orchestrate** - AI agent platform

## Use Cases

### [Use Case 1: Lead-to-Cash Journey](use-case-1-lead-to-cash.md)

**Focus**: End-to-end integration automation

Complete flow from lead capture through order fulfillment, demonstrating:
- webMethods Integration orchestration
- Multi-system integration (Jotform → HubSpot → ERP → Stripe)
- Reliable order and payment processing

**Key Scenario**: Prospect fills out form → Sales qualification → Deal closed → Order created → Payment processed → Order fulfilled

---

### [Use Case 2: AI-Powered Customer Support](use-case-2-ai-support.md)

**Focus**: Interactive AI agent with human-in-the-loop

Customer success rep uses watsonx Orchestrate agent to resolve support issues, demonstrating:
- Natural language interface for system access
- MCP tools on DataPower Interact Gateway
- Multi-system data retrieval and updates
- Conversational AI for support workflows

**Key Scenario**: Missing order investigation - Agent helps rep discover order was delivered to wrong address, updates systems, and resolves issue before customer's weekend sale

---

### [Use Case 3: AI-Powered Lead Qualification](use-case-3-lead-qualification.md)

**Focus**: Automated AI agent embedded in workflow

watsonx Orchestrate agent automatically qualifies and enriches leads, demonstrating:
- AI agent embedded in integration workflow
- Automated decision-making without human intervention
- Lead enrichment with external data
- Intelligent routing based on qualification

**Key Scenario**: Prospect submits form → Agent qualifies based on revenue/business type → Enriches with company data → Creates in HubSpot with lead score → Assigns to appropriate sales rep

---

## Comparison: Use Case 2 vs Use Case 3

| Aspect | Use Case 2: AI Support | Use Case 3: Lead Qualification |
|--------|------------------------|--------------------------------|
| **Interaction Model** | Human-in-the-loop | Fully automated |
| **User** | Customer success rep | No human user (embedded in workflow) |
| **Agent Role** | Assistant/co-pilot | Autonomous decision-maker |
| **Trigger** | Rep asks questions | Form submission webhook |
| **Decision Making** | Rep makes final decisions | Agent makes decisions autonomously |
| **Use of MCP Tools** | Interactive data retrieval | Automated data access |

## Future Extensions

Looking ahead, additional use cases could further demonstrate the platform's capabilities:

- **[Future Use Cases](future-use-cases.md)** - Potential extensions including:
  - API Management with API Connect
  - B2B Integration with webMethods B2B SaaS
  - Managed File Transfer with webMethods MFT SaaS
  - Event Streaming with Kafka
  - Guaranteed Messaging with IBM MQ
  - Use Case 4: Inventory Management with B2B Integration
  - Use Case 5: Proactive Issue Detection with Event Processing

## Related Documentation

- [Classic Models Business Overview](classic-models.md) - Business context and ERP system details
- [Future Use Cases](future-use-cases.md) - Potential extensions and advanced scenarios

## Next Steps

These scenarios form the foundation for demo implementations. Each use case document provides:
- Detailed step-by-step flows
- System integration points
- Technology components
- MCP tool specifications
- Key benefits and outcomes