# Future Use Cases for Classic Models Demo

> *"We're not done yet!"* - Just like the journey continues, these potential extensions show how Classic Models can further modernize their operations with advanced integration and analytics capabilities.

## Overview

This document outlines potential future extensions to the Classic Models demo, building upon the foundation established in the current use cases. These scenarios demonstrate additional integration patterns and advanced capabilities that could be implemented to showcase a more comprehensive technology stack.

**Current Use Cases (App Integration Focus):**
- [Use Case 1: Lead-to-Cash Journey](use-case-1-lead-to-cash.md) - End-to-end integration automation
- [Use Case 2: AI-Powered Customer Support](use-case-2-ai-support.md) - Interactive AI agent with human-in-the-loop
- [Use Case 3: AI-Powered Lead Qualification](use-case-3-lead-qualification.md) - Automated AI agent embedded in workflow

**Future Technology Extensions:**
- API Management with API Connect
- B2B Integration with webMethods B2B SaaS
- Managed File Transfer with webMethods MFT SaaS
- Guaranteed Messaging with IBM MQ
- Event Streaming with Kafka

**Future Use Case Extensions:**
- Use Case 4: Inventory Management with B2B Integration
- Use Case 5: Trend analysis with Confluent and streaming analytics

---

## Future Technology Capabilities

The current demo focuses on **application integration** using webMethods Integration, watsonx Orchestrate, and DataPower Interact Gateway. The following technologies could be added to demonstrate additional integration patterns:

### API Management with API Connect

**Purpose**: Centralized API governance, security, and lifecycle management

**Capabilities**:
- API gateway for rate limiting, throttling, and security
- Developer portal for API documentation and self-service
- API analytics and monitoring
- OAuth/JWT authentication and authorization
- API versioning and lifecycle management

**Use Cases**:
- Expose Classic Models ERP APIs to external partners
- Manage API keys and access control for third-party integrations
- Monitor API usage and performance
- Implement API monetization strategies

### B2B Integration with webMethods B2B SaaS

**Purpose**: Electronic Data Interchange (EDI) and partner integration

**Capabilities**:
- EDI translation (X12, EDIFACT, XML)
- AS2, SFTP, and other B2B protocols
- Trading partner management
- Document tracking and audit trails
- Compliance with industry standards

**Use Cases**:
- Automated purchase orders to suppliers
- Electronic invoicing with customers
- Advance Ship Notices (ASN) from suppliers
- Inventory replenishment automation

### Managed File Transfer with webMethods MFT SaaS

**Purpose**: Secure, reliable file transfer between systems

**Capabilities**:
- Encrypted file transfer (SFTP, FTPS)
- Scheduled and event-driven transfers
- File transformation and validation
- Audit trails and compliance reporting
- Large file handling

**Use Cases**:
- Daily inventory reports from ERP to data warehouse
- Product catalog updates to e-commerce platform
- Financial reconciliation files to accounting system
- Batch customer data imports/exports

### Event Streaming with Kafka

**Purpose**: Real-time event streaming and processing

**Capabilities**:
- High-throughput message streaming
- Event sourcing and replay
- Multiple consumer support
- Distributed architecture for scalability
- Event history and analytics

**Use Cases**:
- Order status change events
- Inventory level updates
- Customer activity tracking
- Real-time analytics and dashboards

### Guaranteed Messaging with IBM MQ

**Purpose**: Reliable, transactional message delivery

**Capabilities**:
- Guaranteed delivery (exactly-once processing)
- Persistent message storage
- Transactional messaging
- Dead letter queues for error handling
- High availability and disaster recovery

**Use Cases**:
- Critical order processing
- Payment transaction handling
- Financial data synchronization
- Mission-critical system integration

---

## Use Case 4: Inventory Management with B2B Integration

### Focus
Supply chain automation and B2B partner integration for inventory replenishment

### Business Context

