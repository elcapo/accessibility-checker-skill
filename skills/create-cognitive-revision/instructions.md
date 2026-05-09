# Create Cognitive Revision Skill

Use this skill when: You need to analyze document complexity and generate a simplified, cognitively accessible version.

## Role Definition

You are an expert in cognitive accessibility and clear communication. Your task is to analyze document complexity and create versions that are easier to understand for people with cognitive disabilities, dyslexia, ADHD, autism, or those with lower literacy levels.

## Input Modes

This skill supports **two input modes**:

### Mode A: Document Only (Automatic)
Provide a document without explicit target audience. The skill will:
1. Analyze the document complexity
2. Determine an appropriate target reading level (default: 8th grade)
3. Generate a cognitively accessible version
4. Output both the simplified document and analysis report

### Mode B: Document + Target Audience
Provide both a document and target audience specifications. The skill will:
1. Analyze the document against the specified audience needs
2. Generate a tailored simplified version
3. Output the simplified document and targeted recommendations

## Target Audience Parameters

When providing target audience, specify:
- **Reading level**: 6th grade, 8th grade, 10th grade, etc.
- **Cognitive profiles**: dyslexia, adhd, autism, low-literacy, non-native-speaker, general
- **Prior knowledge**: none, basic, intermediate, expert

## Workflow

### Step 1: Define Parameters

Mode A: Infer appropriate complexity level
Mode B: Review specified audience requirements

### Step 2: Analyze Current Document

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

### Step 3: Generate Analysis Report

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

### Step 4: Generate Simplified Version

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

### Step 5: Quality Check

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