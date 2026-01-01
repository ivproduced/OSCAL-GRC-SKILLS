# Quick Reference

## Load a Skill

**Claude.ai:** Upload the `SKILL.md` file from any skill folder

**Claude Code:** `/plugin marketplace add ivproduced/OSCAL-GRC-SKILLS`

**API:** Include skill content in your system prompt

---

## Available Skills

| Skill | What It Does |
|-------|--------------|
| `oscal-parser` | Read OSCAL JSON/YAML/XML |
| `oscal-validator` | Check document structure |
| `advanced-oscal-validator` | Deep validation + best practices |
| `controls-extractor` | Get control lists |
| `control-mapper` | Map NIST ↔ ISO ↔ CIS ↔ PCI-DSS |
| `risk-assessor` | Identify gaps and risks |
| `compliance-report-generator` | Create audit reports |
| `evidence-collector` | Track evidence collection |
| `control-implementation-generator` | Write implementation narratives |
| `workflow-orchestrator` | Chain multiple skills |
| `component-definition-builder` | Build reusable components |
| `oscal-visualizer` | Generate diagrams |
| `oscal-text-converter` | OSCAL ↔ plain English |

---

## Common Tasks

### Parse an SSP
> "Parse this SSP and summarize the system description"

### Validate a document
> "Validate this OSCAL catalog for structural issues"

### Extract controls
> "List all AC (Access Control) family controls from this catalog"

### Map frameworks
> "Map these NIST 800-53 controls to ISO 27001"

### Generate a report
> "Create a FedRAMP compliance summary from this SSP"

### Assess risks
> "Identify control gaps and risk levels in this system"

---

## Supported Formats

| Format | Extensions |
|--------|------------|
| JSON | `.json` |
| YAML | `.yaml`, `.yml` |
| XML | `.xml` |

---

## Supported OSCAL Models

- Catalog (control definitions)
- Profile (baselines)
- SSP (System Security Plan)
- SAP (Assessment Plan)
- SAR (Assessment Results)
- POA&M (Plan of Action & Milestones)
- Component Definition

---

## Supported Frameworks

- NIST 800-53 Rev 5
- NIST CSF 2.0
- ISO 27001:2022
- CIS Controls v8
- PCI-DSS 4.0
- HIPAA
- SOC 2
- CMMC 2.0

---

## Tips

1. Upload actual OSCAL files, don't describe them
2. Specify the framework and baseline you're using
3. Request specific output formats (JSON, table, Markdown)
4. Combine skills for complex analysis
5. Ask follow-up questions to drill deeper

---

## Links

- [README](README.md) — Full documentation
- [Usage Guide](USAGE_GUIDE.md) — Detailed examples
- [Architecture](ARCHITECTURE.md) — How skills work
- [Skills Folder](skills/) — All skill definitions
- [Examples](examples/) — Sample OSCAL files
