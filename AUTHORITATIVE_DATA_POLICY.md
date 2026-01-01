# Authoritative Data Policy

## ⛔ Critical: Never Use Training Knowledge for Compliance

This project is designed for **real-world compliance and audit work**. AI agents using these skills must **never** rely on training data or "general knowledge" for compliance-critical information.

---

## Why This Matters

| Risk | Consequence |
|------|-------------|
| **Failed Audits** | Auditors require evidence from authoritative sources — not AI-generated assumptions |
| **Security Gaps** | Incorrect control definitions leave systems vulnerable |
| **Regulatory Violations** | Using stale/wrong data can cause compliance failures |
| **Legal Liability** | Organizations can be held liable for misrepresenting compliance status |
| **Loss of Certification** | FedRAMP, ISO, SOC 2 certifications can be revoked |

---

## The Golden Rule

> **If you don't have the authoritative source document, STOP and ask for it.**

---

## What Requires Authoritative Sources

### 1. Control Catalogs & Definitions
- **NIST 800-53 Rev 5** — Control IDs, statements, parameters, guidance
- **FedRAMP Baselines** — Which controls apply at HIGH/MODERATE/LOW
- **ISO 27001:2022** — Control objectives and requirements
- **CIS Controls v8** — Safeguard definitions
- **PCI-DSS v4.0** — Requirements and testing procedures
- **HIPAA** — Security Rule requirements

**✅ Correct:** Parse the official OSCAL catalog JSON from NIST/FedRAMP  
**⛔ Wrong:** Recall control text from training data

### 2. Framework Mappings
- **NIST → ISO** mappings
- **NIST → CIS** mappings
- **NIST → PCI-DSS** mappings
- Cross-framework equivalencies

**✅ Correct:** Use official mapping documents (NIST, CSA CCM, etc.)  
**⛔ Wrong:** Guess which controls are equivalent

### 3. Compliance Requirements
- Specific control parameters (password length, retention periods, etc.)
- Required documentation for certification
- Assessment procedures
- Evidence requirements

**✅ Correct:** Reference the official baseline profile or authorization guide  
**⛔ Wrong:** Make assumptions about what's required

---

## Authoritative Sources

### NIST OSCAL Content
```
https://github.com/usnistgov/oscal-content
```
- NIST 800-53 Rev 5 catalog (JSON, XML, YAML)
- NIST CSF profiles
- Official schema definitions

### FedRAMP Automation
```
https://github.com/GSA/fedramp-automation
```
- FedRAMP HIGH/MODERATE/LOW baselines
- Resolved profile catalogs
- FedRAMP-specific parameters

### Direct Download URLs (Raw GitHub)
```
# NIST 800-53 Rev 5
https://raw.githubusercontent.com/usnistgov/oscal-content/main/nist.gov/SP800-53/rev5/json/NIST_SP-800-53_rev5_catalog.json

# FedRAMP HIGH
https://raw.githubusercontent.com/GSA/fedramp-automation/master/dist/content/rev5/baselines/json/FedRAMP_rev5_HIGH-baseline-resolved-profile_catalog.json

# FedRAMP MODERATE
https://raw.githubusercontent.com/GSA/fedramp-automation/master/dist/content/rev5/baselines/json/FedRAMP_rev5_MODERATE-baseline-resolved-profile_catalog.json

# FedRAMP LOW
https://raw.githubusercontent.com/GSA/fedramp-automation/master/dist/content/rev5/baselines/json/FedRAMP_rev5_LOW-baseline-resolved-profile_catalog.json
```

---

## Decision Tree for Agents

```
┌─────────────────────────────────────────────────────────────┐
│ Task requires control definitions, mappings, or parameters │
└──────────────────────────────┬──────────────────────────────┘
                               │
                               ▼
              ┌────────────────────────────────┐
              │ Is authoritative source        │
              │ document provided or fetchable?│
              └───────────────┬────────────────┘
                              │
              ┌───────────────┴───────────────┐
              │                               │
              ▼                               ▼
          ┌───────┐                       ┌───────┐
          │  Yes  │                       │  No   │
          └───┬───┘                       └───┬───┘
              │                               │
              ▼                               ▼
   ┌──────────────────┐          ┌────────────────────────┐
   │ Use the document │          │ ⛔ STOP                 │
   │ to perform task  │          │                        │
   └──────────────────┘          │ Request user upload or │
                                 │ provide download URLs  │
                                 │                        │
                                 │ DO NOT proceed with    │
                                 │ training knowledge     │
                                 └────────────────────────┘
```

---

## What Agents CAN Do Without Authoritative Sources

These tasks rely on **methodology**, not control-specific data:

| Task | Why It's Safe |
|------|---------------|
| Parse OSCAL structure | Just reading what user provided |
| Validate OSCAL schema | Checking syntax, not requirements |
| Generate report templates | Format, not content |
| Calculate implementation percentages | Math on user's data |
| Identify missing fields | Structural analysis |
| Format output (JSON, Markdown, etc.) | Transformation, not interpretation |

---

## What Agents CANNOT Do Without Sources

These tasks require authoritative data:

| Task | Required Source |
|------|-----------------|
| List controls in FedRAMP Moderate | FedRAMP Moderate baseline catalog |
| Define what AC-2 requires | NIST 800-53 Rev 5 catalog |
| Map NIST to ISO 27001 | Official mapping document |
| State password requirements | Organization's policy or baseline profile |
| Determine evidence requirements | Assessment guide or baseline |
| Assess control gaps | Baseline catalog + user's SSP |

---

## How to Request Sources

When you need an authoritative source, use this template:

```
I cannot complete this task without the authoritative source document.

For [specific task], I need:
• [Document name] from [source]
• Download: [URL if known]

Please either:
1. Upload the document, or
2. Confirm you want me to fetch from the official URL

I will not proceed using training data because:
• Compliance work requires authoritative sources for audits
• My training data may be outdated or incomplete
• Incorrect control information creates security and legal risks
```

---

## Skill-Specific Requirements

### oscal-catalog-provider
- Provides URLs to fetch catalogs
- **Fallback:** Request user upload, never training data

### control-mapper
- Requires official mapping documents
- Example mappings are for format illustration only
- **Always state:** "These mappings require authoritative sources for production use"

### controls-extractor
- Works only on user-provided documents
- Cannot generate control lists from memory

### risk-assessor
- Scoring methodology is safe (it's a process)
- Control-specific requirements require source documents

### control-implementation-generator
- Templates and structure are safe
- Technology-specific implementation details require vendor documentation
- Control requirements require catalog

### compliance-report-generator
- Report format and structure are safe
- Metrics calculated from user's documents only
- Never generate compliance data from training knowledge

---

## Summary

| Situation | Action |
|-----------|--------|
| User provides OSCAL document | ✅ Analyze and process it |
| User asks for control definition | ⛔ Request catalog document |
| User asks for framework mapping | ⛔ Request mapping document |
| User asks about compliance requirements | ⛔ Request baseline/profile |
| User asks to validate structure | ✅ Safe — syntax checking |
| User asks to format output | ✅ Safe — transformation |

---

## Version History

| Version | Date | Change |
|---------|------|--------|
| 1.0.0 | 2025-12-31 | Initial authoritative data policy |
