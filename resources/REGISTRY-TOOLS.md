# MCP Security Tool Registry

**Comprehensive catalog of available MCP security tools with capabilities, limitations, and integration guidance**

---

## Internal MCP Security Tools

### **mcpserver-finder**
**Purpose**: Discovery and quality evaluation of MCP servers

**Location**: 
- **File**: `../../mcpserver-finder/prompts/main-prompt.md`
- **Repo**: `https://github.com/modelcontextprotocol-security/mcpserver-finder`

**Maturity**: ⚡ **Proof of Concept** - Solid methodology, needs real server evaluations

**Good At**:
- Educational approach to server discovery and evaluation
- Systematic quality assessment with confidence frameworks
- Requirements-driven server matching
- Teaching server evaluation skills through Socratic method
- Comparative analysis of multiple server options

**Not Good At**:
- Automated server discovery (manual process)
- Large-scale server indexing
- Real-time server monitoring
- Security vulnerability detection (use audit for that)

**Known Gaps**:
- Limited real server evaluation examples
- No automated discovery mechanisms  
- Discovery data needs population with community intelligence
- Path portability issues for different environments

**Works Well With**:
- **mcpserver-audit**: Hand off discovered servers for security assessment
- **Community registries**: Leverage existing MCP server lists and directories
- **Third-party discovery tools**: Complement with automated discovery mechanisms

**Typical Usage**:
```
read ../../mcpserver-finder/prompts/main-prompt.md and help me find MCP servers for [describe need]
```

---

### **mcpserver-audit**
**Purpose**: Security vulnerability assessment and education

**Location**:
- **File**: `../../mcpserver-audit/prompts/main-prompt.md`  
- **Repo**: `https://github.com/modelcontextprotocol-security/mcpserver-audit`

**Maturity**: ⚡ **Proof of Concept** - Educational framework complete, limited vulnerability checks

**Good At**:
- Educational security assessment with Socratic teaching
- AIVSS vulnerability scoring and explanation
- CWE mapping and vulnerability classification
- Teaching security thinking and threat modeling
- Manual security code review guidance

**Not Good At**:
- Automated vulnerability scanning (manual process)
- Large-scale code analysis
- Vulnerability remediation (use builder for that)
- Deployment security (use operator for that)

**Known Gaps**:
- Limited CWE coverage (only 2 security checks implemented)
- No integration with automated scanning tools
- Manual process requires human analyst involvement
- Missing many common vulnerability detection patterns

**Works Well With**:
- **mcpserver-finder**: Assess security of discovered servers
- **mcpserver-builder**: Hand off vulnerabilities for remediation
- **Third-party scanners**: Combine with Semgrep, Bandit, etc. for broader coverage
- **Dependency scanners**: Complement with npm audit, Snyk, etc.

**Typical Usage**:
```
read ../../mcpserver-audit/prompts/main-prompt.md and conduct security assessment of [server name]
```

---

### **mcpserver-builder**
**Purpose**: Security remediation and secure development guidance

**Location**:
- **File**: `../../mcpserver-builder/prompts/main-prompt.md`
- **Repo**: `https://github.com/modelcontextprotocol-security/mcpserver-builder`

**Maturity**: 🚧 **Early Development** - Intended functionality defined, implementation in progress

**Intended Capabilities**:
- Vulnerability remediation and fix generation
- Secure MCP server development guidance
- Security hardening and code improvement
- Educational secure coding practices
- Integration with vulnerability findings from audit tools

**Current Status**: Basic framework only - full implementation needed

**Intended Integration**:
- **mcpserver-audit**: Receive vulnerability findings for remediation
- **mcpserver-operator**: Coordinate fixes with deployment security
- **Development tools**: Integrate with existing development workflows

**Typical Usage** (Future):
```
read ../../mcpserver-builder/prompts/main-prompt.md and fix these security vulnerabilities: [list or file]
```

---

