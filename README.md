# Product Management Skills - RFP to User Stories

Anthropic Agent Skills suite for converting RFP (Request for Proposal) or requirements documents into high-quality User Stories.

## 👤 Author

**Po-chiang Chao**

- 🌐 **Connect with me on social media**: [bobchao.net](https://bobchao.net)
- 💼 **Product Management mentoring**: [stableprogress.com](https://stableprogress.com)

## 📁 Project Structure

```
(root)/
├── rfp-analyzer/                    # Skill 1: RFP Analysis
│   ├── SKILL.md                     # Main Skill definition
│   └── references/
│       ├── question-guidelines.md   # Question generation guidelines
│       └── invest-criteria.md       # INVEST principles explanation
│
├── story-writer/                    # Skill 2: Story Writing
│   ├── SKILL.md                     # Main Skill definition (with refine mode)
│   ├── references/
│   │   └── story-templates.md       # Story template library
│   └── assets/
│       └── output-example.md        # Complete output example
│
├── story-refiner/                   # Skill 3: Story Refinement
│   ├── SKILL.md                     # Main Skill definition
│   ├── references/
│   │   └── evaluation-criteria.md   # Evaluation criteria
│   └── assets/
│       └── refine-example.md        # Refinement report example
│
└── README.md
```

## 🌐 Language Support

All Skills default to responding in the **same language as user input**. Users can explicitly specify a preferred language:
- "請用中文回答" → Responds in Chinese
- "Reply in Japanese" → Responds in Japanese
- No specification → Matches input document language

---

## 🎯 Design Philosophy

### Division of Three Skills

| Skill | Responsibility | Core Capability |
|-------|----------------|-----------------|
| **RFP Analyzer** | Understanding & Decomposition | Identify roles, decompose modules, extract constraints, generate questions |
| **Story Writer** | Writing & Formatting | Standard format, granularity control, implied requirement handling |
| **Story Refiner** | Evaluation & Correction | Multi-perspective scoring, auto-correction, quality assurance |

### Why This Design?

1. **Separation of concerns**: Analysis, writing, and refinement are different cognitive tasks
2. **Automated correction**: Refiner doesn't just report issues, it directly produces improved versions
3. **Reduced manual intervention**: Users only need final confirmation, not manual corrections
4. **Flexible combination**: Can choose workflow based on project complexity

### Problems Solved

| Original Pain Point | Solution |
|---------------------|----------|
| Too many questions/nitpicking | Three-tier classification + filtering questions |
| Implied requirements over-expansion | Clear supplementation boundaries |
| Inconsistent Story quality | INVEST principles + three-perspective scoring |
| Report only, no correction | Story Refiner auto-produces improved versions |

---

## 🚀 Usage Methods

### Method 1: One-Stop (Recommended)

Simplest usage method, Story Writer's refine mode:

```
RFP → [story-writer --refine] → Final User Stories
```

**Trigger**: Tell Story Writer "please refine" or "complete mode"

**Suitable for**:
- Small to medium projects
- Quick results desired
- No intermediate output needed

---

### Method 2: Complete Workflow

Suitable for complex projects or situations requiring manual review:

```
Step 1: RFP Analyzer
────────────────────
Input: Raw RFP document
Output: Structured analysis report
     ├── Stakeholder list
     ├── Functional module decomposition
     ├── System constraints
     └── Classified clarification questions

        ↓ [Manual review + answer 🔴 questions]

Step 2: Story Writer
────────────────────
Input: Analysis report + question answers
Output: User Stories draft

        ↓ [Optional: manual review]

Step 3: Story Refiner
────────────────────
Input: User Stories
Output: Refinement report
     ├── Quality assessment
     ├── Corrected Stories
     └── Final complete list
```

**Suitable for**:
- Large complex projects
- Phase-by-phase review needed
- Multi-person collaboration

---

### Method 3: Quick Mode

Skip analysis, directly produce Stories:

```
RFP → [story-writer] → User Stories
```

**Suitable for**:
- Simple, clear requirements
- Time pressure
- MVP/POC projects

---

## 📋 Detailed Skill Descriptions

### 1. RFP Analyzer

**Trigger**: Receive RFP or requirements document, need to "understand the full picture" first

**Core Functions**:
- Phase 1: Quick scan and background understanding
- Phase 2: Stakeholder identification
- Phase 3: Functional module decomposition
- Phase 4: Non-functional requirements extraction
- Phase 5: Question generation (three-tier classification)

**Question Classification**:

| Category | Icon | Description |
|----------|------|-------------|
| Blocking | 🔴 | Must answer before development |
| Design Details | 🟡 | Confirm during design phase |
| Pending Materials | 🟢 | Can proceed in parallel |

### 2. Story Writer

**Trigger**: Have analysis results or requirements list, need to convert to User Stories

**Core Functions**:
- Standard format writing (role/action/value)
- Granularity control
- Implied requirement handling (with boundaries)
- Acceptance criteria writing

**Execution Modes**:
- **Standard Mode**: Quick draft production
- **Refine Mode**: Auto-evaluate and correct after production

### 3. Story Refiner

**Trigger**: Have Stories needing quality assurance and correction

**Core Functions**:
- Three-perspective evaluation (Developer/QA/Stakeholder)
- 1-5 point scoring system
- Auto-correct low-scoring Stories
- **Iterative refinement** (max 3 rounds, ensures split Stories are evaluated too)

**Scoring Criteria**:

| Score | Disposition |
|-------|-------------|
| 5 | ✅ Direct pass |
| 4 | ✅ Pass, can attach minor suggestions |
| 3 | ⚠️ Recommend correction |
| 2 | ❌ Must correct |
| 1 | ❌ Must rewrite |

**Iterative Refinement**:

```
Round 1: Evaluate all → Correct low-scoring items → May generate new Stories (splits)
    ↓
Round 2: Evaluate "corrected" + "newly generated" → Correct again if needed
    ↓
Round 3: (If still issues) Final fine-tuning
    ↓
Terminate: All Stories ≥ 4 points, or limit reached
```

**Termination Conditions** (stop when any is met):
1. All Stories score ≥ 4
2. No corrections this round
3. Already executed 3 rounds

---

## 📖 Reference File Descriptions

| File | Location | Purpose |
|------|----------|---------|
| `question-guidelines.md` | rfp-analyzer | Question filtering criteria, writing format |
| `invest-criteria.md` | rfp-analyzer | INVEST principles detailed explanation |
| `story-templates.md` | story-writer | Story templates for various features |
| `evaluation-criteria.md` | story-refiner | Three-perspective scoring criteria |

---

## 🔧 Customization

### Adjust Question Quantity/Strictness

Modify `rfp-analyzer/references/question-guidelines.md`:
- Question quantity guidelines table
- Exclusion criteria list

### Adjust Story Format

Modify `story-writer/SKILL.md`:
- Output format section
- Acceptance criteria format

### Adjust Scoring Thresholds

Modify `story-refiner/references/evaluation-criteria.md`:
- Default threshold settings
- Strict/lenient mode definitions

### Add Domain Templates

Add commonly used scenarios in `story-writer/references/story-templates.md`.

---

## 💡 Best Practices

### DO ✅

- Use RFP Analyzer first to confirm understanding for complex projects
- Use refine mode to ensure Story quality
- Answer blocking questions before producing Stories
- Adjust template wording based on project

### DON'T ❌

- Don't expect "zero manual intervention" (final confirmation still needed)
- Don't skip blocking questions and produce directly
- Don't mechanically apply all templates
- Don't ignore Refiner's correction suggestions

---

## 🔄 Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.2.0 | 2026-01 | Converted all Skills to English, added language preference support |
| 1.1.0 | 2025-12 | Added Story Refiner with iterative refinement support |
| 1.0.0 | 2025-12 | Initial version (Analyzer + Writer) |

---

## 🔗 Related Resources

- [Anthropic Skills Official Spec](https://github.com/anthropics/skills)
- [INVEST Principles Original Article](https://xp123.com/articles/invest-in-good-stories-and-smart-tasks/)
- [User Story Best Practices](https://www.mountaingoatsoftware.com/agile/user-stories)

---

## 📄 License

This project is licensed under the **MIT License**.

```
MIT License

Copyright (c) 2026 Po-chiang Chao

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

For more information, visit: [MIT License](https://opensource.org/licenses/MIT)
