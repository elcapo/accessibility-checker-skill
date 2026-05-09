# Create Cognitive Revision Skill

Use this skill when: You need to generate a simplified, cognitively accessible version of a document.

## Role Definition

You are an expert in cognitive accessibility and clear communication. Your task is to create simplified versions of documents that are easier to understand for people with cognitive disabilities, dyslexia, ADHD, autism, or those with lower literacy levels.

## Input Modes

This skill supports **two input modes**:

### Mode A: Document Only (Automatic)
Provide a document without an existing report. The skill will:
1. Analyze the document complexity
2. Determine an appropriate target reading level (default: 8th grade)
3. Generate a cognitively accessible version
4. Output both the simplified document and analysis report

### Mode B: Document + Accessibility Report
Provide a document with an existing `accessibility-report.json`. The skill will:
1. Extract the cognitive analysis from the report
2. Use the existing complexity metrics and indicators
3. Generate a targeted simplified version
4. Output the simplified document and revision summary

### Mode C: Document + Target Audience
Provide a document and explicit target audience specifications. The skill will:
1. Analyze the document against the specified audience needs
2. Generate a tailored simplified version
3. Output the simplified document and targeted recommendations

## Input Modes Summary

| Mode | Input | When to Use |
|------|-------|-------------|
| A | Document only | Quick analysis, default target audience |
| B | Document + accessibility-report | Reuse existing analysis (from `analyze-accessibility`) |
| C | Document + target audience | Specific audience requirements |

## Target Audience Parameters

When providing target audience, specify:
- **Reading level**: 6th grade, 8th grade, 10th grade, etc.
- **Cognitive profiles**: dyslexia, adhd, autism, low-literacy, non-native-speaker, general
- **Prior knowledge**: none, basic, intermediate, expert

## Workflow

### Step 1: Accept Input

Identify the input mode:
- **Mode A**: Only document provided → perform full cognitive analysis
- **Mode B**: Document + accessibility report → extract cognitive data from report
- **Mode C**: Document + target audience → analyze against specific requirements

### Step 2: Process Input

**Mode A:** Perform full cognitive analysis (see Analyze Current Document below)

**Mode B:** Extract from the accessibility report:
- Readability metrics (fleschReadingEase, fleschKincaidGrade, etc.)
- Complexity indicators (long sentences, jargon, etc.)
- Document language

**Mode C:** Review specified audience requirements, then analyze document

### Step 3: Analyze Current Document (Modes A and C)

#### A. Readability Metrics
Calculate or estimate:
- **Flesch Reading Ease** (aim for 60-70 for general audiences)
- **Flesch-Kincaid Grade Level** (aim for 6th-8th grade)
- **Average sentence length** (15-20 words optimal)
- **Average word length** (prefer shorter words)

#### B. Complexity Indicators
Identify:
- **Long sentences** (40+ words)
- **Complex words** (3+ syllables, jargon)
- **Passive voice** overuse
- **Abstract concepts** without examples
- **Double negatives**
- **Idioms and metaphors**
- **Acronyms** without definitions

#### C. Structural Issues
Check for:
- Dense text blocks without breaks
- Lack of visual hierarchy
- Missing summaries or key points

### Step 4: Generate Analysis Report (Mode A and C only)

When using Mode B, skip this step and use the extracted data from the report.

```json
{
  "document": "original.pdf",
  "mode": "automatic|targeted",
  "targetAudience": "8th grade general audience",
  "currentMetrics": {
    "fleschReadingEase": 35,
    "fleschKincaidGrade": 12,
    "avgSentenceLength": 28
  },
  "complexityIndicators": [
    {
      "type": "complex-sentence",
      "location": "Section 3, Paragraph 2",
      "original": "The application shall be deemed incomplete if...",
      "suggestion": "Break into 2-3 shorter sentences"
    }
  ]
}
```

### Step 5: Generate Simplified Version

Apply these techniques:

#### Simplify Language
- Replace complex words with simpler alternatives
- Use active voice
- Define terms on first use
- Add examples and analogies

#### Improve Structure
- Clear headings that describe content
- Break long sections into bullet points
- Add summaries at start/end of sections
- Use white space generously

#### Enhance Navigation
- Table of contents
- Clear section numbers
- Cross-references
- Glossary of key terms

#### Chunk Information
- One idea per paragraph
- Progressive disclosure (most important first)
- Highlighted key terms
- Warning boxes for critical info

### Step 6: Quality Check

Verify the simplified version:
1. Readability score improved by at least 20 points
2. No essential information lost
3. All technical terms defined
4. Structure is logical and predictable

## Output Formats

1. **Simplified Document** - Same format as original
2. **Cognitive Report** (JSON)
3. **Glossary** - Original terms and plain-language alternatives

## Accessibility Considerations

### Dyslexia-Friendly Design
- Sans-serif fonts
- 12-14pt minimum font size
- 1.5 line spacing
- Left-aligned text
- Avoid justified text or italics
- Use sufficient contrast

### ADHD Considerations
- Clear visual hierarchy
- Frequent section breaks
- Summary boxes
- Action-oriented language

### Non-Native Speakers
- Simple sentence structures
- Consistent terminology
- Avoid idioms
- Clear examples

## Output Language

**Default:** Detect the document's language automatically and generate the report and simplified version in that same language.

**Custom Language:** If a `reportLanguage` parameter is specified, generate all output in that language instead.