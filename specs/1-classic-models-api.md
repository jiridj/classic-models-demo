# Specification: Classic Models API Management with IBM API Connect

> *"Those aren't pillows!"* - And this isn't just another API - it's a fully managed, governed, and secured gateway to Classic Models' legacy ERP system.

## Overview

This specification outlines the process of taking the Classic Models legacy ERP API under management using IBM API Connect **via AI agents**. The entire workflow - from API definition through testing to publishing - will be executed by either the **API Agent** (embedded in API Connect) or **IBM Bob** (via MCP tools and skills).

## Agent-Driven Approach

### Two Agent Options

1. **API Agent (Embedded in API Connect)**
   - Native agent within API Connect platform
   - Direct access to API Connect APIs and resources
   - Conversational interface for API management tasks
   - Integrated with API Connect UI

2. **IBM Bob (via MCP Tools)**
   - External agent using Model Context Protocol
   - MCP tools exposed via DataPower Interact Gateway
   - Can orchestrate across multiple systems
   - Flexible skill-based automation

**Goal**: Both agents should be capable of completing the entire API management workflow autonomously or with minimal human guidance.

## Objectives

The agent will complete these tasks:

1. **Define REST API Proxy** - Import and configure API proxy in API Connect
2. **Apply Spectral Governance** - Run governance validation and fix issues
3. **Define Test Cases** - Generate and execute comprehensive test suites
4. **Publish to Infrastructure** - Deploy to Nano Gateway, Catalog, and Developer Portal

## Source API Details

### Classic Models ERP API
- **Base URL**: `https://jiridj.be/classic-models/api`
- **API Specification**: https://jiridj.be/classic-models/api/docs/
- **Repository**: https://github.com/jiridj/classic-models-api
- **Technology**: Django REST Framework (Python)
- **Authentication**: JWT tokens and API Keys

## Agent Workflow

### Agent Conversation Flow

**User**: "Take the Classic Models API under management in API Connect. The API is at https://jiridj.be/classic-models/api/docs/"

**Agent**: Executes the following workflow autonomously:

1. **Discovery & Import**
   - Fetch OpenAPI spec from source URL
   - Analyze API structure and endpoints
   - Import into API Connect

2. **Governance Validation**
   - Apply Spectral rules
   - Identify and fix governance issues
   - Generate compliance report

3. **Test Generation & Execution**
   - Generate test cases for all endpoints
   - Execute tests against source API
   - Report results and coverage

4. **Configuration & Publishing**
   - Configure security policies
   - Set up rate limiting plans
   - Deploy to Nano Gateway
   - Publish to catalog
   - Update Developer Portal

5. **Verification**
   - Validate deployment
   - Run smoke tests
   - Confirm portal accessibility

## Success Criteria

- ✅ API proxy deployed and accessible
- ✅ All Spectral governance rules passing
- ✅ 100% test coverage with all tests passing
- ✅ API published to production catalog
- ✅ Developer Portal live with documentation
- ✅ Monitoring and alerting operational

## Related Documentation

- [Classic Models Business Overview](../docs/classic-models.md)
- [Use Case 1: Lead-to-Cash Journey](../docs/use-case-1-lead-to-cash.md)
- [Use Case 2: AI-Powered Customer Support](../docs/use-case-2-ai-support.md)
- [Use Case 3: AI-Powered Lead Qualification](../docs/use-case-3-lead-qualification.md)

## References

- **API Connect Documentation**: https://www.ibm.com/docs/en/api-connect
- **Spectral Documentation**: https://stoplight.io/open-source/spectral
- **OpenAPI Specification**: https://spec.openapis.org/oas/v3.0.3
- **Classic Models API**: https://jiridj.be/classic-models/api/docs/