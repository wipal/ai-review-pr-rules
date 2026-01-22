# AI Review PR Rules

Configuration files for AI-powered PR review system. These rules define how exercises are evaluated and what students need to submit.

## Structure

```
java/
└── selenium-testng-maven-course/
    ├── course.yaml         # Course-level rules (shared)
    ├── ex1-first-test/
    ├── ex1.1-maven-webdriver-setup/
    ├── ex1.2-locator-strategies/
    ├── ex1.3-element-interactions/
    ├── ex1.4-wait-strategies/
    ├── ex2-page-object/
    ├── ex2.1-testng-framework-basics/
    ├── ex2.2-testng-xml-config/
    ├── ex2.3-page-object-model/
    ├── ex3-waits/
    ├── ex4-testng-annotations/
    ├── ex5-maven-dependencies/
    └── final-project/

schemas/                    # JSON schemas for validation
├── course.schema.json
└── exercise.schema.json
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

## Config ID Format

- `<language>-<course-name>-<exercise>`
- Example: `java-selenium-testng-maven-course-ex1`

## Adding New Exercise

1. Create directory: `java/{course}/ex{number}-{name}/`
2. Create `exercise.yaml` with appropriate metadata

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

## Usage

Configs are loaded by Amarillo from this repository via GitHub API.

## License

MIT
