# INVEST Criteria: Quality Standards for User Stories

INVEST is a set of six principles for evaluating User Story quality, proposed by Bill Wake. When analyzing RFPs, ensure that decomposed feature items meet these principles to facilitate conversion into executable User Stories.

## Six Principles

### I - Independent

**Definition**: Stories should be as independent as possible, able to be developed, tested, and deployed separately

**Why It Matters**:
- Allows team flexibility in adjusting development order
- Reduces blocking due to dependencies
- Enables parallel development

**How to Check**:
- Can this Story deliver value independently without other Stories being completed?
- If there are dependencies, are they clearly marked?

**Example**:
```
❌ Bad: "As a user, I want to bookmark articles and view them on the bookmarks page"
   → Contains two independent features, should be split

✅ Good: "As a user, I want to bookmark a specific article"
✅ Good: "As a user, I want to view my list of bookmarked articles"
```

---

### N - Negotiable

**Definition**: Stories are conversation starters, not contract specifications; details can be adjusted during development

**Why It Matters**:
- Maintains requirement flexibility
- Encourages ongoing dialogue between team and PO
- Avoids locking in implementation details too early

**How to Check**:
- Does the Story describe "what to achieve" rather than "how to do it"?
- Are there overly detailed UI or technical specifications?

**Example**:
```
❌ Bad: "As a user, I want to click the red star icon in the top right corner,
         triggering an AJAX request to /api/favorites, and the star turns yellow on success"
   → Over-specifies implementation details

✅ Good: "As a user, I want to quickly bookmark the current page
          so I can easily access it later"
   → Describes the goal, leaves implementation details for development discussion
```

---

### V - Valuable

**Definition**: Each Story must bring clear value to users or the business

**Why It Matters**:
- Ensures all development work is meaningful
- Facilitates prioritization
- Helps team understand "why" this feature is needed

**How to Check**:
- Does the "so that..." part clearly state the value?
- Is this value something users actually care about?

**Example**:
```
❌ Bad: "As a user, I want the system to use PostgreSQL"
   → This is a technical decision, not user value

❌ Bad: "As a user, I want to log into the system"
   → Login itself isn't value, it's a means to achieve other goals

✅ Good: "As a user, I want to log in via company SSO
          so I can access my personalized settings and saved bookmarks"
   → Clearly states the value login brings
```

---

### E - Estimable

**Definition**: The team should be able to roughly estimate the effort needed to complete the Story

**Why It Matters**:
- Supports project planning and scheduling
- Stories that are too large or vague are hard to manage
- Inability to estimate usually indicates insufficient understanding

**How to Check**:
- Can the team estimate without additional research?
- If they can't estimate, is it due to technical unknowns or unclear requirements?

**Example**:
```
❌ Bad: "As an admin, I want to manage all system settings"
   → Scope too large, cannot estimate

✅ Good: "As an admin, I want to set the system's idle logout time
          so I can adjust according to security policy"
   → Clear scope, can be estimated
```

---

### S - Small

**Definition**: Stories should be small enough to complete within one Sprint (typically 1-2 weeks)

**Why It Matters**:
- Provides more frequent progress visibility
- Reduces risk per Story
- Easier to adjust and correct course

**How to Check**:
- Can this Story be completed in 1-3 days? (including testing)
- If it takes more than a week, can it be further split?

**Size Reference**:
| Size | Appropriateness | Action |
|------|-----------------|--------|
| < 0.5 days | Possibly too small | Consider merging related Stories |
| 0.5 - 3 days | Ideal size | ✅ |
| 3 - 5 days | Acceptable | Monitor closely |
| > 5 days | Too large | Must split |

---

### T - Testable

**Definition**: Stories must have clear completion criteria that can be verified through testing

**Why It Matters**:
- Avoids ambiguous "is it done?" disputes
- Supports automated testing
- Ensures quality

**How to Check**:
- Can you write acceptance test cases for this Story?
- Is the value in "so that..." observable or measurable?

**Example**:
```
❌ Bad: "As a user, I want the system to respond quickly"
   → "Quickly" is undefined, cannot test

✅ Good: "As a user, I want the page to load within 1 second
          so I can have a smooth browsing experience"
   → Has specific value, can be tested
```

---

## Application in RFP Analysis

### When Decomposing Features

When breaking down feature items from the RFP, use INVEST as checkpoints:

1. **First split to Independent (I) granularity**
2. **Ensure each item has Value (V)** - If you can't articulate the value, it might be a technical task rather than a Story
3. **Right Size (S)** - If too large, continue splitting; if too small, merge
4. **Keep it Negotiable (N)** - Don't lock in implementation details too early
5. **Mark non-Estimable (E) items** - May need a Spike (technical exploration)
6. **Think about how to Test (T)** - If you can't think of how to test, the Story might not be specific enough

### Annotation Method

Mark INVEST-related information next to feature items:

```
- [ ] **Article Bookmark Feature** [Explicit reference] [Low complexity]
  - INVEST Note: Can be developed independently; needs to split "bookmark" and "view bookmarks"
```

---

## Common INVEST Violation Patterns

| Violation Type | Symptom | Fix |
|----------------|---------|-----|
| Over-coupling | "Implement features A and B" | Split into independent Stories |
| No value | "As a developer..." | Rethink who benefits |
| Not estimable | "Integrate third-party system" | Do technical exploration first, then split into details |
| Too large | "Build complete backend" | Split by functional modules |
| Not testable | "Improve user experience" | Define specific, measurable improvement metrics |