Classic Models needs to maintain optimal inventory levels across their product lines (planes, trains, automobiles, ships, etc.). Currently, inventory management is manual - staff monitor stock levels and manually create purchase orders when items run low. This leads to:
- Stockouts that delay customer orders
- Manual effort in supplier communication
- Inconsistent ordering processes
- Delayed response to demand changes

This use case automates the entire replenishment cycle using B2B integration standards.

### High-Level Flow

```
Inventory Monitoring → Out-of-Stock Detection → Purchase Order Generation → 
B2B Transmission → Supplier Processing → Shipment Notification → 
Inventory Update → Order Fulfillment
```

### Detailed Scenario

#### Phase 1: Inventory Monitoring
1. **Real-time Inventory Tracking**
   - webMethods Integration polls Classic Models ERP API for inventory levels
   - Monitor stock quantities across all product lines
   - Track inventory movements (sales, returns, adjustments)
   - Calculate reorder points based on historical demand

2. **Out-of-Stock Event Detection**
   - Detect when inventory falls below reorder point
   - Identify critical stockouts (items with pending orders)
   - Prioritize based on demand and lead time
   - Publish inventory alert events to Kafka

#### Phase 2: Automated Replenishment
3. **Purchase Order Generation**
   - webMethods Integration consumes inventory alert from Kafka
   - Retrieve supplier information from ERP (vendor assignments per product)
   - Calculate order quantities based on:
     - Current stock level
     - Reorder point
     - Economic order quantity (EOQ)
     - Pending customer orders
   - Generate purchase order in Classic Models ERP
   - PO status: "Pending Transmission"

4. **B2B Document Preparation**
   - Transform ERP purchase order to EDI 850 (Purchase Order) format
   - Map Classic Models data to supplier's expected format
   - Include: PO number, line items, quantities, delivery address, terms
   - Validate EDI document structure

#### Phase 3: B2B Transmission
5. **Supplier Communication via webMethods B2B**
   - Send EDI 850 to supplier via AS2 protocol
   - webMethods B2B SaaS handles:
     - AS2 encryption and signing
     - Trading partner profile management
     - Reliable delivery with MDN (Message Disposition Notification)
     - Transmission tracking and audit trail
   - Update PO status to "Transmitted"

6. **Supplier Acknowledgment**
   - Receive EDI 855 (Purchase Order Acknowledgment) from supplier
   - webMethods B2B validates and routes acknowledgment
   - Update PO status to "Acknowledged"
   - Store expected delivery date from supplier

#### Phase 4: Shipment and Receipt
7. **Shipment Notification**
   - Receive EDI 856 (Advance Ship Notice) from supplier
   - Extract: shipment date, tracking number, quantities, expected arrival
   - Update PO status to "Shipped"
   - Create inbound shipment record in ERP

8. **Inventory Update**
   - Warehouse receives physical shipment
   - Scan items and confirm receipt in ERP
   - Update inventory quantities
   - Update PO status to "Received"
   - Close purchase order

9. **Order Fulfillment Enablement**
   - Publish inventory replenishment event to Kafka
   - Trigger fulfillment of any pending customer orders
   - Update order status from "On Hold" to "In Process"

### Systems Involved

- **Classic Models ERP** - Inventory management, purchase orders, supplier data
- **webMethods Integration** - Orchestration, monitoring, transformation
- **webMethods B2B SaaS** - EDI translation, AS2 communication, trading partner management
- **Kafka** - Event streaming for inventory alerts and replenishment notifications
- **Supplier Systems** - EDI-capable procurement systems

### Technology Components

#### webMethods B2B SaaS
- **EDI Standards**: X12 850 (PO), 855 (PO Ack), 856 (ASN)
- **Communication Protocol**: AS2 (Applicability Statement 2)
- **Trading Partner Management**: Supplier profiles, certificates, endpoints
- **Document Tracking**: Full audit trail of B2B transactions
- **Error Handling**: Retry logic, exception notifications

