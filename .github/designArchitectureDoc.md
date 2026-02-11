---
name: documentSystemArchitecture
description: Create comprehensive system architecture documentation with diagrams, components, assumptions, dependencies, and project considerations.
argument-hint: Project roadmap, requirements, user personas, technology stack, and timeline constraints
---

# Comprehensive System Architecture & Project Documentation

You are helping create professional documentation for a software project covering architecture, assumptions, dependencies, and project-level considerations. Follow this structured approach:

## Phase 1: Identify Architecture Components
- Review the provided project roadmap and requirements
- Identify all major system layers (frontend/client, backend/compute, infrastructure, external services)
- List user personas/actors who interact with the system
- Determine what components might be missing from the initial scope
- Map data flows and integration points between components

## Phase 2: Create Visual Architecture Diagram
- Design a system architecture diagram showing all moving parts
- Include user personas to show who uses the system and how they interact
- Group components by logical layers (client, cloud, services, etc.)
- Show primary data flow connections between components
- Use meaningful color coding to distinguish component categories
- Keep the diagram at a high level without overwhelming internal detail

## Phase 3: Create Component Documentation
- Document each major component in paragraph form
- **Provide a Single, Confident Recommendation**: Do not offer alternatives (e.g., "Use X or Y"). Select the best-fit technology based on requirements and justify the choice confidently.
- For each component, explain what it is and why it's needed
- Cover all layers: infrastructure, compute, storage, AI/analytics, security, and UI
- Keep explanations accessible to both technical and non-technical stakeholders
- Use consistent structure across all component descriptions

## Phase 4: Identify Technical Assumptions
- Clarify assumptions about third-party tools, libraries, and frameworks (versions, compatibility, licensing)
- Document assumptions about infrastructure (cloud services, availability, scalability)
- Define assumptions about data consistency, offline/online modes, and network reliability
- Identify assumptions about integration points and API availability
- List assumptions about development environment and tooling

## Phase 5: Map Dependencies & Sequencing
- Identify critical path dependencies that affect development sequencing
- Document service dependencies (e.g., which components must be built before others can be integrated)
- List external dependencies (APIs, third-party services, hardware, data sources)
- Map temporal dependencies between development phases or activities
- Identify knowledge/expertise dependencies on domain experts or SMEs

## Phase 6: Define Project-Level Considerations (For Client Stakeholder Communication)
- **Scope & Deliverables**: What is included vs. out of scope; what defines "complete"
- **Resource Responsibilities**: What the client must provide (environments, access, personnel, procurements)
- **Collaboration & Decision Making**: Decision-making timelines, approval processes, escalation paths
- **Testing & Quality**: Who performs what type of testing; acceptance criteria definitions
- **Data & Infrastructure**: Data responsibilities, environment setup, cost ownership
- **Regulatory & Legal**: Compliance responsibilities, data ownership, licensing obligations
- **Post-Deployment**: Support duration, training, maintenance scope

## Phase 7: Refine & Organize
- Organize all assumptions by category (technical, operational, business, regulatory)
- Organize all dependencies by criticality and timeline impact
- Ensure no conflicting assumptions exist
- Verify that project-level considerations cover all client interaction touchpoints
- Prepare for presentation to both technical and non-technical stakeholders

## Deliverables
1. System architecture diagram with clear component grouping and data flows
2. Comprehensive component documentation (paragraph-style, all layers)
3. Organized assumptions list (technical, operational, business, regulatory)
4. Dependencies map showing critical path and sequencing constraints
5. Project-level considerations document for client communication
6. Professional presentation-ready format suitable for stakeholder review and sign-off
