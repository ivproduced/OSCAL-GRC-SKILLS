# OSCAL GRC Skills

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![OSCAL 1.1.2](https://img.shields.io/badge/OSCAL-1.1.2-green.svg)](https://pages.nist.gov/OSCAL/)
[![Agent Skills](https://img.shields.io/badge/Agent%20Skills-Anthropic-blueviolet.svg)](https://agentskills.io/)
[![FedRAMP Ready](https://img.shields.io/badge/FedRAMP-Ready-blue.svg)](https://www.fedramp.gov/)

**Agent skills for OSCAL (Open Security Controls Assessment Language) and Cybersecurity GRC (Governance, Risk, and Compliance) automation.**

Following the [Anthropic Agent Skills specification](https://agentskills.io/), these skills teach Claude and other AI agents how to work with OSCAL documents, security controls, and compliance workflows.

---

## 🎯 Overview

OSCAL GRC Skills provides **15 agent skills** for cybersecurity compliance automation:

- **Parsing & Validation** — Work with OSCAL documents (JSON, YAML, XML)
- **Control Analysis** — Extract and analyze security controls across frameworks
- **Risk Assessment** — Threat modeling and vulnerability analysis
- **Evidence Collection** — Compliance evidence gathering and management
- **Implementation Guidance** — Generate control implementation narratives
- **Workflow Orchestration** — End-to-end compliance automation
- **Visualization** — Generate diagrams and visual representations
- **Component Building** — Create reusable OSCAL component definitions

---

## ⛔ Critical: Authoritative Data Policy

**AI agents using these skills must NEVER rely on training knowledge for compliance-critical information.**

| Risk | Consequence |
|------|-------------|
| Failed Audits | Auditors require evidence from authoritative sources |
| Security Gaps | Incorrect control definitions leave systems vulnerable |
| Regulatory Violations | Using stale/wrong data causes compliance failures |
| Legal Liability | Organizations liable for misrepresenting compliance |

### The Golden Rule

> **If you don't have the authoritative source document, STOP and ask for it.**

All skills include built-in data policy enforcement. Skills that require control catalogs, framework mappings, or compliance requirements will stop and request the authoritative source document rather than proceeding with potentially incorrect training data.

**Read:** [AUTHORITATIVE_DATA_POLICY.md](AUTHORITATIVE_DATA_POLICY.md) for the complete policy.

---

## 📦 Skills

Each skill is a folder containing a `SKILL.md` file with instructions that Claude uses to perform compliance tasks.

| # | Skill | Description |
|---|-------|-------------|
| 1 | [oscal-parser](skills/oscal-parser/) | Parse OSCAL documents (JSON, YAML, XML) |
| 2 | [oscal-validator](skills/oscal-validator/) | Validate document structure and references |
| 3 | [controls-extractor](skills/controls-extractor/) | Extract and analyze security controls |
| 4 | [control-mapper](skills/control-mapper/) | Map controls between frameworks (NIST, ISO, CIS, PCI-DSS) |
| 5 | [risk-assessor](skills/risk-assessor/) | Automated risk assessment and POA&M generation |
| 6 | [compliance-report-generator](skills/compliance-report-generator/) | Generate audit-ready compliance reports |
| 7 | [evidence-collector](skills/evidence-collector/) | Plan and track evidence collection |
| 8 | [control-implementation-generator](skills/control-implementation-generator/) | Generate implementation guidance and narratives |
| 9 | [workflow-orchestrator](skills/workflow-orchestrator/) | Multi-step compliance workflow automation |
| 10 | [advanced-oscal-validator](skills/advanced-oscal-validator/) | Schema and business rule validation |
| 11 | [component-definition-builder](skills/component-definition-builder/) | Build reusable component definitions |
| 12 | [oscal-visualizer](skills/oscal-visualizer/) | Generate OSCAL diagrams and visualizations |
| 13 | [oscal-text-converter](skills/oscal-text-converter/) | Convert OSCAL to human-readable formats |
| 14 | [oscal-catalog-provider](skills/oscal-catalog-provider/) | Fetch official NIST/FedRAMP catalogs from authoritative sources |
| 15 | [oscal-ssp-validator](skills/oscal-ssp-validator/) | SSP-specific validation against NIST 800-18 and FedRAMP requirements |

---

## 🚀 Using These Skills

### In Claude.ai

Upload any skill folder to Claude or reference the `SKILL.md` file directly. Claude will learn the instructions and apply them to your compliance tasks.

### In Claude Code

Add this repository as a plugin:

```bash
/plugin marketplace add ivproduced/OSCAL-GRC-SKILLS
```

Or install skills directly:

```bash
/plugin install oscal-grc-skills@ivproduced/OSCAL-GRC-SKILLS
```

Then ask Claude to use the skills:

> "Use the controls-extractor skill to analyze this FedRAMP SSP"

### Via Claude API

Include the skill content in your system prompt or as reference material:

```python
from anthropic import Anthropic

client = Anthropic()

# Load a skill
with open("skills/oscal-parser/SKILL.md", "r") as f:
    skill_content = f.read()

response = client.messages.create(
    model="claude-sonnet-4-20250514",
    system=f"You have access to this skill:\n\n{skill_content}",
    messages=[
        {"role": "user", "content": "Parse this OSCAL catalog and summarize the controls..."}
    ]
)
```

---

## 📋 Supported Frameworks

| Framework | Code | Description |
|-----------|------|-------------|
| NIST 800-53 | NIST-800-53 | Federal security controls |
| NIST CSF | NIST-CSF | Cybersecurity Framework |
| ISO 27001 | ISO-27001 | International security standard |
| CIS Controls | CIS-Controls | Critical security controls |
| PCI-DSS | PCI-DSS | Payment card security |
| HIPAA | HIPAA | Healthcare security |
| SOC 2 | SOC2 | Service organization controls |
| CMMC | CMMC | DoD cybersecurity maturity |

---

## 📋 Supported OSCAL Models

| Model | Description |
|-------|-------------|
| Catalog | Security control definitions (e.g., NIST 800-53) |
| Profile | Baseline customizations and overlays |
| SSP | System Security Plans |
| SAP | Security Assessment Plans |
| SAR | Security Assessment Results |
| POA&M | Plan of Action & Milestones |
| Component Definition | Reusable component controls |

---

## 💡 Example Use Cases

### FedRAMP Package Review

> "Review this FedRAMP SSP for compliance gaps against the Moderate baseline"

Claude will use:
- `oscal-parser` to read the SSP
- `oscal-validator` to check structure
- `controls-extractor` to get implemented controls
- `risk-assessor` to identify gaps and risks
- `compliance-report-generator` to produce findings

### Multi-Framework Mapping

> "Map our NIST 800-53 controls to ISO 27001 requirements"

Claude will use:
- `controls-extractor` to get current controls
- `control-mapper` to find ISO equivalents
- Report mapping confidence and gaps

### SSP Development

> "Generate control implementation narratives for AC-2 in our Azure environment"

Claude will use:
- `control-implementation-generator` with cloud context
- Produce Azure-specific implementation guidance

### Continuous Monitoring

> "Check this SSP against our baseline and generate a status report"

Claude will use:
- `oscal-parser` and `oscal-validator`
- `compliance-report-generator` for status report
- `risk-assessor` for trend analysis

---

## 🗂️ Project Structure

```
oscal-skills/
├── skills/
│   ├── oscal-parser/
│   │   └── SKILL.md
│   ├── oscal-validator/
│   │   └── SKILL.md
│   ├── controls-extractor/
│   │   └── SKILL.md
│   ├── control-mapper/
│   │   └── SKILL.md
│   ├── risk-assessor/
│   │   └── SKILL.md
│   ├── compliance-report-generator/
│   │   └── SKILL.md
│   ├── evidence-collector/
│   │   └── SKILL.md
│   ├── control-implementation-generator/
│   │   └── SKILL.md
│   ├── workflow-orchestrator/
│   │   └── SKILL.md
│   ├── advanced-oscal-validator/
│   │   └── SKILL.md
│   ├── component-definition-builder/
│   │   └── SKILL.md
│   ├── oscal-visualizer/
│   │   └── SKILL.md
│   ├── oscal-text-converter/
│   │   └── SKILL.md
│   └── oscal-catalog-provider/
│       └── SKILL.md
├── examples/
│   ├── sample_catalog.json
│   ├── sample_ssp.json
│   └── sample_component.json
├── AUTHORITATIVE_DATA_POLICY.md   # ⛔ CRITICAL - Read first
├── USE_CASES.md
├── USAGE_GUIDE.md
├── README.md
└── LICENSE
```

---

## 📚 Documentation

| Document | Description |
|----------|-------------|
| [AUTHORITATIVE_DATA_POLICY.md](AUTHORITATIVE_DATA_POLICY.md) | **⛔ Read first** — Anti-hallucination policy for compliance work |
| [USE_CASES.md](USE_CASES.md) | 12 practical scenarios for agent development |
| [USAGE_GUIDE.md](USAGE_GUIDE.md) | How to use individual skills |
| [ARCHITECTURE.md](ARCHITECTURE.md) | Understanding skill structure |
| [QUICK_REFERENCE.md](QUICK_REFERENCE.md) | Quick reference card |
| [CONTRIBUTING.md](CONTRIBUTING.md) | How to contribute skills |
| [CHANGELOG.md](CHANGELOG.md) | Version history |

---

## 🙏 Acknowledgments

This project was inspired by incredible work from the OSCAL community:

| Project | Inspiration |
|---------|-------------|
| [IBM Trestle](https://github.com/oscal-compass/compliance-trestle) | Workspace patterns, validation approaches |
| [oscal-pydantic](https://github.com/RS-Credentive/oscal-pydantic) | Type-safe models, validation patterns |
| [Lula](https://github.com/defenseunicorns/lula) | Validation automation, policy-as-code |
| [CivicActions Components](https://github.com/CivicActions/oscal-component-definitions) | Component definition patterns |
| [oscal-diagrams](https://github.com/degenaro/oscal-diagrams) | OSCAL visualization concepts |
| [OSCAL Club](https://oscal.club) | Community knowledge and best practices |

---

## 📄 License

MIT License - See [LICENSE](LICENSE) for details.

---

## 🤝 Contributing

Contributions welcome! Please:

1. Fork the repository
2. Create a feature branch
3. Add or improve skills following the [Agent Skills specification](https://agentskills.io/)
4. Submit a pull request

---

## 📚 Resources

- [Agent Skills Specification](https://agentskills.io/)
- [NIST OSCAL](https://pages.nist.gov/OSCAL/)
- [FedRAMP OSCAL Resources](https://www.fedramp.gov/oscal/)
- [What are skills?](https://support.claude.com/en/articles/12512176-what-are-skills)
- [Creating custom skills](https://support.claude.com/en/articles/12512198-creating-custom-skills)
