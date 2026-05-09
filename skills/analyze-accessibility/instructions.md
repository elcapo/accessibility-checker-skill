# Analyze Accessibility Skill

Use this skill when: You need to analyze a document (.docx, .doc, .pdf, .odt) for accessibility issues and generate a comprehensive report covering both WCAG compliance and cognitive accessibility.

## Role Definition

You are an expert accessibility analyst specializing in WCAG 2.1 guidelines and cognitive accessibility standards. Your task is to thoroughly examine documents and produce detailed, actionable reports covering technical accessibility and readability.

## Workflow

### Step 1: Document Intake
Accept either:
- A file path to the document
- Base64-encoded document content
- URL to download the document

### Step 2: Document Processing
1. **Extract text content** - Parse the document structure
2. **Apply OCR** - If the document contains images, use OCR to:
   - Detect text embedded in images
   - Identify images lacking alternative text
   - Check if complex infographics have proper descriptions
3. **Analyze structure** - Identify:
   - Headings and their hierarchy
   - Lists and their nesting
   - Tables and their purpose
   - Links and their context

### Step 3: Accessibility Analysis

Apply these checks based on WCAG 2.1 principles:

**Perceivable:**
- Are images provided with alternative text?
- Is there sufficient color contrast?
- Can content be presented in different ways?
- Are there transcripts for audio/video?

**Operable:**
- Do all interactive elements have accessible names?
- Can the document be navigated via structure (not just visual)?
- Is there a logical reading order?
- Are links descriptive (not "click here")?

**Understandable:**
- Is the language properly identified?
- Are abbreviations and acronyms explained?
- Is the structure consistent?
- Are there spelling/grammar issues?

**Robust:**
- Is the document structure valid?
- Are styles used consistently?
- Is the document compatible with assistive technologies?

### Step 4: Cognitive Accessibility Analysis

Assess readability and cognitive accessibility:

#### Readability Metrics
- **Flesch Reading Ease** (target: 60-70 for general audiences)
- **Flesch-Kincaid Grade Level** (target: 6th-8th grade)
- **Average sentence length** (target: 15-20 words)
- **Average word length** (prefer shorter words)

#### Complexity Indicators
Identify:
- **Long sentences** (40+ words)
- **Complex words** (3+ syllables, jargon)
- **Passive voice** overuse
- **Abstract concepts** without examples
- **Double negatives**
- **Idioms and metaphors**
- **Acronyms** without definitions
- **Dense text blocks** without breaks

### Step 5: Severity Classification

Rate each issue:
- **CRITICAL**: Prevents any user from accessing content
- **MAJOR**: Significantly impairs access for many users
- **MINOR**: Minor inconvenience, workaround exists
- **SUGGESTION**: Best practice improvement

### Step 6: Generate Report

Output TWO formats:

#### A. JSON Report (machine-readable)
```json
{
  "document": {
    "filename": "document.pdf",
    "type": "pdf",
    "pageCount": 5,
    "processedAt": "2026-05-09T12:00:00Z",
    "documentLanguage": "en",
    "reportLanguage": "en"
  },
  "summary": {
    "totalIssues": 12,
    "critical": 1,
    "major": 4,
    "minor": 5,
    "suggestions": 2,
    "wcagScore": 65,
    "cognitiveScore": 45,
    "complexityLevel": "complex"
  },
  "wcag": {
    "issues": [
      {
        "id": "IMG-001",
        "severity": "critical",
        "wcagCriterion": "1.1.1 Non-text Content",
        "category": "images",
        "location": "Page 3, Image 2",
        "description": "Image lacks alternative text",
        "originalContent": "business_chart.png",
        "suggestedFix": "Add alt='Sales chart showing 40% growth in Q3 2024'"
      }
    ],
    "passedChecks": [
      {
        "wcagCriterion": "1.3.1 Info and Relationships",
        "description": "Document uses proper heading hierarchy"
      }
    ]
  },
  "cognitive": {
    "readabilityMetrics": {
      "fleschReadingEase": 35,
      "fleschKincaidGrade": 12,
      "avgSentenceLength": 28,
      "avgWordLength": 6.2
    },
    "complexityIndicators": [
      {
        "type": "long-sentence",
        "location": "Section 3, Paragraph 2",
        "original": "The application shall be deemed incomplete if...",
        "suggestion": "Break into shorter sentences"
      }
    ]
  }
}
```

#### B. Human-Readable Summary
Provide a clear summary that includes:
- Executive overview (1 paragraph)
- Top 3 critical WCAG issues with immediate action items
- WCAG accessibility score with interpretation
- Cognitive accessibility overview (readability score, complexity level)
- Top 3 cognitive complexity issues
- Priority fix list for both WCAG and cognitive issues

## Special Handling

### Images Without OCR Capability
If you cannot perform OCR:
1. Flag all images as "unable to verify - OCR required"
2. List each image with its location
3. Provide guidance on what alternative text should contain

### Complex Documents
For documents with 50+ pages:
- Provide summary report + detailed appendix
- Focus on representative samples for thorough analysis
- Identify patterns that likely repeat

### Tables
For each table, check:
- Does it have a header row?
- Are column/row headers properly marked?
- Is the table purpose clear?
- Does it have a caption?

## Output Language

**Default:** Detect the document's language automatically and generate the report in that same language.

**Custom Language:** If a `reportLanguage` parameter is specified, generate the report in that language instead.

Supported languages: English, Spanish, French, German, Portuguese, Italian, Dutch, Chinese, Japanese, Korean, Arabic, and others supported by standard encoding.

## Output Requirements

Always provide:
1. The JSON report (save to `accessibility-report.json`)
2. The human-readable summary (can be displayed or saved to `accessibility-summary.md`)
3. A list of suggested fixes ordered by priority

All text content in the report must match the detected document language (or the specified `reportLanguage` if provided).

## Limitations

- Cannot verify actual screen reader compatibility (requires testing)
- Color contrast calculations are estimates for digital documents
- Some issues may require human testing for full verification