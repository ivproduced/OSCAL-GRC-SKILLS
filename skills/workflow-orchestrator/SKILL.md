---
name: workflow-orchestrator
description: Orchestrate complex multi-step OSCAL compliance workflows by combining multiple skills. Use this skill for end-to-end compliance automation like FedRAMP package reviews, continuous monitoring, and gap assessments.
---

# Workflow Orchestrator Skill

Orchestrate complex, multi-step compliance workflows that combine multiple skills for comprehensive OSCAL processing and analysis.

## When to Use This Skill

Use this skill when you need to:
- Perform end-to-end compliance assessments
- Chain multiple analysis steps together
- Automate repetitive compliance workflows
- Execute continuous monitoring checks
- Process compliance packages comprehensively

---

## ⛔ Authoritative Data Requirement

Workflows operate on **user-provided documents** and chain other skills together.

### Required Documents Per Workflow
| Workflow | Required Documents |
|----------|-------------------|
| FedRAMP Review | SSP, POA&M, Baseline Profile |
| Gap Analysis | Baseline Catalog + SSP |
| Continuous Monitoring | Current SSP, Previous SSP, POA&M |
| SSP Review | SSP + Baseline Profile |
| Multi-Framework Mapping | Source catalog + Target mapping document |

### Inherited Requirements
Each skill invoked in a workflow inherits its own authoritative data requirements. If a workflow step needs a baseline catalog, the workflow will stop and request it.

---

## Available Workflows

| Workflow | Purpose | Skills Used |
|----------|---------|-------------|
| FedRAMP Review | Review authorization package | Parser, Validator, Extractor, Risk Assessor |
| Gap Analysis | Identify missing controls | Parser, Extractor, Mapper, Report Generator |
| Continuous Monitoring | Regular compliance check | Parser, Validator, Risk Assessor, Report Generator |
| SSP Review | Validate SSP completeness | Parser, Validator, Extractor, Evidence Collector |
| Multi-Framework Mapping | Map across standards | Parser, Extractor, Mapper, Report Generator |

## Workflow Components

### Tasks
Individual steps that execute a skill:
```yaml
task:
  id: parse-ssp
  name: Parse SSP Document
  skill: oscal-parser
  parameters:
    file: fedramp_ssp.json
  depends_on: []
```

### Dependencies
Tasks can depend on other tasks:
```yaml
task:
  id: extract-controls
  name: Extract Controls
  skill: controls-extractor
  depends_on:
    - parse-ssp  # Must complete first
```

### Artifacts
Outputs passed between tasks:
```yaml
artifacts:
  - name: parsed_data
    from: parse-ssp
    to: extract-controls
```

## Predefined Workflows

### FedRAMP Package Review

**Purpose:** Comprehensive review of FedRAMP authorization package

**Steps:**
1. **Parse Documents** - Parse SSP, SAR, POA&M
2. **Validate Structure** - Check all documents for validity
3. **Extract Controls** - Get all control implementations
4. **Check Completeness** - Verify all baseline controls addressed
5. **Assess Risks** - Identify and score risks
6. **Generate Report** - Create review findings

**Output:**
```
FEDRAMP PACKAGE REVIEW
======================
System: [Name]
Baseline: [Moderate]
Review Date: [Date]

Document Validation:
- SSP: ✅ Valid
- SAR: ✅ Valid
- POA&M: ⚠️ 2 issues

Control Coverage:
- Required: 325
- Documented: 320 (98.5%)
- Missing: 5

Risk Summary:
- High Risks: 3
- Moderate Risks: 8
- POA&M Items: 15

Recommendation: [READY / NOT READY]
```

### Gap Analysis Workflow

**Purpose:** Identify compliance gaps against a framework

**Steps:**
1. **Parse Current State** - Parse existing SSP/documentation
2. **Extract Implemented Controls** - Get what's implemented
3. **Load Target Baseline** - Get required controls
4. **Compare** - Find differences
5. **Map to Other Frameworks** - Cross-reference if needed
6. **Generate Gap Report** - Document findings

**Output:**
```
GAP ANALYSIS REPORT
==================
Current: NIST 800-53 Low
Target: NIST 800-53 Moderate

New Controls Required: 125
Already Implemented: 200
Estimated Effort: 480 hours

Priority Gaps:
1. SI-4 - Security Monitoring (HIGH)
2. CA-7 - Continuous Monitoring (HIGH)
3. IR-4 - Incident Handling (MEDIUM)
```

### Continuous Monitoring Workflow

**Purpose:** Regular automated compliance check

**Steps:**
1. **Parse Latest Documents** - Get current state
2. **Validate All Documents** - Check for issues
3. **Check for Changes** - Compare to baseline
4. **Assess New Risks** - Score any changes
5. **Update POA&M** - Track any issues
6. **Generate Status Report** - Monthly report

**Frequency:** Daily/Weekly/Monthly

## How to Execute Workflows

### Step 1: Select Workflow
Choose appropriate workflow for the task.

### Step 2: Gather Inputs
Collect required documents:
- OSCAL files (SSP, SAR, POA&M, etc.)
- Baseline/profile references
- Configuration parameters

### Step 3: Execute Tasks
Run each task in dependency order:
1. Check dependencies are satisfied
2. Execute the skill
3. Collect outputs/artifacts
4. Pass to dependent tasks

### Step 4: Handle Errors
If a task fails:
- Log the error
- Determine if workflow can continue
- Skip dependent tasks if needed
- Include in final report

### Step 5: Compile Results
Aggregate outputs from all tasks into comprehensive report.

## Custom Workflow Definition

Create custom workflows:

```yaml
workflow:
  id: custom-review
  name: Quarterly Compliance Review
  description: Q4 compliance status assessment
  
  tasks:
    - id: parse-ssp
      skill: oscal-parser
      params:
        file: current_ssp.json
    
    - id: validate
      skill: oscal-validator
      depends_on: [parse-ssp]
    
    - id: extract
      skill: controls-extractor
      depends_on: [parse-ssp]
    
    - id: assess-risk
      skill: risk-assessor
      depends_on: [extract]
    
    - id: report
      skill: compliance-report-generator
      depends_on: [validate, extract, assess-risk]
      params:
        format: markdown
        type: executive-summary

  output:
    format: markdown
    destination: reports/q4-review.md
```

## Workflow Status Tracking

| Status | Meaning |
|--------|---------|
| Pending | Not started |
| Running | In progress |
| Completed | Successfully finished |
| Failed | Error encountered |
| Cancelled | Manually stopped |

## Example Usage

When asked "Review this FedRAMP package for readiness":

1. Initialize FedRAMP Review workflow
2. Parse all provided documents (SSP, SAR, POA&M)
3. Validate each document structure
4. Extract and count controls
5. Compare against FedRAMP Moderate baseline
6. Identify gaps and risks
7. Score overall readiness
8. Generate comprehensive review report
9. Provide go/no-go recommendation
