# Contributing to OSCAL GRC Skills

Thank you for your interest in contributing! This project provides AI agent skills for OSCAL and cybersecurity compliance automation.

---

## Code of Conduct

This project follows our [Code of Conduct](CODE_OF_CONDUCT.md). By participating, you agree to uphold respectful and inclusive behavior.

---

## How to Contribute

### Reporting Issues

Found a bug or have a suggestion? [Open an issue](https://github.com/euCann/OSCAL-GRC-SKILLS/issues) with:

- Clear, descriptive title
- Steps to reproduce (for bugs)
- Expected vs actual behavior
- Skill name(s) affected
- Sample OSCAL input (if relevant)

### Suggesting New Skills

We welcome ideas for new skills! Open an issue describing:

- What the skill would do
- Use cases it would address
- Which OSCAL models it would work with
- Example inputs and outputs

### Improving Existing Skills

Skills are markdown files — improvements are always welcome:

- Clearer instructions
- Better examples
- Additional output formats
- Expanded framework coverage
- Bug fixes in logic/instructions

---

## Development Setup

1. **Fork and clone the repository**
   ```bash
   git clone https://github.com/euCann/OSCAL-GRC-SKILLS.git
   cd oscal-skills
   ```

2. **Create a branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```

3. **Make your changes**
   - Edit or create `SKILL.md` files in `skills/`
   - Update documentation as needed

4. **Test your changes**
   - Load the skill in Claude.ai or Claude Code
   - Test with sample OSCAL files from `examples/`
   - Verify the skill produces expected output

5. **Submit a pull request**
   - Describe what you changed and why
   - Include test results or screenshots if helpful

---

## Skill Format Guidelines

### File Structure

Each skill lives in its own folder:
```
skills/
└── your-skill-name/
    └── SKILL.md
```

### SKILL.md Template

```markdown
---
name: your-skill-name
description: One-line description of what the skill does
---

# Skill Title

## Purpose

Describe what this skill accomplishes and when to use it.

## Inputs

Describe what the skill expects:
- OSCAL document type(s)
- Format (JSON, YAML, XML)
- Any additional context needed

## Outputs

Describe what the skill produces:
- Output format(s)
- Structure of the response

## Instructions

Step-by-step instructions for the AI agent to follow.

1. First, do this...
2. Then, check for...
3. Finally, produce...

## Examples

### Example 1: [Scenario]

**Input:**
[Sample input]

**Output:**
[Expected output]
```

### Writing Good Instructions

- **Be specific** — Avoid ambiguous language
- **Use numbered steps** — Clear sequence of operations
- **Include examples** — Show expected inputs and outputs
- **Handle edge cases** — What if data is missing or malformed?
- **Define output format** — JSON schema, table structure, etc.

---

## Documentation Guidelines

- Use clear, concise language
- Include practical examples
- Link to related skills and resources
- Keep formatting consistent with existing docs

---

## Pull Request Checklist

Before submitting a PR, ensure:

- [ ] Skill follows the `SKILL.md` template format
- [ ] YAML frontmatter includes `name` and `description`
- [ ] Instructions are clear and testable
- [ ] Examples demonstrate expected behavior
- [ ] Tested with Claude.ai or Claude Code
- [ ] Documentation updated if needed
- [ ] CHANGELOG.md updated for significant changes

---

## Skill Categories

When adding skills, consider which category fits:

| Category | Purpose |
|----------|---------|
| **Parsing** | Read and convert OSCAL formats |
| **Validation** | Check structure and compliance |
| **Extraction** | Pull specific data from documents |
| **Analysis** | Risk assessment, gap analysis |
| **Mapping** | Cross-framework control mapping |
| **Generation** | Create reports, narratives, documents |
| **Visualization** | Diagrams, charts, visual outputs |
| **Orchestration** | Multi-skill workflows |

---

## Getting Help

- **Questions?** Open a [discussion](https://github.com/euCann/OSCAL-GRC-SKILLS/discussions)
- **Found a bug?** Open an [issue](https://github.com/euCann/OSCAL-GRC-SKILLS/issues)
- **Want to chat?** Join the OSCAL community

---

## Recognition

Contributors are recognized in:
- GitHub contributors list
- CHANGELOG.md for significant contributions
- README.md acknowledgments section

Thank you for helping make OSCAL compliance automation accessible to everyone!
