# Create Accessible Revision Skill

Use this skill when: You need to generate an improved, accessible version of a document.

## Role Definition

You are an expert document editor specializing in accessibility compliance. Your task is to create documents that meet WCAG 2.1 standards while preserving original content and intent.

## Input Modes

This skill supports **two input modes**:

### Mode A: Document Only (Automatic)
Provide a document without a pre-existing report. The skill will:
1. Automatically run accessibility analysis (see `analyze-accessibility` skill)
2. Generate the accessibility report internally
3. Apply all fixes to create the revised document
4. Output both the revised document and the analysis report

### Mode B: Document + Report
Provide both a document and an existing accessibility report. The skill will:
1. Review the provided report
2. Apply fixes based on identified issues
3. Output the revised document and a revision summary

## Workflow

### Step 1: Accept Input

You need:
1. **Original document** - The file to be revised
2. **Accessibility report** - (optional) JSON format with issues to fix

If no report is provided, proceed with Mode A (automatic analysis).

### Step 2: Analyze (Mode A Only)

If no accessibility report is provided, first perform accessibility analysis using these guidelines:

**Perceivable:**
- Are images provided with alternative text?
- Is there sufficient color contrast?
- Can content be presented in different ways?

**Operable:**
- Do all interactive elements have accessible names?
- Can the document be navigated via structure?
- Are links descriptive?

**Understandable:**
- Is the language properly identified?
- Are abbreviations and acronyms explained?

**Robust:**
- Is the document structure valid?
- Are styles used consistently?

Rate each issue: CRITICAL > MAJOR > MINOR > SUGGESTION

### Step 3: Plan the Revisions

For each issue, determine:
- What needs to change
- How to preserve original meaning
- Any dependencies between fixes

### Step 4: Apply Fixes

#### Images
- Add descriptive alt text
- Mark decorative images with empty alt
- Ensure complex images have extended descriptions

#### Structure
- Fix heading hierarchy (no skipped levels)
- Add proper list markup
- Ensure logical reading order

#### Links
- Replace "click here" with descriptive text
- Add context for links that need it

#### Tables
- Add header rows
- Include captions
- Ensure proper scope

#### Language
- Define abbreviations on first use
- Expand acronyms
- Simplify complex sentences

### Step 5: Generate Output

Output:

1. **Revised document** - In the same format as the original
2. **Revision Summary**:
```json
{
  "document": "filename.docx",
  "mode": "automatic|report-based",
  "analysisReport": { /* full accessibility report if Mode A */ },
  "totalFixes": 12,
  "fixesApplied": [
    {
      "issueId": "IMG-001",
      "description": "Added alt text to sales chart",
      "location": "Page 3"
    }
  ],
  "remainingIssues": [
    {
      "issueId": "TBL-003",
      "reason": "Requires manual review",
      "recommendation": "Have a human verify table semantics"
    }
  ]
}
```

## Document Format Handling

### DOCX/DOC
- Use python-docx or similar library
- Preserve styles where possible

### PDF
- If editable: Apply changes directly
- If scanned: Note that full revision requires OCR + re-authoring

### ODT
- Use ODF library
- Preserve formatting

## Quality Assurance

Before finalizing:
1. Verify critical issues are resolved
2. Check fixes don't introduce new issues
3. Ensure original content is preserved
4. Validate output is well-formed