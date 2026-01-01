# Story Evaluation Criteria

This document defines the evaluation criteria and scoring methods used by Story Refiner.

## Scoring Dimensions

Each Story is scored from three dimensions, each 1-5 points. Final score is the average of all three (rounded).

### Dimension 1: Development Clarity

**Evaluator Perspective**: Senior Developer

| Score | Criteria |
|-------|----------|
| 5 | Can start development immediately without any additional confirmation |
| 4 | Generally clear, may have 1-2 minor details to confirm |
| 3 | Main direction clear, but some gray areas need discussion |
| 2 | Scope unclear, needs significant clarification before starting |
| 1 | Completely unclear what to do, or contains contradictory requirements |

**Specific Checkpoints**:

```markdown
□ Is action description specific?
  - 5 points: "Upload JPG/PNG format images, limited to 5MB"
  - 3 points: "Upload images"
  - 1 point: "Handle images"

□ Does scope have boundaries?
  - 5 points: "Edit article title and content"
  - 3 points: "Edit article"
  - 1 point: "Manage articles"

□ Are dependencies clear?
  - 5 points: Clearly marked "requires US-001 login feature completed first"
  - 3 points: Implied dependency but not marked
  - 1 point: Confusing or circular dependencies
```

---

### Dimension 2: Testability

**Evaluator Perspective**: QA Engineer

| Score | Criteria |
|-------|----------|
| 5 | Can directly write complete test cases including boundary conditions |
| 4 | Main test cases clear, boundary conditions need minor additions |
| 3 | Know what to test, but specific conditions need confirmation with development |
| 2 | Generally know direction, but can't write specific test cases |
| 1 | Completely untestable, or "so that" value can't be verified |

**Specific Checkpoints**:

```markdown
□ Are acceptance criteria clear?
  - 5 points: Has specific Given-When-Then or checklist
  - 3 points: Has general direction but not specific
  - 1 point: No acceptance criteria, or vague like "should be user-friendly"

□ Is value verifiable?
  - 5 points: "so that I can find target article within 3 seconds" (measurable)
  - 3 points: "so that I can find articles faster" (relative but comparable)
  - 1 point: "so that I can have a better experience" (not measurable)

□ Are error scenarios considered?
  - 5 points: Clearly states error handling
  - 3 points: Only happy path, but error handling can be inferred
  - 1 point: Error scenarios completely unconsidered, and important to feature
```

---

### Dimension 3: Value Clarity

**Evaluator Perspective**: Product Stakeholder

| Score | Criteria |
|-------|----------|
| 5 | Value is clear and important, directly maps to business objectives |
| 4 | Value is clear, reasonable feature requirement |
| 3 | Roughly understand value, but feels optional |
| 2 | Not sure why this feature is needed |
| 1 | Can't see value, or it's a technical task disguised as a Story |

**Specific Checkpoints**:

```markdown
□ Does "so that..." state real value?
  - 5 points: "so that I can pull up data within 10 seconds when customer calls"
  - 3 points: "so that I can quickly view data"
  - 1 point: "so that I can use this feature" (circular reasoning)

□ Is role correct?
  - 5 points: Role is clear and is the true beneficiary of this feature
  - 3 points: Role too generic (e.g., "user" covers too much)
  - 1 point: Wrong role (e.g., giving admin feature to regular user)

□ Maps to original requirements?
  - 5 points: Can directly trace to a specific RFP paragraph
  - 3 points: Is reasonably derived implied requirement
  - 1 point: Can't see connection to original requirements
```

---

## Combined Score Calculation

```
Final Score = round((Development Clarity + Testability + Value Clarity) / 3)
```

### Scoring Examples

**Example 1: High-Scoring Story**

```markdown
Story: As a customer service rep, I want to quickly search customer data by phone number
       so that I can pull up data within 10 seconds when customer calls.

Acceptance Criteria:
- Display search results within 1 second of entering phone number
- Support partial number search (at least 4 digits)
- Show "Customer not found" prompt when no results
```

Scoring:
- Development Clarity: 5 (Specific action, has performance requirements)
- Testability: 5 (Has clear acceptance criteria, measurable metrics)
- Value Clarity: 5 (Clear role, specific and important value)
- **Final: 5 points** ✅ Pass

---

**Example 2: Medium-Scoring Story**

```markdown
Story: As a user, I want to edit my personal profile so that I can keep my information accurate.
```

Scoring:
- Development Clarity: 3 ("Personal profile" - which fields are included?)
- Testability: 3 (Can test edit functionality, but don't know specific fields)
- Value Clarity: 4 (Reasonable value, role slightly generic)
- **Final: 3 points** ⚠️ Needs correction

Correction suggestion: Add list of editable fields

---

**Example 3: Low-Scoring Story**

```markdown
Story: As a developer, I want the system to use Redis for caching so that performance is improved.
```

Scoring:
- Development Clarity: 2 (This is a technical decision not a Story)
- Testability: 2 ("Improved performance" not measurable)
- Value Clarity: 1 (Developer shouldn't be Story's role)
- **Final: 2 points** ❌ Must correct

Correction suggestion: This should be a system constraint, not a User Story. If keeping, rewrite as:
"As a user, I want pages to load within 1 second so that I can have a smooth experience."
(Technical implementation like Redis goes in notes or system constraints)

---

## Common Deduction Patterns

### Development Clarity Common Issues

| Issue | Deduction | Example |
|-------|-----------|---------|
| Vague verbs | -1~2 | "manage", "handle", "maintain" |
| No scope boundary | -1~2 | "all settings", "various reports" |
| Compound features | -1 | "create and edit" |
| Technical details mixed in | -1 | "load using AJAX" |

### Testability Common Issues

| Issue | Deduction | Example |
|-------|-----------|---------|
| No acceptance criteria | -1~2 | None at all (important features deduct more) |
| Vague criteria | -1 | "should be fast", "should look good" |
| Untestable value | -2 | "so that I can have better experience" |

### Value Clarity Common Issues

| Issue | Deduction | Example |
|-------|-----------|---------|
| Circular reasoning | -2 | "so that I can use this feature" |
| Role too generic | -1 | Everything is "user" |
| Technical task disguised | -3 | "As a developer" |
| Deviates from original requirements | -1~2 | Features RFP didn't mention |

---

## Threshold Settings

### Default Thresholds

| Score | Disposition |
|-------|-------------|
| 5 | ✅ Direct pass |
| 4 | ✅ Pass, can attach minor suggestions |
| 3 | ⚠️ Recommend correction (optional) |
| 2 | ❌ Must correct |
| 1 | ❌ Must rewrite or remove |

### Adjusting Thresholds

Adjust based on project nature:

**High-Risk Projects** (finance, healthcare, security-related):
- Raise pass threshold to 5 points
- Must correct 3 points and below
- All Stories must have acceptance criteria

**MVP/POC Projects**:
- Lower pass threshold to 3 points
- Only correct 1-point severe issues
- Acceptance criteria optional