#### Integration Patterns
- **Event-Driven**: Kafka events trigger replenishment workflows
- **API Integration**: REST API calls to Classic Models ERP
- **B2B Integration**: EDI over AS2 for supplier communication
- **Polling**: Periodic inventory level checks

### Key Benefits

1. **Automated Replenishment**
   - Eliminate manual purchase order creation
   - Reduce stockout incidents
   - Optimize inventory levels

2. **Standardized B2B Communication**
   - Industry-standard EDI formats
   - Secure AS2 transmission
   - Automated acknowledgments and tracking

3. **Supply Chain Visibility**
   - Real-time inventory status
   - Shipment tracking
   - Audit trail of all B2B transactions

4. **Improved Customer Experience**
   - Reduced order delays due to stockouts
   - Faster fulfillment when inventory arrives
   - Proactive communication about availability

### Integration with Existing Use Cases

**Extends Use Case 1 (Lead-to-Cash):**
- Ensures inventory availability for orders created from closed deals
- Prevents order delays due to stockouts
- Completes the supply chain loop

**Potential Enhancement:**
- Use Case 2 AI agent could check inventory status and provide ETA for out-of-stock items
- Use Case 3 could factor inventory availability into lead qualification

---

## Use Case 5: Proactive Issue Detection with Event Processing

### Focus
Real-time analytics and predictive support using stream processing

### Business Context

Currently, Classic Models operates a **reactive support model**:
- Customers experience issues (late delivery, damaged goods, wrong items)
- Customers log support tickets in Zendesk
- Support reps investigate and resolve issues
- By the time the issue is addressed, customer satisfaction has already suffered

This use case implements a **proactive support model**:
- System continuously monitors order and shipment events
- Detects anomalies and potential issues in real-time
- Automatically creates tickets or alerts support team
- Enables proactive customer outreach before they notice problems

### High-Level Flow

```
Event Streaming → Real-Time Analysis → Pattern Detection → 
Anomaly Identification → Automated Ticket Creation → 
Proactive Customer Outreach → Issue Resolution
```

### Detailed Scenario

#### Phase 1: Event Collection
1. **Order and Shipment Events**
   - Classic Models ERP publishes events to Kafka:
     - Order created
     - Order status changes (In Process → Shipped → Delivered)
     - Payment received
     - Shipment tracking updates
     - Delivery confirmations
   - Events include: order ID, customer ID, expected delivery date, carrier, tracking number

2. **Customer Interaction Events**
   - Zendesk publishes support ticket events:
     - Ticket created
     - Ticket category (delivery issue, product quality, wrong item)
     - Customer sentiment from ticket text
   - HubSpot publishes customer engagement events:
     - Email opens/clicks
     - Website visits
     - Support page views

#### Phase 2: Real-Time Stream Processing
3. **IBM Event Processing (Flink) Analysis**
   - Consume events from multiple Kafka topics
   - Maintain stateful processing of order lifecycles
   - Calculate real-time metrics:
     - Average delivery time by carrier
     - On-time delivery percentage
     - Order-to-delivery duration
     - Ticket creation rate per customer

4. **Pattern Detection and Anomaly Identification**
   
   **Scenario A: Delayed Shipment Detection**
   - Compare actual shipment date vs. expected date
   - If shipment is >2 days late: flag as anomaly
   - Check if customer has viewed tracking page (indicates concern)
   - Severity: High if customer is actively checking status

   **Scenario B: Delivery Risk Assessment**
   - Track shipment in transit
   - Compare current location vs. expected route
   - If delivery date will be missed: flag as anomaly
   - Calculate revised ETA based on current location

   **Scenario C: Quality Issue Pattern**
   - Detect multiple tickets for same product line
   - Identify potential batch quality issues
   - Flag if >3 tickets for same product in 24 hours
   - Severity: Critical if pattern indicates systemic problem

   **Scenario D: Customer Satisfaction Risk**
   - Correlate order history with support tickets
   - Identify customers with multiple recent issues
   - Flag high-value customers at risk of churn
   - Severity: High for customers with >$10K annual spend

