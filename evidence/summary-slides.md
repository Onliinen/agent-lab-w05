# NDHU Campus Agent Lab · Executive Summary Deck

````carousel
# Slide 1: Welcome & Mission
## NDHU Campus Agent Lab (`agent-lab-w05`)
**讓 AI 幫你完成一件校園小事 · Practical Agent Pairing & Critical Inspection**

- **Target**: Practical pairing with an autonomous coding agent (Antigravity).
- **Core Philosophy**: Human-in-the-loop oversight. Moving beyond naive prompting to active plan evaluation, rigorous boundary testing, and structured feedback.
- **Repository Deliverables**:
  - `practice/01-club-files/`: Safe file organization & manifest generation.
  - `practice/02-campus-picker/`: Offline single-page campus activity picker (v1 & v2).
  - `practice/03-equipment/`: Data cleaning, formatting, and anomaly detection.
  - `practice/04-review/`: Critical plan evaluation & formal rejection note.
  - `submission-template.md` & `evidence/`: Complete verification audit trail.
<!-- slide -->
# Slide 2: The 4 Core Principles
## What This Lab Is Actually Teaching

1. **Understand Agent Plans Before Execution**
   - Demand plain-language explanations of proposed reads, writes, and deletions.
   - Enforce least-privilege folder boundaries before granting write permissions.
2. **Verify Results Objectively**
   - Never trust "Task Complete" at face value.
   - Verify file counts, perform SHA-256 hash checks, and test edge conditions.
3. **Recognize Agent Overreach & Limitations**
   - Catch permission oversteps (scanning entire `Downloads` folder, hallucinating missing data).
4. **Iterate & Reject Professionally**
   - Differentiate newly requested features from unmet baseline specifications.
   - Formulate actionable, unambiguous rejection messages with acceptable alternatives.
<!-- slide -->
# Slide 3: Task A · Safe File Organization
## `practice/01-club-files`

- **Scenario**: Organizing 12 club files without losing draft proposals or duplicate records.
- **Key Principles Executed**:
  - **100% Non-Destructive**: Input directory preserved completely untouched.
  - **Duplicate Preservation**: Identical copies (`announcement.txt` & `equipment_list.txt`) verified via SHA-256 and retained.
  - **Anti-Hallucination**: Refused to declare `proposal_final2.txt` as "definitive" over `proposal_final.txt`. Both outdoor (30m) and indoor (20m) proposals retained for club vote.
- **Key Outputs**:
  - `output/manifest.json`: Array of 12 source-to-destination mappings with reasons.
  - `output/report.md`: Complete audit report detailing categorizations and action items.
<!-- slide -->
# Slide 4: Task B · Offline Activity Picker
## `practice/02-campus-picker`

- **Goal**: Create an offline single-page tool (`index.html`) to pick campus break activities.
- **Version 1 (B v1)**:
  - Zero external dependencies: pure CSS & JavaScript, works offline on double-click.
  - Strict 3-way filtering: Location (indoor/outdoor/all), Time (≤ 15/30/60 min), Energy (low/med/all).
  - Explicit warning when no activities match (never quietly relaxes user criteria).
  - Recent 5-draw history (latest first) & instant Chinese/English toggle.
- **Evolution (B v2)**:
  - **Anti-Consecutive Repeat**: Guarantees distinct picks in consecutive draws when candidates ≥ 2.
  - **Live Candidate Counter**: Dynamic badge displaying currently matching item count.
  - **Keyboard Accessibility**: Quick trigger using Spacebar or Enter.
<!-- slide -->
# Slide 5: Task C · Data Hygiene & Cleaning
## `practice/03-equipment`

- **Goal**: Clean messy club equipment records without corrupting raw facts.
- **Key Achievements**:
  - **Row Pruning (10 ➔ 9)**: Removed row 6 (all-null empty object `{}`) while strictly preserving original `source_row` IDs for auditability.
  - **Zero Data Hallucination**: Invalid quantities (`""` on row 7, `-1` on row 8) retained verbatim in data and flagged in `issues.md` without guessing or zero-padding.
  - **Conflict Identification**: Retained duplicate item IDs (`EQ01` and `EQ02`), explicitly documenting the count discrepancy (2 vs. 3 extension cords).
  - **Status Standardization**: Normalized aliases (`可借`, `借出`, `可出借`), mapped non-standard `待盤點` to `unknown`.
<!-- slide -->
# Slide 6: Task D · Critical Review & Rejection
## `practice/04-review`

- **Scenario**: Reviewing `bad-plan.txt` ("Organize all of Downloads, delete duplicates, assume final2 is latest, guess missing values, auto-publish").
- **Identified Red Flags**:
  1. *Scope Violation*: Accessing entire system Downloads folder.
  2. *Destructive Action*: Irreversible duplicate file deletion.
  3. *Arbitrary Versioning*: Guessing latest version by filename suffix.
  4. *Data Hallucination*: Making up numbers for missing values.
  5. *Data Leakage*: Unauthorized automatic external publishing.
- **Deliverable**:
  - `my-rejection.md`: Formal prompt rejecting the plan, explaining why, and detailing 5 acceptable alternative constraints.
<!-- slide -->
# Slide 7: Audit Trail & Conclusion
## Transparent Learning Record & Git Discipline

- **Git Commit Progression**:
  - `95f03f9` · `A: organize club files`
  - `d791a2f` · `B v1: activity picker`
  - `82bac42` · `B v2: add no consecutive repeats and live counter`
  - `d9cd345` · `D: rejection`
  - `4c798cf` · `C: normalize equipment records`
  - `e599ce8` · `record: update learning record with task c`
- **Takeaway**:
  - AI Agents excel at execution when guided by clear boundaries, verification metrics, and proactive human judgment.
````
