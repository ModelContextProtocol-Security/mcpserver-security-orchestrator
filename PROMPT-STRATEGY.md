# MCP Security Orchestrator - Prompt Strategy

**Progressive disclosure architecture for intelligent MCP security coordination**

---

## Overview

This document outlines the prompt architecture strategy for the MCP Security Orchestrator MVP. The core concept is **progressive disclosure** - starting with a lightweight main orchestrator prompt that dynamically loads specialized domain prompts only when needed.

**Key Innovation**: Rather than loading all capabilities upfront, we use conditional prompt loading based on user intent, creating an efficient and modular system.

---

## Architecture Philosophy

### Progressive Disclosure Pattern
- **Main Prompt**: High-level coordination and user intent detection
- **Domain Coordinators**: Specialized prompts for discovery, audit, build, operate, education
- **Tool Integration**: Load actual tool prompts only when domain is activated
- **Context Handoffs**: Smooth transitions between domains with preserved context

### Repository Layout Assumptions
```
parent-directory/
├── mcpserver-security-orchestrator/
│   └── prompts/
│       ├── main-prompt.md
│       ├── discovery-coordinator.md
│       ├── audit-coordinator.md
│       ├── build-coordinator.md
│       ├── operate-coordinator.md
│       └── educational-coordinator.md
├── mcpserver-finder/
│   └── prompts/
│       └── main-prompt.md
├── mcpserver-audit/
│   └── prompts/
│       └── main-prompt.md
├── mcpserver-builder/
│   └── prompts/
│       └── main-prompt.md
└── mcpserver-operator/
    └── prompts/
        └── main-prompt.md
```

---

## Prompt Architecture Design

### 1. Main Orchestrator Prompt (`main-prompt.md`)

**Purpose**: Entry point that identifies user intent and routes to appropriate domain

**Core Responsibilities**:
- User intent detection and classification
- Context gathering (deployment scenario, experience level, learning preferences)
- High-level capability overview without domain-specific details
- Progressive loading decision making
- Cross-domain workflow coordination

**Loading Logic Pattern**:
```markdown
## Progressive Loading Rules

IF user wants DISCOVERY/FINDING servers:
→ Load: `./discovery-coordinator.md`
→ Load: `../../mcpserver-finder/prompts/main-prompt.md`

IF user wants SECURITY ASSESSMENT:
→ Load: `./audit-coordinator.md` 
→ Load: `../../mcpserver-audit/prompts/main-prompt.md`

IF user wants REMEDIATION/BUILDING:
→ Load: `./build-coordinator.md`
→ Load: `../../mcpserver-builder/prompts/main-prompt.md`

IF user wants DEPLOYMENT:
→ Load: `./operate-coordinator.md`
→ Load: `../../mcpserver-operator/prompts/main-prompt.md`

IF user wants LEARNING focus:
→ Load: `./educational-coordinator.md`
→ Overlay educational approach on any domain
```

### 2. Domain Coordinator Prompts

#### Discovery Coordinator (`discovery-coordinator.md`)
**Purpose**: Orchestrate server discovery and evaluation workflows
**Integrates**: mcpserver-finder tool capabilities
**Key Workflows**: 
- Requirements-driven discovery
- Quality-focused evaluation
- Multi-option comparison
- Context-appropriate recommendations

#### Audit Coordinator (`audit-coordinator.md`)
**Purpose**: Orchestrate security assessment workflows  
**Integrates**: mcpserver-audit tool capabilities
**Key Workflows**:
- Context-driven security assessment
- Multi-tool coordination (when other scanners available)
- Risk analysis and prioritization
- Finding synthesis and reporting

#### Build Coordinator (`build-coordinator.md`)
**Purpose**: Orchestrate security remediation workflows
**Integrates**: mcpserver-builder tool capabilities  
**Key Workflows**:
- Vulnerability remediation planning
- Secure development guidance
- Fix validation and testing
- Progressive capability building

#### Operate Coordinator (`operate-coordinator.md`)
**Purpose**: Orchestrate secure deployment workflows
**Integrates**: mcpserver-operator tool capabilities
**Key Workflows**:
- Deployment security planning
- Operational controls implementation
- Monitoring and incident response setup
- Compliance and governance

#### Educational Coordinator (`educational-coordinator.md`)
**Purpose**: Layer educational approach over any domain
**Integrates**: Educational capabilities from all tools
**Key Workflows**:
- Learning style adaptation
- Progressive skill building
- Teaching moment identification
- Meta-learning and capability development

---

## Progressive Loading Mechanisms

### Intent Detection Triggers

**Discovery Intent Signals**:
- "I need an MCP server that..."
- "Find me servers for..."
- "What servers are available for..."
- "Compare options for..."

**Assessment Intent Signals**:
- "Is this server safe?"
- "Check the security of..."
- "Audit this server..."
- "What vulnerabilities does..."

**Remediation Intent Signals**:
- "Fix these security issues..."
- "How do I secure this server..."
- "Build a secure server that..."
- "Implement security controls..."

**Deployment Intent Signals**:
- "Deploy this server securely..."
- "Production deployment of..."
- "Operational security for..."
- "How do I run this safely..."

**Educational Intent Signals**:
- "I want to learn about..."
- "Teach me how to..."
- "Explain the security concepts..."
- "Walk me through..."

### Context Preservation Strategy