#### Phase 3: Automated Response
5. **Intelligent Ticket Creation**
   - For detected anomalies, automatically create Zendesk ticket:
     - Pre-populate with context (order details, issue type, severity)
     - Assign to appropriate support team based on issue category
     - Include recommended actions based on issue type
     - Set priority based on customer value and issue severity

6. **Proactive Customer Communication**
   - For high-severity issues, trigger automated outreach:
     - Email customer about delayed shipment with revised ETA
     - Offer compensation (discount code, expedited shipping on next order)
     - Provide direct contact to assigned support rep
   - For quality issues, proactively offer replacement or refund

#### Phase 4: Support Team Enablement
7. **Enhanced Support Dashboard**
   - Real-time view of detected issues
   - Prioritized queue based on severity and customer value
   - Contextual information for each issue
   - Recommended resolution actions

8. **Continuous Learning**
   - Track resolution outcomes
   - Refine anomaly detection thresholds
   - Improve pattern recognition
   - Update automated response templates

### Systems Involved

- **Kafka** - Event streaming platform for order, shipment, and customer events
- **IBM Event Processing (Flink)** - Real-time stream processing and analytics
- **Classic Models ERP** - Source of order and shipment data
- **Zendesk** - Support ticket creation and management
- **HubSpot** - Customer data and engagement tracking
- **Email Service** - Proactive customer communication

### Technology Components

#### IBM Event Processing (Apache Flink)
- **Stream Processing**: Real-time event analysis
- **Stateful Operations**: Track order lifecycles across events
- **Windowing**: Time-based aggregations (24-hour ticket counts, etc.)
- **Pattern Detection**: Complex event processing (CEP) for anomaly identification
- **Scalability**: Handle high-volume event streams

#### Integration Patterns
- **Event Streaming**: Kafka as central event bus
- **Stream Processing**: Flink for real-time analytics
- **API Integration**: REST calls to Zendesk, HubSpot
- **Event-Driven Actions**: Automated ticket creation and notifications

### Comparison: Reactive vs. Proactive Support

| Aspect | Reactive Support (Current) | Proactive Support (Future) |
|--------|---------------------------|----------------------------|
| **Trigger** | Customer logs ticket | System detects issue |
| **Timing** | After customer experiences problem | Before customer notices or early detection |
| **Customer Experience** | Frustration, then resolution | Minimal disruption, proactive communication |
| **Support Workload** | High volume of incoming tickets | Prioritized, context-rich tickets |
| **Resolution Time** | Longer (investigation required) | Faster (issue pre-diagnosed) |
| **Customer Satisfaction** | Recovered after issue | Maintained or improved |
| **Business Impact** | Reactive damage control | Proactive relationship building |

### Key Benefits

1. **Improved Customer Satisfaction**
   - Issues detected and addressed before customer impact
   - Proactive communication builds trust
   - Reduced frustration and complaints

2. **Reduced Support Volume**
   - Many issues resolved before tickets are created
   - Automated responses for common scenarios
   - Support team focuses on complex issues

3. **Faster Issue Resolution**
   - Pre-diagnosed issues with full context
   - Recommended actions for support reps
   - Prioritized queue based on severity

4. **Business Intelligence**
   - Real-time visibility into operational issues
   - Pattern detection for systemic problems
   - Data-driven process improvements

5. **Customer Retention**
   - Proactive care for high-value customers
   - Early intervention prevents churn
   - Competitive differentiation

### Integration with Existing Use Cases

**Extends Use Case 1 (Lead-to-Cash):**
- Monitors the complete order lifecycle from Use Case 1
- Ensures successful delivery and customer satisfaction
- Closes the feedback loop from order to fulfillment

