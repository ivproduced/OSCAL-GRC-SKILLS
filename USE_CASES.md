# OSCAL GRC Skills — Use Cases

Practical scenarios for building AI agents that automate cybersecurity compliance using OSCAL GRC Skills.

---

## ⛔ Critical: Authoritative Data Only

**All use cases require authoritative source documents.** AI agents using these skills must NEVER rely on training knowledge for compliance-critical information.

| Risk of Using Training Knowledge | Consequence |
|----------------------------------|-------------|
| Failed audits | Auditors require evidence from authoritative sources |
| Security gaps | Incorrect control definitions leave systems vulnerable |
| Regulatory violations | Using stale/wrong data causes compliance failures |
| Legal liability | Organizations liable for misrepresenting compliance |

**See:** [AUTHORITATIVE_DATA_POLICY.md](AUTHORITATIVE_DATA_POLICY.md) for complete policy.

### Required Documents Per Use Case

| Use Case | Required Documents |
|----------|-------------------|
| FedRAMP Authorization | SSP, POA&M, FedRAMP Baseline Catalog |
| Continuous Monitoring | Current SSP, Previous SSP, POA&M |
| Multi-Framework Mapping | NIST Catalog + Official Mapping Documents |
| Gap Analysis | Baseline Profile + SSP |
| SSP Development | Baseline Catalog, Technology Stack Docs |
| Control Mapping | Authoritative Mapping Publications |

---

## Table of Contents