### **mcpserver-operator**
**Purpose**: Secure deployment and operational security controls

**Location**:
- **File**: `../../mcpserver-operator/prompts/main-prompt.md`
- **Repo**: `https://github.com/modelcontextprotocol-security/mcpserver-operator`

**Maturity**: 🚧 **Early Development** - Intended functionality defined, implementation in progress

**Intended Capabilities**:
- Deployment security planning and configuration
- Operational security controls implementation
- Runtime security monitoring and alerting
- Incident response procedures and automation
- Compliance and governance frameworks

**Current Status**: Basic framework only - full implementation needed

**Intended Integration**:
- **mcpserver-audit**: Apply security findings to deployment planning
- **mcpserver-builder**: Coordinate secure code with secure deployment
- **Infrastructure tools**: Integrate with containers, orchestration, monitoring
- **Compliance frameworks**: Support SOC2, PCI-DSS, etc. requirements

**Typical Usage** (Future):
```
read ../../mcpserver-operator/prompts/main-prompt.md and plan secure deployment for [context]
```

---

## Third-Party Tool Categories

### **Discovery Tools** (To Be Discovered)
**Purpose**: Alternative or complementary server discovery mechanisms

**Potential Tools**:
- MCP registry scrapers and indexers
- Automated quality assessment scanners
- Community recommendation engines
- Search and filtering tools for MCP ecosystems

**How to Find**: Use mcpserver-finder to discover additional discovery tools

---

#### **MCP Eval** (Hosted Compatibility & Capability Testing)
**Purpose**: Evaluate MCP servers for client compatibility, tool coverage, and basic performance

**Location**:
- **Hosted App**: https://www.mcpevals.ai/
- **Repo**: https://github.com/scorecard-ai/mcp-eval

**Maturity**: 🚀 **Production** - Hosted service with self-host option

**Good At**:
- Client compatibility matrix (ChatGPT, Claude, Cursor)
- OAuth 2.0 flow validation and testing
- Tool discovery with intelligent argument generation
- Performance metrics with real-time streaming logs
- One-click testing and easy report sharing

**Not Good At**:
- Security vulnerability scanning or code-level analysis (use mcpserver-audit and scanners)
- Deep protocol fuzzing or adversarial testing
- Offline/batch CLI workflows (use self-host/API if needed)

**Known Limitations**:
- Requires accessible server URL or proper OAuth configuration
- Generated test arguments may need manual adjustment for highly custom schemas
- Focused on compatibility and behavior, not security posture

**Works Well With**:
- **mcpserver-finder**: Screen discovered candidates for compatibility and readiness
- **mcpserver-audit**: Use as a preflight/regression check before/after security audits
- **mighty-security / other scanners**: Complement with vulnerability scanning for risk assessment

**Typical Usage** (Hosted):
```
1) Visit https://www.mcpevals.ai/
2) Paste the MCP server URL (OAuth-supported)
3) Run evaluation and export/share the report
```

**Outputs Captured**:
- Pass/fail per client (ChatGPT, Claude, Cursor)
- Tool-level success/error rates and logs
- Response time metrics (e.g., p50/p95) per tool
- OAuth/authorization flow results and errors

---

### **Security Assessment Tools**

#### **mighty-security** (Third-Party MCP Scanner)
**Purpose**: Automated MCP server vulnerability scanning and detection

**Location**: 
- **Repo**: `https://github.com/NineSunsInc/mighty-security`
- **Tool**: `python3 mighty_mcp.py check <server-url>`
- **Setup**: Requires Python 3.13+, optional Cerebras API key for LLM analysis

**Maturity**: 🚀 **Production** - Actively maintained, claims 500+ servers scanned in wild

**Good At**:
- Automated vulnerability detection (command injection, SSRF, credential theft, path traversal)
- Multi-language analysis (Python/JS/TS/Go/Rust) 
- ML/LLM-enhanced pattern recognition with Cerebras integration
- Production-ready CI/CD integration (returns exit codes)
- Web dashboard for results visualization and monitoring
- Real-world vulnerability patterns from actual MCP server analysis

