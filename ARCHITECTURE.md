# Architecture Overview

This document describes the structure and design of OSCAL GRC Skills.

---

## What Are Agent Skills?

Agent Skills are markdown instruction files (`SKILL.md`) that teach AI agents how to perform specific tasks. They follow the [Anthropic Agent Skills specification](https://agentskills.io/).

Unlike traditional software libraries, skills are:
- **Not executable code** — They're instructions, not programs
- **Model-agnostic** — Work with Claude, GPT, and other LLMs
- **Composable** — Multiple skills can be combined
- **Human-readable** — Plain markdown anyone can understand and modify

---

## Project Structure

```
oscal-grc-skills/
├── skills/                          # All skill definitions
│   ├── oscal-parser/
│   │   └── SKILL.md                 # Parser instructions
│   ├── oscal-validator/
│   │   └── SKILL.md                 # Validation instructions
│   ├── controls-extractor/
│   │   └── SKILL.md                 # Control extraction
│   ├── control-mapper/
│   │   └── SKILL.md                 # Framework mapping
│   ├── risk-assessor/
│   │   └── SKILL.md                 # Risk analysis
│   ├── compliance-report-generator/
│   │   └── SKILL.md                 # Report generation
│   ├── evidence-collector/
│   │   └── SKILL.md                 # Evidence management
│   ├── control-implementation-generator/
│   │   └── SKILL.md                 # Implementation narratives
│   ├── workflow-orchestrator/
│   │   └── SKILL.md                 # Multi-skill workflows
│   ├── advanced-oscal-validator/
│   │   └── SKILL.md                 # Deep validation
│   ├── component-definition-builder/
│   │   └── SKILL.md                 # Component definitions
│   ├── oscal-visualizer/
│   │   └── SKILL.md                 # Diagrams & visuals
│   └── oscal-text-converter/
│       └── SKILL.md                 # OSCAL ↔ plain text
│
├── examples/                        # Sample OSCAL files
│   ├── sample_catalog.json
│   ├── sample_ssp.json
│   ├── fedramp_ssp_template.json
│   ├── fedramp_poam_template.json
│   └── fedramp_component_definition.json
│
├── data/                            # Reference data
├── evidence/                        # Evidence templates
├── workflows/                       # Workflow definitions
│
├── README.md                        # Main documentation
├── USAGE_GUIDE.md                   # How to use skills
├── CONTRIBUTING.md                  # Contribution guidelines
├── CHANGELOG.md                     # Version history
├── LICENSE                          # MIT License
└── SECURITY.md                      # Security policy
```

---

## Skill Anatomy

Each `SKILL.md` file follows this structure:

```markdown
---
name: skill-name
description: Brief description of what the skill does
---

# Skill Name

## Purpose
What this skill accomplishes

## Inputs
What the skill expects to receive

## Outputs
What the skill produces

## Instructions
Step-by-step guide for the AI agent

## Examples
Sample inputs and expected outputs
```

---

## Skill Categories

### Foundation Skills
Core capabilities for working with OSCAL:

```
┌──────────────────┐    ┌──────────────────┐    ┌──────────────────┐
│   oscal-parser   │───►│  oscal-validator │───►│controls-extractor│
│                  │    │                  │    │                  │
│  Parse JSON/     │    │  Validate        │    │  Extract         │
│  YAML/XML        │    │  structure       │    │  controls        │
└──────────────────┘    └──────────────────┘    └──────────────────┘
```

### Analysis Skills
Deep analysis and risk assessment:

```
┌──────────────────┐    ┌──────────────────┐    ┌──────────────────┐
│  control-mapper  │    │  risk-assessor   │    │evidence-collector│
│                  │    │                  │    │                  │
│  NIST → ISO      │    │  Gaps & risks    │    │  Evidence        │
│  mapping         │    │  analysis        │    │  planning        │
└──────────────────┘    └──────────────────┘    └──────────────────┘
```

### Output Skills
Generate documents and reports:

```
┌──────────────────┐    ┌──────────────────┐    ┌──────────────────┐
│compliance-report │    │ control-impl-gen │    │oscal-visualizer  │
│   -generator     │    │                  │    │                  │
│                  │    │  Implementation  │    │  Diagrams &      │
│  Audit reports   │    │  narratives      │    │  charts          │
└──────────────────┘    └──────────────────┘    └──────────────────┘
```

### Orchestration
Combine skills for complex workflows:

```
┌─────────────────────────────────────────────────────────────────┐
│                    workflow-orchestrator                        │
│                                                                 │
│  ┌─────────┐   ┌─────────┐   ┌─────────┐   ┌─────────┐        │
│  │ Parse   │──►│Validate │──►│ Analyze │──►│ Report  │        │
│  └─────────┘   └─────────┘   └─────────┘   └─────────┘        │
└─────────────────────────────────────────────────────────────────┘
```

---

## Data Flow

```
                    User Request
                         │
                         ▼
              ┌─────────────────────┐
              │   Load Skill(s)     │
              │   from SKILL.md     │
              └──────────┬──────────┘
                         │
                         ▼
              ┌─────────────────────┐
              │   Claude/AI Agent   │
              │   Reads & Follows   │
              │   Instructions      │
              └──────────┬──────────┘
                         │
                         ▼
              ┌─────────────────────┐
              │   Process OSCAL     │
              │   Document(s)       │
              └──────────┬──────────┘
                         │
                         ▼
              ┌─────────────────────┐
              │   Generate Output   │
              │   (Report/Analysis) │
              └─────────────────────┘
```

---

## Supported Standards

| Standard | Version | Description |
|----------|---------|-------------|
| OSCAL | 1.1.2 | Open Security Controls Assessment Language |
| NIST 800-53 | Rev 5 | Federal security controls |
| NIST CSF | 2.0 | Cybersecurity Framework |
| ISO 27001 | 2022 | Information security management |
| CIS Controls | v8 | Critical security controls |
| PCI-DSS | 4.0 | Payment card security |
| HIPAA | — | Healthcare security |
| SOC 2 | — | Service organization controls |
| CMMC | 2.0 | DoD cybersecurity maturity |

---

## Extensibility

### Adding New Skills

1. Create a new folder under `skills/`
2. Add a `SKILL.md` file following the format above
3. Test with Claude or your preferred AI agent
4. Submit a PR

### Modifying Existing Skills

Skills are plain markdown — edit them like any documentation:
- Add new instructions or examples
- Refine output formats
- Expand framework coverage

---

## Design Principles

1. **Instructions, not code** — Skills teach, they don't execute
2. **Human-readable** — Anyone can understand and modify skills
3. **Composable** — Skills work together seamlessly
4. **Framework-agnostic** — Support multiple compliance frameworks
5. **OSCAL-native** — Built around OSCAL 1.1.2 specification
