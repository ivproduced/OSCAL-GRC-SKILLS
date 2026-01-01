# OSCAL SSP Validator - Usage Scenarios

## Scenario 1: Basic SSP Validation

**Situation:** You've just finished drafting your SSP and want a comprehensive check before submission.

**Prompt:**
```
Validate this OSCAL SSP against NIST 800-18 and FedRAMP Moderate requirements:

[paste SSP JSON or provide file path]
```

**Expected Output:**
```json
{
  "validation_summary": {
    "total_checks": 47,
    "passed": 42,
    "failed": 3,
    "warnings": 2,
    "severity_breakdown": {
      "critical": 1,
      "high": 2,
      "medium": 2,
      "low": 0
    }
  },
  "findings": [
    {
      "id": "VAL-001",
      "category": "structural_completeness",
      "severity": "critical",
      "finding": "Missing security-impact-level in system-characteristics",
      "location": "system-characteristics",
      "requirement": "NIST 800-18 Section 13.3",
      "remediation": "Add security-impact-level with security-objective-confidentiality, security-objective-integrity, and security-objective-availability fields"
    }
  ]
}
```

## Scenario 2: Gap Analysis

**Situation:** You're preparing for FedRAMP submission and need to identify all gaps.

**Prompt:**
```
Perform a FedRAMP gap analysis on this SSP and show:
1. Missing required sections
2. Incomplete control implementations
3. Documentation quality issues
4. Priority for remediation

[SSP content]
```

**Expected Output:**
A prioritized remediation roadmap with:
- Critical gaps (blocks submission)
- High priority gaps (likely rejection)
- Medium priority improvements
- Low priority enhancements

## Scenario 3: Continuous Validation

**Situation:** Your SSP is living documentation updated regularly. You want quick validation during updates.

**Prompt:**
```
Quick validation check - focus on:
- New/modified controls since last validation
- Schema compliance
- FedRAMP-specific requirements

[SSP content]
```

**Expected Output:**
Fast check (< 30 seconds) highlighting only changed areas.

## Scenario 4: Specific Section Validation

**Situation:** You're working on the System Characteristics section and want focused feedback.

**Prompt:**
```
Validate only the system-characteristics section of this SSP:
- Information types and categorizations
- Security impact levels
- Authorization boundary
- System status

[system-characteristics section]
```

**Expected Output:**
Detailed analysis of just that section with specific NIST 800-18 references.

## Scenario 5: Control Implementation Quality

**Situation:** You want to ensure control implementations are detailed enough for FedRAMP.

**Prompt:**
```
Analyze control implementation quality for these controls:
- AC-2 (Account Management)
- IA-2 (Identification and Authentication)
- SC-7 (Boundary Protection)

Check for:
- Sufficient detail
- Evidence of implementation
- Customer responsibility statements
- Implementation status

[control-implementation section]
```

**Expected Output:**
Control-by-control assessment with quality scores and improvement suggestions.

## Scenario 6: Pre-Submission Checklist

**Situation:** Final check before submitting to FedRAMP PMO.

**Prompt:**
```
Perform pre-submission validation with FedRAMP checklist:
✓ All required sections present
✓ All Moderate baseline controls addressed
✓ Proper OSCAL schema compliance
✓ Metadata completeness
✓ No placeholder text
✓ Dates are current
✓ Contact information valid

[complete SSP]
```

**Expected Output:**
Go/No-Go recommendation with specific blockers if any.

## Scenario 7: Comparison with Baseline

**Situation:** You want to ensure your SSP covers all required controls from the baseline profile.

**Prompt:**
```
Compare this SSP against FedRAMP Moderate baseline:
- List missing controls
- Identify controls marked as "Inherited" without proper documentation
- Flag controls with insufficient implementation details

[SSP + baseline profile]
```

**Expected Output:**
Coverage matrix showing implemented vs. missing vs. insufficient controls.

## Scenario 8: Custom Rule Validation

**Situation:** Your organization has additional requirements beyond standard FedRAMP.

**Prompt:**
```
Validate this SSP with custom rules:
- All controls must have implementation status with dates
- Customer Responsibility Matrix must be included
- All components must have version numbers
- Diagrams must be referenced in boundary description

[SSP + custom rules]
```

**Expected Output:**
Standard validation + custom rule results.

## Example Files

### sample_ssp_basic.json
A minimal but valid OSCAL SSP demonstrating:
- Required metadata structure
- System characteristics
- Basic control implementations
- Component definitions
- User roles

**Use for:** Learning OSCAL structure, testing basic validation

### sample_ssp_invalid.json
An SSP with intentional errors:
- Missing required fields
- Invalid UUID formats
- Incomplete control implementations
- Schema violations

**Use for:** Testing validator's error detection, understanding common mistakes

### sample_ssp_fedramp_complete.json
A comprehensive SSP meeting all FedRAMP Moderate requirements:
- All required sections present
- 325+ control implementations
- Proper customer responsibility documentation
- Complete metadata and references

**Use for:** Reference implementation, submission preparation

## Testing the Skill

### Test 1: Schema Validation
```bash
# Should pass
claude validate sample_ssp_basic.json

# Should fail with specific errors
claude validate sample_ssp_invalid.json
```

### Test 2: FedRAMP Compliance
```bash
claude validate --baseline fedramp-moderate sample_ssp_complete.json
```

### Test 3: Batch Validation
```bash
claude validate --batch *.json --output validation_report.md
```

## Tips for Best Results

1. **Provide Context**: Mention your target baseline (FedRAMP Low/Moderate/High)
2. **Be Specific**: Focus on particular sections if you're making targeted updates
3. **Include Baselines**: Provide the profile you're implementing against
4. **Request Format**: Specify if you want JSON, Markdown, or CSV output
5. **Set Priorities**: Ask for critical issues first if you're on a timeline

## Common Questions

**Q: How long does validation take?**
A: Basic validation: 10-30 seconds. Comprehensive FedRAMP validation: 1-2 minutes.

**Q: Can I validate against custom baselines?**
A: Yes, provide your custom profile JSON along with the SSP.

**Q: Does it check for inherited controls?**
A: Yes, it validates that inherited controls are properly documented with source information.

**Q: Can I get validation in CI/CD?**
A: Yes, see the CI/CD integration example in the main SKILL.md.

**Q: What OSCAL versions are supported?**
A: Currently 1.0.0 through 1.0.4. Automatically detected from oscal-version field.

## Next Steps

After validation:
1. **Fix Critical Issues** - Address anything blocking submission
2. **Use oscal-poam-manager** - Convert findings to POA&Ms if needed
3. **Update Components** - Use oscal-component-generator for missing pieces
4. **Re-validate** - Ensure all issues resolved
5. **Submit** - You're ready for FedRAMP!
