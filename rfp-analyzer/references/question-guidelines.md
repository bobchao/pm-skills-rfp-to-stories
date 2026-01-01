# Question Generation Guidelines

This document defines how to generate high-quality clarification questions in RFP analysis.

## Core Philosophy

> **A good question allows the client to answer in 30 seconds and unlocks a week of work for the development team.**

## Question Quality Checklist

Before raising any question, it must pass the following checks:

### ✅ Necessity Check

| Check Item | Pass Criteria |
|------------|---------------|
| Blocking | Development cannot start or will go in the wrong direction without this answer |
| Non-obvious | The answer cannot be directly found or reasonably inferred from the document |
| Specific Impact | Can clearly state which feature or decision this question affects |

### ❌ Exclusion Criteria

The following types of questions should be **avoided**:

1. **Academic Questions**
   - ❌ "Have you considered using GraphQL instead of REST?"
   - This is a technical choice discussion, not requirements clarification

2. **Perfectionist Questions**
   - ❌ "If the user's network disconnects while uploading an image, how should the system handle it?"
   - Unless the RFP explicitly requires offline support, this is an implementation detail

3. **Open-ended Exploration Questions**
   - ❌ "Besides the listed features, what other features are needed?"
   - This should be discussed in a kickoff meeting, not as a written question

4. **Questions with Reasonable Assumptions**
   - ❌ "Should user passwords be encrypted when stored?"
   - This is a basic security requirement, no need to ask

5. **Premature Questions**
   - ❌ "What export formats should Phase 3 reports support?"
   - If Phase 3 is six months away, this isn't a blocking question now

## Question Classification Framework

### 🔴 Blocking Questions (P0)

**Definition**: Questions whose answers are needed before system design can begin or to avoid wrong architectural decisions

**Typical Scenarios**:
- Divergence points in core business processes
- Technical specifications for third-party system integration
- Design basis for permission models
- Data sources and formats

**Example**:
```
🔴 Blocking: SSO Integration
The document mentions connecting to company SSO. Please confirm:
1. Is the SSO system SAML 2.0, OAuth 2.0, or LDAP?
2. Is there existing API documentation or test environment available?

【Impact】: This answer determines the authentication module's technical architecture and cannot be assumed.
```

### 🟡 Design Details (P1)

**Definition**: Questions that don't block development start but affect UI/UX design or feature details

**Typical Scenarios**:
- Interface interaction details
- Prompt message copy
- Non-core workflow handling

**Example**:
```
🟡 Design Detail: Delete Confirmation Mechanism
The document mentions "deletion requires confirmation". Please confirm preferred interaction method:
A. Pop-up confirmation dialog
B. Double-click confirmation (button changes color, then click again)
C. Type confirmation text (like GitHub repo deletion)

【Default Suggestion】: If no special requirements, recommend A (most common and familiar to users)
```

### 🟢 Pending Materials (P2)

**Definition**: External resources needed from the client that can proceed in parallel with development

**Typical Scenarios**:
- Design files (Figma/Sketch)
- API documentation
- Test accounts
- Asset resources

**Example**:
```
🟢 Pending Materials:
- [ ] Figma design file link (or confirm development team will design)
- [ ] GA4 tracking code (if analytics needed)
- [ ] Test environment SSO account
```

## Question Writing Format

### Standard Format

```markdown
### [Question Title]

[One sentence describing the question background]

**Specific Question**:
[Clear, directly answerable question]

**Impact Scope**:
- [Feature A]
- [Feature B]

**Suggested Options** (if applicable):
- A. [Option one]
- B. [Option two]

**Default Assumption** (if applicable):
If no response, will proceed with [X] approach for design.
```

### Question Consolidation Principle

Related questions should be consolidated into one group rather than split into multiple independent questions:

**Bad Practice**:
```
1. What protocol does SSO use?
2. Is there SSO API documentation?
3. Is there an SSO test environment?
```

**Good Practice**:
```
1. SSO Integration Details
   - Protocol type: SAML 2.0 / OAuth 2.0 / LDAP / Other
   - Is there API documentation for reference?
   - Is there a test environment? If so, how to obtain test accounts?
```

## Question Quantity Guidelines

Reasonable question count ranges based on RFP complexity:

| RFP Complexity | 🔴 Blocking | 🟡 Design Details | 🟢 Pending Materials |
|----------------|-------------|-------------------|---------------------|
| Simple (single feature) | 0-2 | 1-3 | 1-2 |
| Medium (complete system) | 3-5 | 3-5 | 2-4 |
| Complex (multi-system integration) | 5-8 | 5-8 | 3-5 |

**Note**: These are guidelines, not hard limits. If the RFP is very complete, fewer questions may be needed; if the RFP is too brief, more questions may be required.

## Common Error Patterns

### Error 1: Nitpicking

**Question**: "If the user is logged into two browsers simultaneously and editing the same document, how should the system handle conflicts?"

**Why It's Bad**: Unless the RFP explicitly mentions collaborative editing, this is over-expansion

**Improvement**: First confirm if multi-user collaborative editing is needed, then dive deeper if required

### Error 2: Pretending Not to Know Industry Conventions

**Question**: "Should the password field have a show/hide toggle during registration?"

**Why It's Bad**: This is standard modern UI practice, no need to ask

**Improvement**: Don't ask, implement as a basic feature

### Error 3: Pushing Responsibility Back to Client

**Question**: "Please provide the complete field list and validation rules"

**Why It's Bad**: The analyst should organize based on the RFP and ask the client to confirm, not expect the client to produce everything

**Improvement**: "Based on RFP analysis, user data is suggested to include the following fields: [list]. Please confirm if anything is missing or needs adjustment"

### Error 4: Overly Technical Questions

**Question**: "Should the API support HATEOAS?"

**Why It's Bad**: The client may not understand what this is

**Improvement**: "Are there specific requirements for API response format? Or can the development team design based on best practices?"
