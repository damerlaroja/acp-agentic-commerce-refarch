# ADR-001: ACP-Inspired vs Custom API Approach

## Status
Accepted

## Context
The reference architecture needs to demonstrate how autonomous commerce systems can maintain security and human control while enabling agent participation. We must decide between adopting Agent-Centric Protocol (ACP) principles versus building a completely custom API approach.

## Decision
Adopt an **ACP-inspired approach** that implements the core principles of controlled delegation and trust boundaries, but does not attempt a full ACP implementation.

## Rationale

### Why ACP-Inspired Approach

#### 1. Trust Boundary Design
ACP provides well-defined patterns for creating trust boundaries between autonomous agents and human-controlled systems. This aligns perfectly with our goal of maintaining human oversight while enabling autonomous commerce.

#### 2. Controlled Delegation
ACP's delegation model allows agents to operate with explicit authority limits and revocation capabilities. This prevents privilege escalation and maintains human control over critical decisions.

#### 3. Audit-First Design
ACP emphasizes immutable audit trails for all agent actions. This provides the compliance and forensic capabilities essential for commerce systems.

#### 4. Industry Relevance
ACP represents emerging best practices for agent commerce systems. A reference architecture should demonstrate industry-relevant patterns.

#### 5. Educational Value
The principles are transferable to other domains where humans delegate to autonomous systems.

### Why Not Full ACP Implementation

#### 1. Complexity vs. Learning
A full ACP implementation would introduce significant protocol complexity that distracts from the core architectural learning objectives.

#### 2. Reference Scope
This is a reference architecture, not a production protocol implementation. The goal is to demonstrate patterns, not implement a complete protocol.

#### 3. Timeline Constraints
A full ACP implementation would require extensive protocol development, testing, and ecosystem integration that exceeds our reference timeline.

#### 4. Focus on Architecture
The value is in demonstrating trust boundary design, not protocol compliance.

#### 5. Mock Environment
In a reference environment with mock services, full protocol compliance provides limited additional value.

### What We Implement (ACP-Inspired)

#### Core Principles
1. **Explicit Delegation**: Agents receive clearly defined authority scopes
2. **Trust Boundaries**: Six distinct boundaries with validation rules
3. **Human-in-the-Loop**: Critical decisions require explicit approval
4. **Audit Immutability**: All cross-boundary actions are permanently recorded
5. **Revocation Capability**: Human control can override agent decisions

#### Architectural Patterns
1. **Boundary Controllers**: Each trust boundary has its own validation logic
2. **State Machines**: Clear state transitions with validation at each step
3. **Event Sourcing**: Audit trail based on immutable event logs
4. **Proxy Patterns**: Agents act on behalf of humans with limited authority
5. **Approval Workflows**: Human approval gates for high-risk decisions

#### What We Don't Implement
1. **Full Protocol Stack**: Complete ACP message formats and transport
2. **Cryptographic Primitives**: ACP's specific cryptographic requirements
3. **Multi-Party Negotiation**: Complex agent-to-agent protocols
4. **Federation Protocols**: Cross-organization trust establishment
5. **Discovery Mechanisms**: Dynamic agent and service discovery

## Consequences

### Positive Consequences

#### 1. Clear Architecture
The trust boundary approach provides a clean, understandable architecture that demonstrates key principles.

#### 2. Educational Value
Developers can see how to apply ACP principles without being overwhelmed by protocol details.

#### 3. Transferable Patterns
The patterns can be applied to other domains requiring human-agent collaboration.

#### 4. Reasonable Complexity
The implementation complexity matches the reference architecture scope.

#### 5. Future Extensibility
The architecture can be extended toward full ACP compliance if needed.

### Negative Consequences

#### 1. Limited Protocol Compliance
Not a fully ACP-compliant implementation, which may limit direct applicability.

#### 2. Simplified Security
Mock implementations don't demonstrate full security considerations.

#### 3. Narrow Scope
Single-merchant, single-scenario focus limits demonstration of broader capabilities.

#### 4. Educational Gaps
Developers may need additional resources to understand full ACP concepts.

### Mitigation Strategies

#### 1. Clear Documentation
Explicitly document what is ACP-inspired vs. full ACP implementation.

#### 2. Reference Materials
Provide links to ACP specifications for further learning.

#### 3. Extension Points
Design the architecture to allow extension toward full compliance.

#### 4. Use Case Focus
Emphasize that this demonstrates patterns, not complete protocol implementation.

## Alternatives Considered

### Alternative 1: Custom API Approach
Build a completely custom API without ACP influence.

**Pros**: 
- Maximum flexibility
- No external dependencies
- Simpler initial implementation

**Cons**:
- Misses industry best practices
- Limited educational value
- Reinvents known patterns
- No trust boundary guidance

**Rejected**: Would not demonstrate emerging best practices for agent commerce.

### Alternative 2: Full ACP Implementation
Implement complete ACP protocol compliance.

**Pros**:
- Industry standard compliance
- Maximum educational value
- Production-ready patterns

**Cons**:
- Excessive complexity for reference
- Longer development timeline
- Protocol complexity distracts from architecture
- Over-engineering for reference scope

**Rejected**: Would exceed reference architecture scope and timeline.

### Alternative 3: Hybrid Approach
Mix ACP principles with custom extensions.

**Pros**:
- Balance of standards and flexibility
- Can prioritize most valuable patterns

**Cons**:
- Inconsistent approach
- Confusing learning objectives
- Hard to maintain clear boundaries

**Rejected**: Would create confusion about what is standard vs. custom.

## Implementation Notes

### Phase 1: Foundation
- Define trust boundaries based on ACP principles
- Implement basic delegation patterns
- Create audit logging infrastructure

### Phase 2: Agent Integration
- Implement buyer agent with scoped authority
- Add approval workflow patterns
- Create boundary validation logic

### Phase 3: Control Enhancement
- Add human approval boundaries
- Implement revocation capabilities
- Enhance audit and compliance features

## Future Considerations

### Path to Full Compliance
The architecture is designed to allow extension toward full ACP compliance:

1. **Protocol Layer**: Add ACP message formats and transport
2. **Cryptography**: Implement ACP security primitives
3. **Federation**: Add multi-organization trust establishment
4. **Discovery**: Implement dynamic service discovery

### Evolution Strategy
1. **Reference Phase**: Demonstrate patterns with simplified implementation
2. **Production Phase**: Extend toward full protocol compliance
3. **Ecosystem Phase**: Integrate with broader ACP ecosystem

---

*This decision balances the educational value of ACP principles with the practical constraints of a reference architecture implementation.*
