# MCP Security Workflow Registry

**Proven patterns for coordinating tools across the MCP security ecosystem**

---

## Overview

This registry documents effective workflows that combine multiple tools to accomplish common MCP security goals. These patterns emerge from real usage and provide templates for users while maintaining flexibility for adaptation.

**Philosophy**: These are **starting points and suggestions**, not rigid requirements. Users can adapt, combine, or ignore these patterns based on their specific needs and context.

---

## Core Workflow Patterns

### **Pattern 1: Discovery → Assessment → Decision**
**Scenario**: "I need an MCP server for [specific functionality]"

#### Workflow Steps
```
1. DISCOVERY
   └── Use mcpserver-finder to discover and evaluate candidates
   
2. SECURITY ASSESSMENT  
   └── Use mcpserver-audit on top candidates
   
3. DECISION POINT
   ├── Safe to use → Deploy with standard security
   ├── Needs fixes → Route to mcpserver-builder
   ├── Needs hardening → Route to mcpserver-operator  
   └── Too risky → Return to discovery for alternatives
```

#### Context Adaptations
- **Local Use**: Light assessment, focus on functionality
- **Remote Single-User**: Basic security assessment, standard deployment
- **Remote Multi-User**: Comprehensive assessment, likely needs fixes or hardening
- **Enterprise**: Full security audit, almost certainly needs remediation

#### Tool Synergies
- **Finder provides context** to audit (deployment scenario, quality baseline)
- **Audit findings inform** builder (specific vulnerabilities to fix)
- **Audit findings inform** operator (compensating controls needed)

#### Example Usage
```
# Phase 1: Discovery
read ../../mcpserver-finder/prompts/main-prompt.md and find web search MCP servers for enterprise deployment

# Phase 2: Assessment  
read ../../mcpserver-audit/prompts/main-prompt.md and assess security of [chosen server]

# Phase 3: Decision
[Based on findings, route to builder for fixes OR operator for hardening]
```

---

### **Pattern 2: Assessment → Remediation → Validation**
**Scenario**: "I have this MCP server, how do I make it secure?"

#### Workflow Steps
```
1. SECURITY ASSESSMENT
   └── Use mcpserver-audit to identify vulnerabilities
   
2. REMEDIATION PLANNING
   ├── Critical/High issues → mcpserver-builder for fixes
   ├── Deployment concerns → mcpserver-operator for controls
   └── Acceptable risk → Document and monitor
   
3. VALIDATION
   └── Re-assess with mcpserver-audit to verify improvements
```

#### Decision Logic
- **Fixable Issues**: Code vulnerabilities → Builder
- **Environmental Issues**: Deployment risks → Operator  
- **Hybrid Approach**: Some fixes + some operational controls
- **Risk Acceptance**: Document residual risk and monitoring

#### Example Usage
```
# Phase 1: Assessment
read ../../mcpserver-audit/prompts/main-prompt.md and audit security of my-custom-server

# Phase 2: Remediation (based on findings)
read ../../mcpserver-builder/prompts/main-prompt.md and fix vulnerabilities: [list]
# OR
read ../../mcpserver-operator/prompts/main-prompt.md and secure deployment for: [server with known issues]

# Phase 3: Validation
read ../../mcpserver-audit/prompts/main-prompt.md and re-assess security after fixes
```

---

### **Pattern 3: Build → Audit → Deploy**
**Scenario**: "I'm building a new MCP server, how do I do it securely?"

#### Workflow Steps
```
1. SECURE DEVELOPMENT
   └── Use mcpserver-builder for secure development guidance
   
2. SECURITY VALIDATION
   └── Use mcpserver-audit to validate security implementation
   
3. SECURE DEPLOYMENT
   └── Use mcpserver-operator for deployment security
```

#### Development Integration
- **Design Phase**: Security-by-design principles from builder
- **Implementation Phase**: Secure coding practices and patterns
- **Testing Phase**: Security testing and vulnerability assessment
- **Deployment Phase**: Operational security and monitoring

#### Example Usage
```
# Phase 1: Secure Development
read ../../mcpserver-builder/prompts/main-prompt.md and guide secure development of [new server concept]

# Phase 2: Security Validation
read ../../mcpserver-audit/prompts/main-prompt.md and validate security of newly built server

# Phase 3: Secure Deployment  
read ../../mcpserver-operator/prompts/main-prompt.md and plan secure deployment
```

---

## Educational Workflow Patterns

### **Pattern 4: Learning-Focused Discovery**
**Scenario**: "I want to learn about MCP security while finding/evaluating servers"

#### Educational Integration
```
ANY CORE WORKFLOW + Educational Focus:
├── Start with learning objectives and skill assessment
├── Use educational modes of all tools
├── Focus on teaching concepts through practical application  
├── Build understanding progressively across tool usage
└── Capture learning outcomes and skill development
```

