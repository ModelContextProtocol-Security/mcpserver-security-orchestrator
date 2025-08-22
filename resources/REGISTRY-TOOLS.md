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

### **Security Assessment Tools** (To Be Discovered)  
**Purpose**: Alternative or complementary security analysis capabilities

**Known Categories**:
- **Static Analysis**: Semgrep, CodeQL, Bandit, ESLint security plugins
- **Dependency Scanning**: npm audit, Snyk, OWASP Dependency Check
- **Container Security**: Trivy, Anchore, Clair
- **Specialized Scanners**: MCP-specific security tools (to be discovered)

**Integration Approach**: Run in parallel with mcpserver-audit for comprehensive coverage

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