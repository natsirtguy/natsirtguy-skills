# Agent SOP Format Specification

Complete reference for the Agent SOP format standard.

## Table of Contents

1. [File Naming](#file-naming)
2. [Required Sections](#required-sections)
3. [Parameters](#parameters)
4. [Steps and Constraints](#steps-and-constraints)
5. [RFC 2119 Keywords](#rfc-2119-keywords)
6. [Conditional Logic](#conditional-logic)
7. [Interactive SOPs](#interactive-sops)
8. [Best Practices](#best-practices)

## File Naming

- All SOP files MUST use the `.sop.md` file extension
- File names SHOULD use kebab-case (e.g., `code-assist.sop.md`)
- Names SHOULD be descriptive of the SOP's purpose

## Required Sections

Every SOP MUST include:

### Title and Overview

```markdown
# [SOP Name]

## Overview

[Concise description of what the SOP does and when to use it]
```

### Parameters

```markdown
## Parameters

- **required_param** (required): Description of the required parameter
- **optional_param** (optional): Description of optional parameter
- **param_with_default** (optional, default: "value"): Description
```

### Steps

```markdown
## Steps

### 1. [Step Name]

[Natural language description]

**Constraints:**
- You MUST [requirement]
- You SHOULD [recommendation]
- You MAY [optional behavior]
```

## Parameters

### Naming Rules

Parameter names MUST:
- Use lowercase letters only
- Use underscores for spaces (snake_case)
- Be descriptive of their purpose

### Parameter Types

```markdown
- **task_description** (required): Main input description
- **output_format** (optional, default: "markdown"): Format for output
- **max_retries** (optional, default: 3): Number of retry attempts
```

### Parameter Acquisition Constraints

For parameters with flexible input methods:

```markdown
**Constraints for parameter acquisition:**
- You MUST ask for all required parameters upfront in a single prompt
- You MUST support multiple input methods:
  - Direct input: Text provided in conversation
  - File path: Path to a local file
  - URL: Link to a resource
- You MUST confirm successful acquisition before proceeding
- You SHOULD save acquired data to a consistent location
```

## Steps and Constraints

### Step Structure

```markdown
### N. [Step Name]

[Natural language description of what happens in this step]

**Constraints:**
- You MUST [specific requirement]
- You SHOULD [recommended behavior]
- You MAY [optional behavior]
- You MUST NOT [prohibition] because [reason]
```

### Constraint Guidelines

1. Each step SHOULD have a **Constraints:** section
2. Use RFC 2119 keywords for clarity
3. Negative constraints MUST include reasoning
4. Order constraints by importance (MUST before SHOULD before MAY)

## RFC 2119 Keywords

Keywords as defined in RFC 2119:

| Keyword | Synonyms | Meaning |
|---------|----------|---------|
| MUST | REQUIRED, SHALL | Absolute requirement |
| MUST NOT | SHALL NOT | Absolute prohibition |
| SHOULD | RECOMMENDED | Valid reasons may exist to ignore, but understand implications |
| SHOULD NOT | NOT RECOMMENDED | Valid reasons may exist when acceptable, but understand implications |
| MAY | OPTIONAL | Truly optional item |

### Negative Constraint Format

Always provide context for prohibitions:

```markdown
- You MUST NOT [action] because [reason/consequence]
- You SHOULD NEVER [action] since [explanation]
- You SHALL NOT [action] as [technical limitation or risk]
```

Common contexts:
- Technical limitations: "because the system cannot handle..."
- Security risks: "since this could expose sensitive data..."
- Data integrity: "as this could corrupt or lose information..."
- User experience: "because users will be confused by..."
- Workflow disruption: "because this interferes with processes..."

## Conditional Logic

For steps with conditional behavior:

```markdown
### N. [Conditional Step]

If [condition], proceed with [specific action]. Otherwise, [alternative action].

**Constraints:**
- You MUST check [condition] before proceeding
- If [condition] is true, You MUST [action A]
- If [condition] is false, You MUST [action B]
```

## Interactive SOPs

For SOPs requiring user interaction:

```markdown
### N. [Interactive Step]

Guide the user through questions to gather requirements.

**Constraints:**
- You MUST ask one question at a time
- You MUST append each Q&A to "[filename].md"
- You SHOULD adapt follow-up questions based on answers
- You MUST continue until sufficient detail gathered
```

Interactive elements SHOULD:
1. Clearly indicate when user interaction expected
2. Specify how to handle user responses
3. Specify where to save interaction records

## Best Practices

1. **Keep steps focused** - One main action per step
2. **Use clear constraints** - Specific and actionable
3. **Include examples** - Show input/output pairs for complex operations
4. **Use natural language** - Easy to understand descriptions
5. **Minimize complexity** - Avoid deeply nested conditional logic
6. **Specify file paths** - Name all artifacts created
7. **Add troubleshooting** - Cover common issues and resolutions
8. **Test thoroughly** - Validate SOPs work as intended
9. **Order parameters** - Required before optional
10. **Explain prohibitions** - Always give reasons for MUST NOT