1. [FedRAMP Authorization Package](#1-fedramp-authorization-package)
2. [Continuous Compliance Monitoring](#2-continuous-compliance-monitoring)
3. [Multi-Framework Compliance Mapping](#3-multi-framework-compliance-mapping)
4. [POA&M Management & Remediation](#4-poam-management--remediation)
5. [Audit Preparation & Evidence Collection](#5-audit-preparation--evidence-collection)
6. [SSP Development Assistant](#6-ssp-development-assistant)
7. [Reusable Component Library](#7-reusable-component-library)
8. [Compliance Chatbot](#8-compliance-chatbot)
9. [Inherited Controls Analysis](#9-inherited-controls-analysis)
10. [Risk-Based Prioritization](#10-risk-based-prioritization)
11. [Compliance Dashboard Data](#11-compliance-dashboard-data)
12. [Policy-to-Control Traceability](#12-policy-to-control-traceability)

---

## 1. FedRAMP Authorization Package

### Scenario
Your organization is preparing for FedRAMP Moderate authorization. You need to validate your SSP, identify gaps against the baseline, and generate documentation for the 3PAO assessment.

### Agent Workflow

```
User uploads: SSP JSON, Component Definitions, POA&M

Agent uses:
├── oscal-parser          → Parse all uploaded documents
├── oscal-validator       → Check structural integrity
├── advanced-oscal-validator → Validate FedRAMP-specific requirements
├── controls-extractor    → List all implemented controls
├── control-mapper        → Compare against FedRAMP Moderate baseline
├── risk-assessor         → Identify gaps and assess risk levels
├── evidence-collector    → Generate evidence collection checklist
└── compliance-report-generator → Produce authorization package summary
```

### Example Prompts

**Initial Assessment:**
> "I'm uploading our FedRAMP SSP. Validate it against OSCAL 1.1.2 requirements and identify any structural issues that would cause problems during 3PAO review."

**Gap Analysis:**
> "Compare our implemented controls against the FedRAMP Moderate baseline. List any missing controls or incomplete implementations, sorted by risk level."

**Evidence Checklist:**
> "Based on our SSP, generate an evidence collection checklist for 3PAO assessment. Include artifact types, responsible parties, and suggested collection methods."

**Package Summary:**
> "Generate an executive summary of our FedRAMP authorization readiness, including control coverage percentage, high-risk gaps, and recommended remediation priorities."

### Expected Outputs
- Validation report with errors/warnings
- Gap analysis matrix (control ID, status, gap description, risk)
- Evidence collection plan with 400+ artifact requirements
- Executive readiness summary with go/no-go recommendation

---

## 2. Continuous Compliance Monitoring

### Scenario
You need to automate ongoing compliance monitoring for a system with an active ATO. The agent should detect drift, track POA&M progress, and generate monthly status reports.

### Agent Workflow

```
Scheduled inputs: Current SSP, Previous SSP, POA&M, Scan results

Agent uses:
├── oscal-parser          → Parse current and baseline documents
├── oscal-validator       → Validate document integrity
├── controls-extractor    → Extract control status from both versions
├── risk-assessor         → Compare and detect drift/degradation
├── compliance-report-generator → Generate monthly status report
└── oscal-visualizer      → Create trend charts and dashboards
```

### Example Prompts

**Drift Detection:**
> "Compare this month's SSP against last month's baseline. Identify any controls that have changed status, new vulnerabilities, or modified implementation statements."

**POA&M Progress:**
> "Analyze our POA&M and report on remediation progress. Which items are overdue? What's our closure rate? Are there any items that have been open more than 90 days?"

**Monthly Report:**
> "Generate our monthly continuous monitoring report including: control status summary, POA&M metrics, vulnerability trends, and any significant changes since last month."

**Trend Analysis:**
> "Create a 6-month trend visualization showing our control compliance percentage, open POA&M items, and risk score over time."

### Expected Outputs
- Drift detection report with specific changes highlighted
- POA&M dashboard with aging analysis
- Monthly ConMon report (FedRAMP format)
- Mermaid/ASCII trend charts

---

## 3. Multi-Framework Compliance Mapping

### Scenario
Your organization must comply with multiple frameworks (NIST 800-53, ISO 27001, SOC 2, PCI-DSS). You need to understand control overlap, identify gaps, and optimize your compliance program.

### Agent Workflow

```
User uploads: Current SSP or control inventory

Agent uses:
├── oscal-catalog-provider → Fetch NIST 800-53 Rev 5 catalog from official sources
├── oscal-parser          → Parse control catalog and inventory
├── controls-extractor    → Extract all current controls
├── control-mapper        → Map to ISO 27001, SOC 2, PCI-DSS, CIS
├── risk-assessor         → Identify framework-specific gaps
└── compliance-report-generator → Generate unified compliance matrix
```

### Example Prompts

**Cross-Framework Mapping:**
> "Map our NIST 800-53 controls to ISO 27001:2022 requirements. Show me which NIST controls satisfy ISO requirements and where we have gaps."

**Unified Matrix:**
> "Create a unified control matrix showing how each of our controls maps to NIST 800-53, ISO 27001, SOC 2, and PCI-DSS. Include coverage percentages for each framework."

**Gap Prioritization:**
> "We need to achieve ISO 27001 certification. Based on our current NIST 800-53 implementation, what additional controls or modifications do we need? Prioritize by effort and impact."

**Efficiency Analysis:**
> "Identify controls that satisfy requirements across multiple frameworks. Which 20 controls give us the most cross-framework coverage?"

### Expected Outputs
- Framework mapping table with confidence scores
- Unified compliance matrix (exportable)
- Gap analysis with prioritized remediation roadmap
- "Bang for buck" control recommendations

---

## 4. POA&M Management & Remediation

### Scenario
Your security team needs to manage Plan of Action & Milestones (POA&M) items efficiently — creating new items from scan results, tracking remediation, and ensuring nothing falls through the cracks.

### Agent Workflow

```
User uploads: Vulnerability scan results, Current POA&M, SSP

Agent uses:
├── oscal-parser          → Parse POA&M and scan results
├── controls-extractor    → Map vulnerabilities to affected controls
├── risk-assessor         → Score and prioritize findings
├── control-implementation-generator → Suggest remediation steps
└── compliance-report-generator → Generate POA&M updates
```

### Example Prompts

**Create POA&M Items:**
> "I'm uploading our Nessus scan results. Create POA&M items for all High and Critical findings, mapping each to the affected NIST 800-53 controls with realistic remediation milestones."

**Remediation Guidance:**
> "For POA&M item V-2024-0142 (missing MFA on admin accounts), generate detailed remediation steps for our Azure environment, including Azure AD configuration changes."

**Risk Prioritization:**
> "Analyze our POA&M and recommend which items to remediate first based on: exploitability, asset criticality, level of effort, and days overdue."

**Status Report:**
> "Generate a POA&M status report for leadership showing: items by status, aging analysis, closure trends, and projected completion dates for open items."

### Expected Outputs
- Auto-generated POA&M items in OSCAL format
- Step-by-step remediation playbooks
- Risk-prioritized remediation queue
- Executive POA&M dashboard

---

## 5. Audit Preparation & Evidence Collection

### Scenario
A 3PAO assessment or internal audit is approaching. You need to prepare evidence packages, ensure documentation is complete, and brief stakeholders on what to expect.

### Agent Workflow

```
User uploads: SSP, SAP (if available), Previous SAR

Agent uses:
├── oscal-parser          → Parse authorization documents
├── controls-extractor    → List controls in scope for assessment
├── evidence-collector    → Generate evidence requirements per control
├── control-implementation-generator → Prepare interview talking points
└── compliance-report-generator → Generate pre-audit readiness report
```

### Example Prompts

**Evidence Inventory:**
> "Based on our SSP, generate a complete evidence collection matrix. For each control, list: required evidence types, suggested artifacts, responsible team, and collection deadline."

**Interview Prep:**
> "The auditors will interview our system administrators about access control (AC family). Generate talking points for each AC control, highlighting our implementation and evidence."

**Document Checklist:**
> "Create a pre-audit document checklist covering: policies, procedures, system documentation, configuration evidence, and training records. Flag any documents more than 12 months old."

**Readiness Assessment:**
> "Assess our audit readiness. Based on our current documentation, identify controls with weak or missing evidence and estimate our likelihood of findings."

### Expected Outputs
- Evidence collection matrix (400+ items for FedRAMP)
- Control-by-control interview guides
- Document freshness report
- Audit readiness scorecard with risk areas

---

## 6. SSP Development Assistant

### Scenario
You're developing a new System Security Plan from scratch or updating an existing one. You need help writing implementation narratives, ensuring completeness, and maintaining OSCAL compliance.

### Agent Workflow

```
User provides: System description, technology stack, baseline profile

Agent uses:
├── oscal-parser          → Parse baseline profile
├── controls-extractor    → Get required controls
├── control-implementation-generator → Write narratives
├── oscal-validator       → Validate SSP structure
├── component-definition-builder → Create reusable components
└── oscal-text-converter  → Generate human-readable versions
```

### Example Prompts

**Generate Narratives:**
> "Our system runs on AWS (EC2, RDS, S3) with Azure AD for authentication. Generate implementation narratives for the Access Control (AC) family controls at FedRAMP Moderate."

**Inheritance Analysis:**
> "We're using AWS GovCloud. Identify which controls are fully inherited from AWS, which are shared responsibility, and which are customer-implemented."

**Section Drafting:**
> "Draft the System Description section of our SSP including: system purpose, authorization boundary, data types, user roles, and interconnections."

**Completeness Check:**
> "Review our draft SSP and identify any controls with incomplete or missing implementation statements. Suggest boilerplate language where appropriate."

### Expected Outputs
- OSCAL-formatted implementation statements
- Inheritance/responsibility matrix
- Complete SSP sections in OSCAL and human-readable format
- Gap report with suggested remediation

---

## 7. Reusable Component Library

### Scenario
Your organization uses common platforms (AWS, Azure, Okta, Splunk) across multiple systems. You want to create reusable OSCAL component definitions to accelerate SSP development.

### Agent Workflow

```
User provides: Platform/service name, baseline, responsibility model

Agent uses:
├── control-mapper        → Identify applicable controls
├── control-implementation-generator → Write component narratives
├── component-definition-builder → Generate OSCAL component definition
├── oscal-validator       → Validate component structure
└── oscal-parser          → Parse for integration testing
```

### Example Prompts

**Create Component:**
> "Create an OSCAL component definition for Okta (Identity Provider). Include implementation statements for all identity-related controls at FedRAMP Moderate, marking each as 'implemented' or 'shared'."

**AWS Service Component:**
> "Generate a component definition for AWS S3 covering data protection controls (SC family). Include AWS-specific configuration requirements and customer responsibilities."

**Component Library:**
> "We use: AWS GovCloud, Azure AD, Splunk, CrowdStrike, and Tenable. Generate component definitions for each that we can import into future SSPs."

**Inheritance Mapping:**
> "Our new system will inherit controls from these existing components: [AWS-GovCloud, Okta, Splunk]. Show me which controls are covered and which I still need to implement."

### Expected Outputs
- OSCAL component-definition JSON files
- Control coverage matrix per component
- Component integration guide
- Inheritance calculator

---

## 8. Compliance Chatbot

### Scenario
You want to build an internal chatbot that helps engineers and compliance staff answer questions about your security program, controls, and compliance status.

### Agent Workflow

```
Context: SSP, Policies, POA&M loaded into agent context

Agent uses:
├── oscal-parser          → Parse all compliance documents
├── controls-extractor    → Enable control lookups
├── oscal-text-converter  → Generate plain-language responses
├── control-mapper        → Answer framework questions
└── risk-assessor         → Provide risk context
```

### Example Prompts (End Users Ask)

**Control Lookup:**
> "What does AC-2 require and how do we implement it?"

**Policy Question:**
> "What's our password policy? How often do we require password changes?"

**Responsibility Question:**
> "I'm configuring a new EC2 instance. What security controls am I responsible for implementing?"

**Status Question:**
> "Are we compliant with PCI-DSS requirement 8.3 (MFA)? What's our current status?"

**Remediation Question:**
> "We got a finding for missing encryption at rest. What do I need to do to fix it?"

### Implementation Notes
- Load SSP and policies into agent context at session start
- Use `oscal-text-converter` to make responses accessible
- Link to specific control IDs for traceability
- Include caveats about authoritative sources

---

## 9. Inherited Controls Analysis

### Scenario
Your system leverages cloud services and shared platforms. You need to accurately document inherited controls, validate provider responsibility claims, and identify your customer responsibilities.

### Agent Workflow

```
User uploads: CSP CRM/SSP, Platform component definitions, Your SSP

Agent uses:
├── oscal-parser          → Parse all documents
├── controls-extractor    → Extract provider implementations
├── control-mapper        → Match to your required controls
├── risk-assessor         → Identify gaps in inheritance claims
└── compliance-report-generator → Generate inheritance matrix
```

### Example Prompts

**Inheritance Analysis:**
> "I'm uploading AWS's FedRAMP CRM. Cross-reference with FedRAMP Moderate and tell me exactly which controls are fully inherited, partially inherited, and not covered."

**Gap Identification:**
> "For partially inherited controls, identify the specific customer responsibilities we need to implement. Generate implementation requirements for each."

**Validate Claims:**
> "Our SSP claims AC-2 is inherited from Okta. Validate this claim — does Okta's component definition actually cover all AC-2 requirements?"

**Stacking Analysis:**
> "Our system uses AWS (IaaS), Salesforce (SaaS), and Okta (IDaaS). Analyze the control inheritance stack and show me the final customer responsibility for each control."

### Expected Outputs
- Customer Responsibility Matrix (CRM)
- Inheritance validation report
- Customer implementation requirements
- Multi-layer inheritance diagram

---

## 10. Risk-Based Prioritization

### Scenario
You have limited resources and need to prioritize security investments. The agent should help identify the highest-risk gaps and recommend where to focus remediation efforts.

### Agent Workflow

```
User uploads: SSP, POA&M, Vulnerability scans, Asset inventory

Agent uses:
├── oscal-parser          → Parse all documents
├── controls-extractor    → Identify control coverage
├── risk-assessor         → Calculate risk scores
├── control-mapper        → Assess multi-framework impact
└── compliance-report-generator → Generate prioritized roadmap
```

### Example Prompts

**Risk Scoring:**
> "Analyze our control gaps and score each by risk level considering: data sensitivity, threat likelihood, existing mitigations, and regulatory impact."

**Prioritization:**
> "We have budget for 5 security projects this quarter. Based on our current gaps and risks, which 5 initiatives would reduce our risk profile the most?"

**Cost-Benefit Analysis:**
> "For our top 10 control gaps, estimate the implementation effort (low/medium/high) and risk reduction. Recommend which to tackle first."

**Attack Path Analysis:**
> "Based on our control gaps, identify potential attack paths an adversary could exploit. Which gaps are most critical to close?"

### Expected Outputs
- Risk-scored gap inventory
- Prioritized remediation roadmap
- Cost-benefit matrix
- Attack path diagram with mitigation recommendations

---

## 11. Compliance Dashboard Data

### Scenario
You're building a compliance dashboard for leadership and need structured data about control status, risk metrics, and trends over time.

### Agent Workflow

```
User uploads: SSP, POA&M, Historical snapshots

Agent uses:
├── oscal-parser          → Parse all documents
├── controls-extractor    → Get control counts and status
├── risk-assessor         → Calculate aggregate metrics
├── oscal-visualizer      → Generate chart data
└── compliance-report-generator → Structure for dashboard consumption
```

### Example Prompts

**Dashboard Metrics:**
> "Extract the following metrics from our SSP: total controls, implemented, partially implemented, planned, not applicable. Include breakdown by control family."

**JSON Export:**
> "Generate a JSON data structure suitable for a dashboard showing: control compliance by family, POA&M aging, and risk score distribution."

**Trend Data:**
> "I'm uploading SSP snapshots from the last 6 months. Generate trend data showing compliance percentage and open findings over time."

**Executive Summary:**
> "Generate executive dashboard talking points: overall compliance posture, top 3 risks, POA&M health, and comparison to last quarter."

### Expected Outputs
- Structured JSON for dashboard APIs
- Control family breakdown charts
- Trend datasets (CSV or JSON)
- Executive summary bullets

---

## 12. Policy-to-Control Traceability

### Scenario
Auditors want to see traceability from high-level policies through controls to specific implementations. You need to demonstrate this mapping clearly.

### Agent Workflow

```
User uploads: Security policies, SSP, Control catalog

Agent uses:
├── oscal-parser          → Parse all documents
├── oscal-text-converter  → Extract policy requirements
├── controls-extractor    → Map controls to policy sections
├── control-mapper        → Build traceability matrix
└── compliance-report-generator → Generate traceability report
```

### Example Prompts

**Policy Mapping:**
> "I'm uploading our Access Control Policy. Map each policy statement to the specific NIST 800-53 controls that implement it."

**Traceability Matrix:**
> "Create a traceability matrix showing: Policy → Control → Implementation → Evidence. Start with our Data Protection policies."

**Gap Analysis:**
> "Identify any policy requirements that don't have corresponding control implementations. Also identify any controls not tied to policy."

**Audit Evidence:**
> "Generate a traceability report for auditors showing how our policies are implemented through controls, with links to evidence for each."

### Expected Outputs
- Policy-to-control mapping table
- Full traceability matrix
- Gap report (policy vs. implementation)
- Auditor-ready traceability documentation

---

## Building Your Agent

### Architecture Pattern

```
┌─────────────────────────────────────────────────────────────────┐
│                        Your AI Agent                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌─────────────┐   ┌─────────────┐   ┌─────────────┐          │
│  │   Claude    │   │   OpenAI    │   │   Other     │          │
│  │   API       │   │   API       │   │   LLM       │          │
│  └──────┬──────┘   └──────┬──────┘   └──────┬──────┘          │
│         │                 │                 │                  │
│         └─────────────────┼─────────────────┘                  │
│                           │                                    │
│                           ▼                                    │
│         ┌─────────────────────────────────────┐                │
│         │         OSCAL GRC Skills            │                │
│         │                                     │                │
│         │  Load SKILL.md files into system    │                │
│         │  prompt or context window           │                │
│         └─────────────────────────────────────┘                │
│                           │                                    │
│                           ▼                                    │
│         ┌─────────────────────────────────────┐                │
│         │         OSCAL Documents             │                │
│         │                                     │                │
│         │  SSP, POA&M, Catalogs, Components   │                │
│         └─────────────────────────────────────┘                │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### Implementation Tips

1. **Load relevant skills** — Don't load all 14 skills; choose those needed for your use case
2. **Provide OSCAL context** — Upload or inject relevant OSCAL documents into context
3. **Use structured outputs** — Request JSON when you need machine-readable data
4. **Chain requests** — Complex workflows may need multiple agent turns
5. **Validate outputs** — Use `oscal-validator` skill to verify generated OSCAL
6. **⛔ Enforce data policy** — Never allow the agent to use training knowledge for compliance data

### Critical: Include Data Policy in System Prompt

Add this to your agent's system prompt to prevent hallucination:

```
CRITICAL RULE: Never use training knowledge for compliance data.

For any task requiring control definitions, framework mappings, or 
compliance requirements, you MUST have the authoritative source document.

If the required document is not provided:
1. State what document you need
2. Provide the official download URL if known
3. Request the user upload or confirm fetch
4. DO NOT proceed with training data

This is non-negotiable for compliance work due to audit, security,
and legal risks.
```

### Example: Python Agent Skeleton

```python
from anthropic import Anthropic

# Load skills
def load_skill(skill_name: str) -> str:
    with open(f"skills/{skill_name}/SKILL.md", "r") as f:
        return f.read()

# Build system prompt with skills
skills_to_load = ["oscal-parser", "controls-extractor", "risk-assessor"]
system_prompt = "You are a compliance automation assistant.\n\n"
system_prompt += "You have access to these skills:\n\n"
for skill in skills_to_load:
    system_prompt += f"---\n{load_skill(skill)}\n---\n\n"

# Create agent
client = Anthropic()

def ask_agent(user_message: str, oscal_document: str = None) -> str:
    messages = []
    
    if oscal_document:
        messages.append({
            "role": "user",
            "content": f"OSCAL Document:\n```json\n{oscal_document}\n```\n\n{user_message}"
        })
    else:
        messages.append({"role": "user", "content": user_message})
    
    response = client.messages.create(
        model="claude-sonnet-4-20250514",
        max_tokens=8192,
        system=system_prompt,
        messages=messages
    )
    
    return response.content[0].text

# Use the agent
with open("my_ssp.json", "r") as f:
    ssp = f.read()

result = ask_agent(
    "Identify control gaps against FedRAMP Moderate and assess risk levels.",
    oscal_document=ssp
)
print(result)
```

---

## Next Steps

1. **Read the data policy** — Review [AUTHORITATIVE_DATA_POLICY.md](AUTHORITATIVE_DATA_POLICY.md) before building
2. **Pick a use case** — Start with one scenario that matches your immediate needs
3. **Load the skills** — Upload relevant `SKILL.md` files to Claude or include in your agent
4. **Test with sample data** — Use files from `examples/` to validate the workflow
5. **Customize** — Modify skills to match your organization's specific requirements
6. **Integrate** — Build the agent into your existing tools and workflows

---

## Resources

- [Skills Folder](skills/) — All 14 skill definitions
- [Authoritative Data Policy](AUTHORITATIVE_DATA_POLICY.md) — **Critical: Read first**
- [Examples](examples/) — Sample OSCAL files for testing
- [USAGE_GUIDE.md](USAGE_GUIDE.md) — How to use individual skills
- [ARCHITECTURE.md](ARCHITECTURE.md) — Understanding skill structure
- [Anthropic Agent Skills Spec](https://agentskills.io/) — Skills format reference
