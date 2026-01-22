# AI Review PR Rules

Configuration files for AI-powered PR review system. These rules define how exercises are evaluated and what students need to submit.

## Structure

```
configs/
├── schemas/                    # JSON schemas for validation
│   ├── course.schema.json
│   └── exercise.schema.json
└── java/
    └── selenium-testng-maven-course/
        ├── course.yaml         # Course-level rules (shared)
        ├── ex1.1-maven-webdriver-setup/
        ├── ex1.2-locator-strategies/
        ├── ex1.3-element-interactions/
        ├── ex1.4-wait-strategies/
        ├── ex2.1-testng-framework-basics/
        ├── ex2.2-testng-xml-config/
        └── ex2.3-page-object-model/
```

## Course Config (`course.yaml`)

Defines shared rules for all exercises:

- `quick_rules` - Regex patterns for quick code checks
- `pr_quality_rules` - PR title, description, and image validation
- `ai_instructions_template` - AI prompt template
- `checklist` - Default checklist items

## Exercise Config (`exercise.yaml`)

Each exercise has:

- `requirements` - What students must implement
- `checklist` - Evaluation criteria with weights
- `additional_rules` - Exercise-specific regex rules
- `pr_expectations` - PR title/description format
- `ai_instructions_override` - Exercise-specific scoring guide

## Adding New Exercise

1. Create directory: `configs/{language}/{course}/ex{number}-{name}/`
2. Create `exercise.yaml` with:

```yaml
metadata:
  id: "{language}-{course}-ex{number}"
  name: "Exercise {number}: {Name}"
  exercise: {number}
  inherits: "../../../course.yaml"

requirements:
  description: |
    What this exercise is about.

  must_have:
    - "Required item 1"
    - "Required item 2"

  nice_to_have:
    - "Optional item 1"

checklist:
  - item: "Checklist item"
    category: "selenium"
    weight: 10

additional_rules:
  - id: "rule_id"
    pattern: "regex_pattern"
    message: "Error message"
    severity: "error"
    category: "selenium"

pr_expectations:
  title_format: "ex{number}: {description}"
  title_examples:
    - "ex{number}: Example title"
  description_template: |
    ## Summary
    Brief description

    ## What's done
    - [x] Item 1
    - [x] Item 2

  screenshots_required: true

ai_instructions_override: |
  Review Exercise {number}:
  1. Criteria 1 (25 points)
  2. Criteria 2 (25 points)
  3. Criteria 3 (25 points)
  4. Criteria 4 (25 points)

  Score: 0-100
```

## PR Quality Rules

The system automatically checks:

### Title
- Min/max length
- Format: `ex1.1: Brief description`
- No vague words: "wip", "fix", "update", "changes"

### Description
- Has summary section
- Has checklist with `- [x]` format
- Contains relevant keywords

### Images
- Screenshots required for exercises 1.3+
- Preferred formats: png, jpg, gif

## License

MIT