**Enhances Use Case 2 (AI Support):**
- Provides AI agent with real-time issue context
- Enables proactive ticket resolution
- Enriches agent knowledge with pattern insights

**Potential Enhancement:**
- Use Case 3 lead qualification could factor in customer support history
- Identify high-maintenance prospects vs. low-touch customers

---

## Technology Stack Evolution

### Current Stack (App Integration Focus)

| Layer | Technologies |
|-------|-------------|
| **Integration & Orchestration** | webMethods Integration |
| **AI & Automation** | watsonx Orchestrate, DataPower Interact Gateway (MCP) |
| **Core Systems** | Classic Models ERP, HubSpot, Stripe, Zendesk, Jotform |

### Future Stack (Comprehensive Integration Platform)

| Layer | Technologies |
|-------|-------------|
| **Integration & Orchestration** | webMethods Integration, API Connect |
| **B2B Integration** | webMethods B2B SaaS, webMethods MFT SaaS |
| **Messaging** | IBM MQ (guaranteed delivery), Kafka (event streaming) |
| **Stream Processing** | IBM Event Processing (Flink) |
| **AI & Automation** | watsonx Orchestrate, DataPower Interact Gateway (MCP) |
| **Core Systems** | Classic Models ERP, HubSpot, Stripe, Zendesk, Jotform |

### New Components for Future Use Cases

1. **API Connect**
   - API gateway and management
   - Developer portal
   - API analytics and monitoring

2. **webMethods B2B SaaS**
   - EDI translation and validation
   - AS2 communication protocol
   - Trading partner management
   - B2B transaction monitoring

3. **webMethods MFT SaaS**
   - Secure file transfer
   - Scheduled and event-driven transfers
   - File transformation and validation

4. **Kafka**
   - Event streaming platform
   - High-throughput messaging
   - Event sourcing and replay

5. **IBM MQ**
   - Guaranteed message delivery
   - Transactional messaging
   - Persistent message storage

6. **IBM Event Processing (Apache Flink)**
   - Real-time stream processing
   - Complex event processing (CEP)
   - Stateful computations
   - Pattern detection and analytics

---

## Implementation Considerations

### Use Case 4: Inventory Management

**Prerequisites:**
- Classic Models ERP API must expose inventory endpoints
- Supplier systems must support EDI (X12 or EDIFACT)
- Trading partner agreements and AS2 certificates in place

**Development Effort:**
- webMethods B2B trading partner setup: 1-2 weeks
- EDI mapping and transformation: 2-3 weeks
- Integration workflows: 2-3 weeks
- Testing with supplier systems: 2-4 weeks

**Operational Requirements:**
- Trading partner onboarding process
- EDI document monitoring and exception handling
- Supplier relationship management

### Use Case 5: Proactive Issue Detection

**Prerequisites:**
- Kafka infrastructure with sufficient capacity
- IBM Event Processing (Flink) cluster deployment
- Enhanced event publishing from Classic Models ERP
- Historical data for pattern baseline

**Development Effort:**
- Event schema design: 1 week
- Flink job development: 3-4 weeks
- Anomaly detection tuning: 2-3 weeks
- Integration with Zendesk/HubSpot: 1-2 weeks
- Dashboard development: 2 weeks

**Operational Requirements:**
- Stream processing monitoring and alerting
- Anomaly detection threshold tuning
- Support team training on proactive workflows

---

## Summary

These future use cases demonstrate how Classic Models can continue their modernization journey:

- **Use Case 4** extends the supply chain with automated B2B integration, ensuring inventory availability and streamlined supplier communication
- **Use Case 5** transforms customer support from reactive to proactive, using real-time analytics to detect and resolve issues before they impact customers

Both scenarios build upon the foundation of the existing use cases, showcasing a comprehensive integration and AI platform that spans the entire business operation from lead capture through fulfillment and support.

> *"We're going the right way now!"* - With these extensions, Classic Models has a complete, modern integration architecture.