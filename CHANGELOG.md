# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [1.0.0] - 2025-12-31

### Initial Release — Anthropic Agent Skills Format

OSCAL GRC Skills provides **14 agent skills** for cybersecurity compliance automation, following the [Anthropic Agent Skills specification](https://agentskills.io/).

Skills are markdown files that teach Claude and other AI agents how to perform OSCAL compliance tasks — no code installation required.

### Skills

| # | Skill | Description |
|---|-------|-------------|
| 1 | oscal-parser | Parse OSCAL documents (JSON, YAML, XML) |
| 2 | oscal-validator | Validate document structure and references |
| 3 | advanced-oscal-validator | Deep semantic validation and best practices |
| 4 | controls-extractor | Extract and analyze security controls |
| 5 | control-mapper | Map controls between frameworks (NIST, ISO, CIS, PCI-DSS) |
| 6 | risk-assessor | Automated risk assessment and gap analysis |
| 7 | compliance-report-generator | Generate audit-ready compliance reports |
| 8 | evidence-collector | Plan and track evidence collection |
| 9 | control-implementation-generator | Generate implementation guidance and narratives |
| 10 | workflow-orchestrator | Multi-step compliance workflow automation |
| 11 | component-definition-builder | Build reusable OSCAL component definitions |
| 12 | oscal-visualizer | Generate diagrams and visualizations |
| 13 | oscal-text-converter | Convert OSCAL to human-readable formats |
| 14 | oscal-catalog-provider | Fetch official NIST/FedRAMP catalogs from authoritative sources |

### Anti-Hallucination Policy

Every skill includes a **⛔ Authoritative Data Requirement** or **✅ Data Source Principle** section that:
- Defines what data sources are required for each task
- Specifies what the agent CAN provide (methodology, templates, formats)
- Specifies what the agent CANNOT provide (control definitions, framework mappings)
- Includes a hard-stop message template for when authoritative sources are missing

See [AUTHORITATIVE_DATA_POLICY.md](AUTHORITATIVE_DATA_POLICY.md) for the complete policy.

### Documentation

- README.md — Project overview and quick start
- AUTHORITATIVE_DATA_POLICY.md — Critical anti-hallucination policy
- USE_CASES.md — 12 practical scenarios for agent development
- USAGE_GUIDE.md — How to use individual skills
- ARCHITECTURE.md — Understanding skill structure
- QUICK_REFERENCE.md — Quick reference card
- CONTRIBUTING.md — How to contribute skills

### Framework Support

- NIST SP 800-53 Rev 5 (1,193 controls)
- FedRAMP HIGH/MODERATE/LOW/LI-SaaS baselines
- NIST Cybersecurity Framework 2.0
- Cross-framework mapping support (ISO 27001, CIS, PCI-DSS, HIPAA, SOC 2, CMMC)
- OSCAL 1.1.2 compatibility