**Not Good At**:
- Educational explanation of vulnerabilities (use mcpserver-audit for learning)
- Perfect accuracy (75-85% detection rate, ~5% false positives acknowledged)
- Obfuscated or heavily transformed code detection
- Runtime protection (basic monitoring only)

**Known Limitations**:
- Third-party tool - we haven't independently validated their vulnerability claims
- Newer tool - long-term maintenance and community support unknown
- May have different security philosophy than our educational approach

**Research/Beta Integration**:
- **Quick Pre-screening**: Run mighty-security before manual educational analysis
- **Bulk Assessment**: Scan multiple discovered servers efficiently  
- **Validation**: Compare automated findings with our manual assessment results
- **Learning**: Study their detection patterns to improve our own checks

**Works Well With**:
- **mcpserver-finder**: Pre-screen discovered servers for obvious vulnerabilities
- **mcpserver-audit**: Use automated findings as input for educational security analysis
- **mcpserver-builder**: Feed automated vulnerability findings into remediation planning

**Typical Usage** (Research):
```bash
# Basic automated scan
python3 mighty_mcp.py check https://github.com/some/mcp-server

# Enhanced with LLM analysis  
python3 mighty_mcp.py check https://github.com/some/mcp-server --llm

# Integration with our educational tools
mighty-security scan → mcpserver-audit manual analysis → mcpserver-builder fixes
```

**Research Questions**:
- How do their automated findings compare with our manual educational assessments?
- Can we learn from their vulnerability patterns to improve our own detection?
- What's the false positive rate on servers we know are safe?
- How does their approach complement our educational methodology?

---

#### **Other Security Assessment Tools**
**Purpose**: Additional security analysis capabilities for comprehensive coverage

**Known Categories**:
- **Static Analysis**: Semgrep, CodeQL, Bandit, ESLint security plugins
- **Dependency Scanning**: npm audit, Snyk, OWASP Dependency Check
- **Container Security**: Trivy, Anchore, Clair
- **Specialized Scanners**: Other MCP-specific security tools (to be discovered)

**Integration Approach**: Run in parallel with mcpserver-audit and mighty-security for comprehensive coverage

---

### **Remediation Tools** (To Be Discovered)
**Purpose**: Alternative approaches to vulnerability fixing and secure development

**Potential Categories**:
- Automated fix generation tools
- Security-focused code refactoring tools
- Secure development templates and frameworks
- Code transformation and improvement tools

**Integration**: Complement mcpserver-builder with specialized capabilities

---

### **Deployment and Operations Tools** (To Be Discovered)
**Purpose**: Infrastructure, monitoring, and operational security tools

**Known Categories**:
- **Container Orchestration**: Docker, Kubernetes with security configurations
- **Infrastructure as Code**: Terraform, Ansible with security hardening
- **Monitoring**: Security monitoring and observability platforms
- **Network Security**: Reverse proxies, API gateways, network controls

**Integration**: Complement mcpserver-operator with specialized infrastructure capabilities

---

## Registry Maintenance

### **Community Curation**
- Tools evaluated and recommended by community usage and feedback
- Quality assessments using our own tools (dogfooding)
- Regular review and updates based on tool evolution
- Community contribution and collaboration

### **Dynamic Discovery**
- Use mcpserver-finder to discover new security tools periodically
- Monitor GitHub, package repositories, and community resources
- Evaluate emerging tools using established assessment criteria
- Integrate promising tools into workflows and recommendations

### **Quality Standards**
- **Functional**: Tool must work reliably for its intended purpose
- **Maintained**: Evidence of active maintenance and community support
- **Secure**: Tool itself must meet security standards
- **Integrable**: Must work reasonably well with orchestration approach

---

*This registry evolves continuously as new tools are discovered, evaluated, and integrated into the MCP security ecosystem.*
