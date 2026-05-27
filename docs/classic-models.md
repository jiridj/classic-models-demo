# Classic Models Demo Business

## Overview

**Classic Models** is a fictional mid-sized retailer specializing in scale model cars and other collectible vehicles. The company operates as a B2B wholesaler, selling die-cast replicas of classic and contemporary automobiles to retail stores, hobby shops, and collectors worldwide.

> *"Those aren't pillows!"* - Just like the classic 1987 comedy, Classic Models' journey involves navigating unexpected challenges with their legacy systems while trying to get home (to the cloud).

This demo scenario uses Classic Models as a representative example of a company with a **legacy home-grown ERP system** that needs to integrate with modern cloud services and AI capabilities.

## Business Model

### Core Business
- **Industry**: Wholesale distribution of collectible scale model vehicles
- **Business Type**: B2B (Business-to-Business)
- **Product Focus**: Die-cast model **planes, trains, and automobiles** (plus ships and other collectible vehicles)
- **Market**: Global distribution to retail partners and specialty stores

### Product Categories
Classic Models organizes its inventory into distinct **product lines** - covering everything you need for your journey:
- Classic Cars (Automobiles)
- Vintage Cars
- Motorcycles
- **Planes** ✈️
- Ships
- **Trains** 🚂
- Trucks and Buses

Each product line contains multiple products with detailed specifications including scale, vendor information, pricing, and stock levels.

## Organizational Structure

### Office Locations
Classic Models operates from multiple **office locations** around the world, managing local sales territories and customer relationships across major markets (San Francisco, Boston, NYC, Paris, Tokyo, Sydney, London, etc.).

### Employees
The company employs a **sales force** organized in a hierarchical structure:
- Sales Representatives manage customer accounts and process orders
- Sales Managers oversee regional teams
- Each employee is assigned to a specific office location
- Clear reporting structure from reps to managers to executives

## Customer Base

### Customer Profile
Classic Models serves a diverse **customer base** of retail partners:
- Specialty hobby shops
- Museum gift shops
- Collectible stores
- Online retailers
- Corporate gift suppliers

### Customer Management
- Each customer is assigned to a specific sales representative
- Credit limits enforced based on payment history
- Comprehensive tracking of orders and payments
- Full contact and address information maintained

## Order Management

### Order Processing
Classic Models processes **customer orders** through a comprehensive order management system with the following lifecycle:

1. **Order Creation** - Customer places order with product details
2. **Order Details** - Multiple line items with quantities and pricing
3. **Status Tracking** - In Process → Shipped → Resolved (or Cancelled/Disputed/On Hold)
4. **Fulfillment** - Shipping and delivery
5. **Payment** - Payment processing and reconciliation

### Order Status Values
- **In Process**: Order received and being prepared
- **Shipped**: Order dispatched to customer
- **Resolved**: Order completed successfully
- **Cancelled**: Order cancelled before fulfillment
- **Disputed**: Issue requiring resolution
- **On Hold**: Order temporarily suspended

## Payment Processing

Classic Models tracks **customer payments** with:
- Check numbers and payment dates
- Payment amounts linked to customer accounts
- Payment history for credit management
- Outstanding balance monitoring

## Legacy ERP System

### System Overview

The Classic Models ERP system is a **home-grown application** that serves as the "legacy system" for integration demos. It provides a realistic example of aging enterprise software that needs modernization.

**Technology Stack**:
- MySQL database (Classic Models tutorial schema)
- Django REST Framework (Python)
- RESTful API with full CRUD operations
- JWT and API Key authentication
- Docker/Docker Compose deployment

### API Resources

The system exposes comprehensive REST APIs for:
- **Authentication** - User management and token-based auth
- **Product Lines** - Product category management
- **Products** - Full product catalog with specifications
- **Offices** - Company locations and facilities
- **Employees** - Staff information and organizational hierarchy
- **Customers** - Customer accounts and relationships
- **Orders** - Order processing and status tracking
- **Payments** - Payment recording and reconciliation

### Technical Resources

**API Documentation**: https://jiridj.be/classic-models/api/docs/
- Interactive Swagger/ReDoc interface
- Complete endpoint documentation
- Try-it-now functionality with demo credentials

**GitHub Repository**: https://github.com/jiridj/classic-models-api
- Full source code and implementation
- Docker deployment configurations
- Comprehensive test suite
- Setup and usage instructions

**Demo Credentials**:
- JWT Auth - Username: `demo` / Password: `demo123`
- API Key: `GzIGzQD0pdtAi2LvYZCvJDhZZH2w87AaPZI_hFlF5BY`

## Integration Challenges

As a legacy home-grown ERP system, Classic Models faces typical **integration challenges**:

### Technical Debt
- Custom-built system with limited documentation
- Monolithic architecture
- Tightly coupled components
- Limited scalability for modern cloud workloads

### Integration Needs
- Connect to modern cloud services (CRM, analytics, AI)
- Real-time data synchronization
- Event-driven architecture for order processing
- API gateway for secure external access
- Microservices migration path

### Data & Security
- Data locked in legacy database
- Limited real-time reporting capabilities
- Legacy authentication mechanisms
- Compliance requirements (GDPR, data privacy)

## Summary

Classic Models represents a realistic **legacy ERP system** scenario that demonstrates common challenges faced by mid-sized businesses:
- Aging technology stack requiring modernization
- Need for cloud integration and API connectivity
- Opportunities for AI and automation
- Data trapped in legacy systems
- Security and compliance requirements

The fully functional API and comprehensive data model make it an ideal platform for demonstrating **integration, automation, and modernization solutions** in a realistic business context.

For detailed API specifications and implementation details, refer to:
- **API Docs**: https://jiridj.be/classic-models/api/docs/
- **GitHub**: https://github.com/jiridj/classic-models-api