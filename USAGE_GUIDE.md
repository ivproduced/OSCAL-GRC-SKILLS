# Usage Guide

This guide explains how to use OSCAL GRC Skills with Claude and other AI agents.

---

## Quick Start

### 1. Choose Your Skills

Each skill is a `SKILL.md` file that teaches Claude how to perform a specific compliance task:

| Skill | Best For |
|-------|----------|
| [oscal-parser](skills/oscal-parser/) | Reading OSCAL documents |
| [oscal-validator](skills/oscal-validator/) | Checking document structure |
| [controls-extractor](skills/controls-extractor/) | Getting control lists |
| [control-mapper](skills/control-mapper/) | Cross-framework mapping |
| [risk-assessor](skills/risk-assessor/) | Gap and risk analysis |
| [compliance-report-generator](skills/compliance-report-generator/) | Audit reports |
| [evidence-collector](skills/evidence-collector/) | Evidence tracking |
| [control-implementation-generator](skills/control-implementation-generator/) | Implementation narratives |
| [workflow-orchestrator](skills/workflow-orchestrator/) | Multi-step automation |

### 2. Load the Skill

**Option A: Upload directly to Claude.ai**
1. Open [claude.ai](https://claude.ai)
2. Click the attachment icon
3. Upload the `SKILL.md` file from the skill folder
4. Start asking questions

**Option B: Include in your prompt**
Copy the skill content into your system prompt or conversation.

**Option C: Use Claude Code plugin marketplace**
```
/plugin marketplace add ivproduced/OSCAL-GRC-SKILLS
```

### 3. Provide Your OSCAL Document

Upload or paste your OSCAL document (JSON, YAML, or XML format) and ask Claude to analyze it using the skill.

---

## Example Workflows

### Validate a FedRAMP SSP

1. Load the `oscal-validator` and `advanced-oscal-validator` skills
2. Upload your SSP JSON file
3. Ask: *"Validate this SSP against OSCAL 1.1.2 requirements and FedRAMP best practices"*

### Map Controls Between Frameworks

1. Load the `controls-extractor` and `control-mapper` skills
2. Upload your NIST 800-53 catalog or SSP
3. Ask: *"Map these controls to ISO 27001 requirements and show coverage gaps"*

### Generate Implementation Guidance

1. Load the `control-implementation-generator` skill
2. Specify the system type (cloud, on-prem, hybrid)
3. Ask: *"Generate implementation guidance for AC-2 (Account Management) for our AWS environment"*

### Create a Compliance Report

1. Load the `oscal-parser` and `compliance-report-generator` skills
2. Upload your SSP or assessment results
3. Ask: *"Generate an executive compliance summary for our FedRAMP Moderate authorization"*

### Assess Risks and Gaps

1. Load the `risk-assessor` skill
2. Upload your SSP and control baseline
3. Ask: *"Identify control gaps and assess risk levels for our system"*

---

## Combining Multiple Skills

Claude can use multiple skills together. Load several skill files and ask for complex workflows:

> "Use the parser to read this SSP, the validator to check it, the controls-extractor to list implemented controls, and the compliance-report-generator to create an audit summary."

Claude will chain the skills automatically.

---

## Skill Output Formats

Each skill produces structured output. Common formats include:

| Output Type | Description |
|-------------|-------------|
| **Summary** | Human-readable analysis |
| **Table** | Structured data (controls, mappings, gaps) |
| **JSON** | Machine-readable structured output |
| **Report** | Formatted document (Markdown) |
| **Diagram** | Mermaid/ASCII visualizations |

Request your preferred format in your prompt:
> "...and output the results as a JSON object"

---

## Tips for Best Results

1. **Be specific** — Include your system type, baseline, and framework when asking questions
2. **Provide context** — Upload the actual OSCAL files rather than describing them
3. **Chain skills** — Ask for multi-step analysis in one request
4. **Request formats** — Specify JSON, Markdown, or table output as needed
5. **Iterate** — Ask follow-up questions to drill deeper into findings

---

## Supported OSCAL Models

| Model | File Extension | Description |
|-------|----------------|-------------|
| Catalog | `*-catalog.json` | Control definitions (e.g., NIST 800-53) |
| Profile | `*-profile.json` | Baseline customizations |
| SSP | `*-ssp.json` | System Security Plans |
| SAP | `*-sap.json` | Security Assessment Plans |
| SAR | `*-sar.json` | Security Assessment Results |
| POA&M | `*-poam.json` | Plan of Action & Milestones |
| Component Definition | `*-component.json` | Reusable component controls |

---

## Troubleshooting

**Claude doesn't seem to understand the skill**
- Ensure the full `SKILL.md` content was uploaded or included
- Re-upload the skill file if the conversation is long

**Output is generic or incorrect**
- Provide the actual OSCAL file, not just a description
- Specify the OSCAL version (1.1.2) and model type

**Need more detail**
- Ask Claude to "expand on" or "provide more detail about" specific findings
- Request specific sections of the OSCAL document to analyze

---

## Next Steps

- Browse the [skills/](skills/) folder to see all available skills
- Check [examples/](examples/) for sample OSCAL files to test with
- Read individual `SKILL.md` files to understand each skill's capabilities