**Context Handoff Pattern**:
```markdown
## Context Handoff Template

**User Context**:
- Deployment Scenario: [Local/Remote Single/Remote Multi/Enterprise]
- Experience Level: [Beginner/Intermediate/Advanced/Expert]  
- Learning Preference: [Educational/Hybrid/Execution]
- Time Constraints: [Comprehensive/Standard/Quick]
- Risk Tolerance: [High Security/Balanced/Convenience]

**Current Workflow State**:
- Primary Intent: [Discovery/Assessment/Remediation/Deployment]
- Secondary Intents: [Cross-domain workflows]
- Previous Actions: [What's been done already]
- Pending Decisions: [What needs user input]

**Domain-Specific Context**:
[Passed to the loaded domain coordinator]
```

---

## Multi-Domain Workflow Patterns

### Sequential Workflows
**Discovery → Assessment → Remediation → Deployment**
- Context flows forward through each stage
- User can jump stages or go backwards
- Previous decisions inform subsequent stages

### Parallel Workflows  
**Assessment + Remediation (for known servers)**
- Run audit while planning fixes
- Coordinate findings with remediation planning
- Efficient for experienced users

### Educational Overlay Workflows
**Any Domain + Educational Coordinator**
- Educational coordinator provides learning layer
- Domain coordinator handles technical execution
- Adaptive depth based on user learning preferences

---

## Implementation Strategy

### Phase 1: Core MVP
1. **Main Orchestrator Prompt**: Intent detection and basic routing
2. **Discovery Coordinator**: Basic discovery workflow coordination  
3. **Audit Coordinator**: Basic assessment workflow coordination
4. **Simple Loading Logic**: Conditional prompt loading based on user intent

### Phase 2: Enhanced Coordination
1. **Build and Operate Coordinators**: Complete the tool ecosystem
2. **Educational Coordinator**: Learning overlay capabilities
3. **Cross-Domain Workflows**: Seamless multi-stage processes
4. **Advanced Context Management**: Sophisticated context preservation

### Phase 3: Advanced Features
1. **Dynamic Tool Discovery**: Integration with community tools
2. **Intelligent Routing**: ML-enhanced intent detection
3. **Workflow Optimization**: Learn from usage patterns
4. **Community Integration**: Shared patterns and best practices

---

## Technical Implementation Notes

### Prompt Loading Syntax
**Relative Path Strategy**:
- Use `../../tool-name/prompts/main-prompt.md` for tool integration
- Use `./coordinator-name.md` for orchestrator coordinators
- Maintain flexibility for different directory structures

**Loading Instructions**:
```markdown
## Progressive Loading Instructions

When user intent matches [TRIGGER_CONDITION]:
1. Load coordinator prompt: `./[coordinator-name].md`  
2. Load tool prompt: `../../[tool-name]/prompts/main-prompt.md`
3. Pass context using standard context handoff template
4. Begin coordinated workflow
```

### Context Management
**Context Variables**:
- User profile and preferences
- Current workflow state
- Previous actions and decisions
- Pending tasks and decisions
- Cross-domain dependencies

**Context Passing**:
- Standardized context templates
- Explicit context validation
- Context update mechanisms
- Context persistence patterns

---

## Benefits of This Architecture

### For Users
- **Faster Loading**: Only load what's needed
- **Cleaner Experience**: No overwhelming initial prompt
- **Flexible Workflows**: Jump between domains as needed
- **Learning Adaptation**: Educational overlay when desired

### For Development  
- **Modular Design**: Easy to develop and maintain individual coordinators
- **Testable Components**: Each coordinator can be tested independently
- **Extensible Architecture**: Easy to add new domains or tools
- **Community Integration**: Clear patterns for third-party tool integration

### for Maintenance
- **Clear Separation**: Domain expertise contained in coordinators
- **Version Management**: Update individual components independently  
- **Bug Isolation**: Issues contained to specific domains
- **Documentation Alignment**: Prompts mirror architectural documentation

---

## Future Enhancements

### Advanced Progressive Disclosure
- **Predictive Loading**: Pre-load likely next domains based on workflow patterns
- **Contextual Suggestions**: Suggest domain transitions based on current state
- **Workflow Templates**: Common multi-domain workflow shortcuts
- **User Customization**: Personal workflow preferences and shortcuts

### Intelligent Coordination
- **Intent Disambiguation**: Handle ambiguous user requests intelligently
- **Workflow Optimization**: Learn and suggest more efficient workflow paths
- **Error Recovery**: Graceful handling of domain transitions and failures
- **Community Learning**: Incorporate community workflow patterns

### Tool Ecosystem Evolution
- **Dynamic Tool Discovery**: Automatically discover and integrate new tools
- **Tool Quality Assessment**: Evaluate and rank available tools
- **Custom Tool Integration**: Support for organization-specific tools
- **Tool Coordination Optimization**: Learn optimal tool combinations

---

## Success Metrics

### User Experience Metrics
- **Time to First Value**: How quickly users get useful results
- **Workflow Completion Rates**: Percentage of started workflows completed
- **User Satisfaction**: Feedback on orchestration effectiveness
- **Learning Effectiveness**: Skill development and knowledge retention

### Technical Metrics  
- **Loading Performance**: Time to load and initialize domain coordinators
- **Context Preservation**: Accuracy of context handoffs between domains
- **Error Rates**: Failures in domain transitions and workflow execution
- **Resource Utilization**: Efficiency of progressive loading approach

### Ecosystem Metrics
- **Tool Integration Success**: Successful integration of new tools
- **Community Adoption**: Usage of orchestrator by community
- **Workflow Pattern Evolution**: Development of effective coordination patterns
- **Knowledge Sharing**: Community contribution to orchestration intelligence

---

*This prompt architecture enables intelligent, efficient coordination of MCP security workflows while maintaining flexibility for diverse user needs and evolving tool ecosystems.*