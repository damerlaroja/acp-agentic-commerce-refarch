# ACP-Inspired Commerce Reference Architecture

A strategic reference implementation demonstrating controlled delegation across trust boundaries in autonomous commerce systems.

## Problem Statement

Traditional e-commerce architectures concentrate control in a single monolithic system, creating security risks and limiting autonomous agent participation. As commerce increasingly involves AI agents making decisions on behalf of humans, we need architectural patterns that maintain human oversight while enabling autonomous operations.

This reference architecture demonstrates how **Agent-Centric Protocol (ACP) principles** can be applied to create secure, auditable commerce systems where autonomous agents operate within well-defined trust boundaries.

## Architecture Overview

The system is organized around six explicit trust boundaries that preserve human control while enabling autonomous commerce:

1. **Buyer Intent Layer** - Captures and validates human requirements
2. **Buyer Agent Decisioning** - Autonomous shopping logic with constraint enforcement  
3. **Merchant Checkout Control** - Product catalog and payment flow management
4. **Human Approval Boundary** - Manual override capability for high-risk decisions
5. **Mock Settlement Layer** - Escrow and payment simulation
6. **Audit Log** - Immutable transaction recording

### Key Design Principles

- **Controlled Delegation**: Agents receive scoped authority with explicit revocation
- **Trust Boundary Preservation**: Each boundary maintains its own state and validation rules
- **Human-in-the-Loop**: Critical decisions require explicit approval
- **Audit Immutability**: All cross-boundary actions are permanently recorded
- **Minimal Attack Surface**: Only necessary interfaces between boundaries

## Repository Structure

```
acp-agentic-commerce-refarch/
    README.md                          # This file
    requirements.txt                   # Python dependencies
    IMPLEMENTATION_PLAN.md             # Detailed development roadmap
    docs/
        architecture.md                # Trust boundaries and component roles
        scenarios.md                    # Use case scenarios
        adrs/                           # Architecture Decision Records
            ADR-001-acp-vs-custom-api.md
            ADR-002-human-approval-boundary.md
            ADR-003-mock-settlement-vs-real-payments.md
    diagrams/
        architecture.mmd               # Mermaid architecture diagram
    data/
        products.json                  # Sample product catalog
    backend/
        app.py                         # Simple HTTP server (canonical entrypoint)
        app_fastapi.py                 # Original FastAPI version (deprecated)
        storage.py                     # In-memory storage layer
        models/
            schemas.py                 # Plain Python data models
        agents/
            buyer_agent.py             # Autonomous shopping logic
            approval_agent.py          # Human-in-the-loop approval
        merchant/
            catalog.py                 # Product catalog management
            checkout_api.py            # Checkout process API
        settlement/
            escrow.py                  # Mock escrow and settlement
    streamlit_app/
        app.py                         # Human oversight interface
    tests/
        test_checkout_flow.py          # End-to-end integration tests
        test_simple_flow.py            # Manual end-to-end test runner
        test_streamlit_app.py         # Streamlit AppTest UI tests
        test_ui_basic.py               # Basic UI structure test
```

## Setup and Run Instructions

### Prerequisites
- Python 3.14+
- Git

### Installation

```bash
# Clone the repository
git clone <repository-url>
cd acp-agentic-commerce-refarch

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Load sample data (automatically handled by backend startup)
```

### Running the System

```bash
# Start the backend API (canonical entrypoint)
python backend/app.py

# In a separate terminal, start the Streamlit interface
python -m streamlit run streamlit_app/app.py
```

Access points:
- Backend API: http://localhost:8000
- Streamlit UI: http://localhost:8501

### Testing

```bash
# Run end-to-end integration tests
python tests/test_simple_flow.py

# Run Streamlit UI tests
python tests/test_streamlit_app.py

# Run pytest (limited by Python 3.14 compatibility)
python -m pytest tests/test_checkout_flow.py -q
```

## Demo Scenario

**"Buy a laptop bag under $120 with fast shipping"**

### Demo Flow

1. **User Input**: Enter "Find a laptop bag under $120 with fast shipping" in Streamlit UI
2. **Agent Processing**: Buyer agent selects "Executive Laptop Briefcase" ($119.99)
3. **Approval Boundary**: System requires human approval (price > $100 threshold)
4. **Human Decision**: Approve or reject the purchase request
5. **Checkout Completion**: System processes approved transaction
6. **Settlement**: Mock escrow creates settlement record
7. **Audit Trail**: Complete timeline shows all actions and decisions

### Expected Results

- **Product**: Executive Laptop Briefcase
- **Price**: $119.99 (within budget)
- **Approval Required**: Yes (price exceeds $100 threshold)
- **Final Status**: Approved and settled
- **Audit Events**: 5+ events logged chronologically

## Why This Matters

### For Architects
- Demonstrates trust boundary design patterns
- Shows how to maintain human control in autonomous systems
- Provides reference for secure agent commerce integration

### For Product Teams
- Illustrates user experience trade-offs in autonomous commerce
- Shows where human approval adds value vs. creates friction
- Provides framework for feature prioritization

### For Security Teams
- Explicit threat modeling across trust boundaries
- Clear audit trails for compliance
- Minimal attack surface through scoped delegation

## Known Limitations

### Technical Constraints
- **FastAPI replaced**: Original FastAPI backend replaced with simple HTTP server for Python 3.14 compatibility
- **Pydantic compatibility**: Limited pytest functionality due to Python 3.14 + Pydantic compatibility issues
- **In-memory storage only**: No persistence complexity for v1
- **Mock settlement**: No real payment processing to focus on architecture

### Intentional Limitations
- **Single merchant**: Federation complexity deferred
- **No OAuth**: Identity management scoped to demo
- **Limited catalog**: 8 sample products for demonstration

## Trade-offs

### Architectural Decisions
- **Human approval as boundary**: Explicit control point vs. implicit trust
- **Agent autonomy with constraints**: Freedom within guardrails vs. rigid workflows
- **Audit-first design**: Compliance and observability vs. performance optimization

## Future Roadmap

### Phase 2: Multi-Merchant Federation
- Merchant discovery and reputation systems
- Cross-merchant settlement coordination
- Federated identity and trust propagation

### Phase 3: Real-World Integration
- Stripe payment processing
- Real shipping API integration
- Production-grade persistence

### Phase 4: Advanced Agent Capabilities
- Multi-agent collaboration
- Learning and adaptation
- Complex constraint optimization

### Phase 5: Enterprise Features
- Multi-tenant support
- Advanced compliance reporting
- High-availability deployment patterns

## Architecture Decision Records

Key architectural decisions are documented in the `docs/adrs/` directory:
- [ADR-001](docs/adrs/ADR-001-acp-vs-custom-api.md): ACP-inspired vs. Custom API approach
- [ADR-002](docs/adrs/ADR-002-human-approval-boundary.md): Human approval as trust boundary
- [ADR-003](docs/adrs/ADR-003-mock-settlement-vs-real-payments.md): Mock settlement strategy

## Contributing

This is a reference architecture. Changes should preserve the core trust boundary principles and maintain the balance between autonomous operation and human control.

## License

MIT License - see LICENSE file for details.

---

*This reference architecture demonstrates how ACP principles can be applied to create secure, auditable commerce systems where autonomous agents operate within well-defined trust boundaries while preserving human oversight.*
