# Skill Schemas

This directory contains the shared JSON schemas used across skills.

## Schema Overview

| Schema | Purpose |
|--------|---------|
| `accessibility-report.json` | Output format for document accessibility analysis |
| `revision-request.json` | Input format for document revision requests |
| `cognitive-analysis.json` | Input format for cognitive accessibility analysis |
| `cognitive-report.json` | Output format for cognitive accessibility reports |

## Usage

### As a Reusable Schema Reference

These schemas can be referenced using `$ref` in other schemas:

```json
{
  "$ref": "schemas/accessibility-report.json"
}
```

### Validation

You can validate JSON files against these schemas using tools like:

- **Python**: `jsonschema` library
- **JavaScript**: `ajv` library
- **CLI**: `json-schema-cli` or `check-jsonschema`

Example validation command:
```bash
ajv validate -s schemas/accessibility-report.json -d your-report.json
```

## Schema Design Principles

1. **Strict typing** - Clear type definitions for all fields
2. **Descriptive metadata** - Descriptions explain purpose and format
3. **Enum constraints** - Fixed values prevent invalid data
4. **Version stability** - Using JSON Schema draft-07 for stability
5. **Self-contained** - Schemas reference only standard JSON Schema features