#### Example Approach
```
# Educational Discovery
read ../../mcpserver-finder/prompts/main-prompt.md and teach me server evaluation while finding [specific need]

# Educational Assessment
read ../../mcpserver-audit/prompts/main-prompt.md and teach me security assessment using [chosen server]
```

---

## Multi-Tool Coordination Patterns

### **Parallel Assessment Pattern**
**Scenario**: Comprehensive security evaluation using multiple tools

#### Coordination Strategy
```
PARALLEL TOOL USAGE:
├── mcpserver-audit (primary assessment + education)
├── Third-party static analysis (additional coverage)
├── Dependency scanners (supply chain security)
└── Specialized tools (based on server technology)

SYNTHESIS:
├── Correlate findings across tools
├── Deduplicate similar vulnerabilities  
├── Prioritize based on deployment context
└── Create unified security posture assessment
```

### **Iterative Improvement Pattern**
**Scenario**: Continuous improvement of server security

#### Iteration Cycle
```
1. BASELINE ASSESSMENT
   └── Initial security audit and quality evaluation
   
2. TARGETED IMPROVEMENT  
   ├── Address highest-priority issues first
   ├── Use builder for code fixes
   ├── Use operator for deployment controls
   └── Apply incremental improvements
   
3. RE-ASSESSMENT
   └── Validate improvements and identify remaining issues
   
4. REPEAT
   └── Continue until acceptable security posture achieved
```

---

## Context-Specific Workflow Adaptations

### **Local Development Workflows**
**Focus**: Functionality and basic security, learning opportunities

**Typical Pattern**: Discovery → Light Assessment → Direct Use
- Minimal security requirements
- Educational focus if user wants to learn
- Emphasis on functionality and ease of use

### **Remote Single-User Workflows**  
**Focus**: Input validation, credential security, basic hardening

**Typical Pattern**: Discovery → Standard Assessment → Fix Critical Issues → Deploy
- Focus on obvious security vulnerabilities
- Basic operational security
- Reasonable security without over-engineering

### **Remote Multi-User Workflows**
**Focus**: Comprehensive security, access controls, monitoring

**Typical Pattern**: Discovery → Comprehensive Audit → Builder + Operator → Validation
- Full security assessment required
- Likely needs both code fixes and operational controls
- Comprehensive deployment security

### **Enterprise Workflows**
**Focus**: Full security hardening, compliance, governance

**Typical Pattern**: Discovery → Multi-Tool Audit → Comprehensive Remediation → Full Deployment Security → Compliance Validation
- Multiple assessment tools for comprehensive coverage
- Both vulnerability fixes and deployment hardening required
- Compliance and governance considerations throughout

---

## Workflow Decision Points

### **When to Use Builder vs Operator**
```
DECISION LOGIC:
├── Code-Level Issues Found
│   ├── Input validation, authentication, authorization → Builder
│   ├── Insecure coding patterns, vulnerability patterns → Builder
│   └── Architecture or design flaws → Builder
├── Deployment-Level Concerns
│   ├── Network exposure, access controls → Operator
│   ├── Monitoring, logging, incident response → Operator
│   └── Infrastructure security, isolation → Operator
├── Both Needed
│   ├── Comprehensive security issues → Builder first, then Operator
│   ├── Timeline constraints → Operator for immediate risk reduction
│   └── Compliance requirements → Usually both Builder and Operator
└── Neither Sufficient
    ├── Fundamental security flaws → Don't use server
    ├── Architecture problems → Major redesign needed
    └── Unmaintained/abandoned → Find alternative server
```

### **When to Loop Back to Discovery**
```
DISCOVERY RE-ENTRY POINTS:
├── Unacceptable Security Risk
│   └── Current server too risky, need alternatives
├── Missing Functionality
│   └── Server doesn't meet requirements after evaluation
├── Maintenance Concerns  
│   └── Server quality issues, need better-maintained alternative
├── Better Options Available
│   └── Discovery of superior alternatives during assessment
└── User Preference Change
    └── Requirements or context evolved during workflow
```

---

## Future Workflow Evolution

### **Pattern Learning**
- **Success Tracking**: Monitor which patterns work best for different scenarios
- **User Feedback**: Adapt patterns based on user experience and outcomes
- **Effectiveness Metrics**: Measure workflow success and efficiency
- **Community Contribution**: Learn from community usage and innovation

### **Workflow Innovation**
- **New Pattern Development**: Create new patterns for emerging needs
- **Pattern Combination**: Develop meta-patterns that combine existing workflows
- **Specialized Patterns**: Domain-specific or technology-specific workflows
- **Automation Opportunities**: Identify steps that could be automated while preserving user control

### **Community Integration**
- **Pattern Sharing**: Share successful patterns with broader community
- **Collaborative Development**: Work with community to refine and extend patterns
- **Best Practice Documentation**: Document effective approaches and anti-patterns
- **Knowledge Transfer**: Help other projects adopt effective orchestration patterns

---

*These workflow patterns provide structure and guidance while maintaining the flexibility for users to adapt, combine, or create their own approaches based on specific needs and context.*