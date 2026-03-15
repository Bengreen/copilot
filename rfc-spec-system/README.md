# RFC-Style Specification System

**Version:** 1.0  
**Last Updated:** 2026-03-14  

This is the global template and documentation for an RFC-inspired requirement and specification system designed for scalable, auditable, and team-friendly project documentation.

## Overview

A specification framework that:
- ✅ Tracks requirements as versioned, living documents (like IETF RFCs)
- ✅ Consolidates specifications, work items, and implementation results
- ✅ Prevents duplicate information across documentation
- ✅ Enables requirement supersession with full history preservation
- ✅ Supports globally unique numbering to prevent collisions
- ✅ Provides single source of truth for project specifications

## Key Features

### 1. RFC-Inspired Versioning
Requirements evolve over time. Track changes with:
- **Status:** ACTIVE, PROPOSED, SUPERSEDED
- **Version:** Semantic versioning (1.0, 1.1, 2.0)
- **Proposed Date:** When the requirement was created
- **Supersession:** References to new versions (old versions preserved)

### 2. Modular Organization
Split specifications into individual files rather than monolithic documents:
- **Architecture requirements** (REQ-A###)
- **Feature requirements** (REQ-F###)
- **Documentation requirements** (REQ-D###)
- Easy to version control, review, and parallel work

### 3. Unified Content
Each requirement file contains everything related to that requirement:
- Specification (description, rationale, key points)
- Current implementation status
- Work items (all tasks needed with priority, effort, acceptance criteria)
- Implementation results (if completed)
- Related requirements (cross-links)

### 4. Global Unique Numbering
Prevent number collisions across categories:
- Format: `[PREFIX]-[GLOBAL_NUMBER]`
- Example: REQ-A001, REQ-F005, REQ-D014
- Each number 001-999 used only once across all requirements
- Prevents confusion with duplicate numbers

### 5. Work Item Tracking
Tasks embedded in requirements with:
- Priority emoji (🔴 CRITICAL, 🟠 HIGH, 🟡 MEDIUM, 🟢 LOW)
- Status tracking (✅ DONE, ⏳ PENDING, 🔄 IN_PROGRESS)
- Effort estimates (hours or range)
- Acceptance criteria (checklist)
- Dependencies (what blocks this task)
- Related issues from analysis documents

## Directory Structure

```
spec/
├── README.md                          # Navigation hub
├── ARCHITECTURE.md                    # System architecture overview (with diagrams)
├── GAP_ANALYSIS.md          # Gap analysis (findings from review)
├── requirements/                      # SINGLE SOURCE OF TRUTH
│   ├── README.md                      # Index of all requirements
│   ├── architecture/                  # Architecture requirements
│   │   ├── REQ-A001.md
│   │   ├── REQ-A002.md
│   │   └── ...
│   ├── features/                      # Feature requirements
│   │   ├── REQ-F005.md
│   │   ├── REQ-F006.md
│   │   └── ...
│   └── documentation/                 # Documentation requirements
│       ├── REQ-D014.md
│       ├── REQ-D015.md
│       └── ...
```

## Requirement File Template

See `templates/REQ-TEMPLATE.md` for the standard structure each requirement should follow.

### Key Sections:
1. **Header:** Status, Version, Proposed date, Supersession info
2. **Description:** What is this requirement?
3. **Rationale:** Why is this important?
4. **Key Implementation Points:** How to build it
5. **Current Status:** ✅ Implemented or ⏳ Pending
6. **Work Items:** Tasks to implement this (embedded)
7. **Implementation Results:** What changed (if completed)
8. **Related Requirements:** Cross-links to other specs

## Naming Convention

### Categories
- **A** = Architecture requirements (infrastructure, patterns, design)
- **F** = Feature requirements (functionality, capabilities)
- **D** = Documentation requirements (docs, guides, specs)

### Numbering
- Format: `REQ-[CATEGORY][GLOBAL_NUMBER]`
- Examples: REQ-A001, REQ-A002, REQ-F003, REQ-D004
- **Global uniqueness:** Each number used only once across all categories
- Prevents: REQ-A001 and REQ-F001 (collision)
- Correct: REQ-A001 and REQ-F005 (unique)

### File Naming
- Format: `REQ-[CATEGORY][NUMBER].md`
- Example: `REQ-A001.md`, `REQ-F005.md`
- Match filename exactly with requirement header

## Work Item Structure

Each work item embedded in a requirement includes:

```
### 🔴 [WORK-ID]: [Title] — STATUS

**Priority:** 🔴 CRITICAL  
**Status:** ⏳ PENDING  
**Effort:** X hours or X-Y hour range  

**Description:** One sentence summary

**Problem:**
- What's broken or missing?
- Why does it matter?

**Solution:** 
- How to fix/implement it?
- What's the approach?

**Files to Change:**
- List files that need updates
- New files to create

**Acceptance Criteria:**
- [ ] Checklist item 1
- [ ] Checklist item 2
- [ ] Verification step

**Related Issues:** Reference to GAP_ANALYSIS.md findings

**Dependencies:** What must be done first (if any)
```

## Process: Adding a New Requirement

1. **Assign next global number:** Check existing REQ files, pick next unused number
2. **Choose category:** A (architecture), F (feature), or D (documentation)
3. **Create file:** `REQ-[CATEGORY][NUMBER].md`
4. **Use template:** Copy `templates/REQ-TEMPLATE.md`
5. **Fill sections:** Description, rationale, key points, work items
6. **Link in index:** Add to `requirements/README.md` index table
7. **Validate:** Check numbering is globally unique, links work
8. **Commit:** Git commit with clear message

## Process: Superseding a Requirement

When a requirement needs to change:

1. **Update header:** Set status to SUPERSEDED
2. **Add supersession info:** "Superseded by: REQ-X###"
3. **Create new version:** If significant changes, create REQ-[CAT][NUM]-v2.md
4. **Preserve old:** Keep old version for history
5. **Update work items:** Point to new requirement
6. **Update index:** Show both old and new
7. **Document why:** Explain reasoning for change

## Consistency Validation

The system enforces:
- ✅ **Unique numbering:** No duplicate numbers across categories
- ✅ **Naming convention:** Filename matches header exactly
- ✅ **Required sections:** All templates have Description, Rationale, Status, Work Items
- ✅ **Cross-references:** Links point to actual files
- ✅ **Status values:** Only ACTIVE, PROPOSED, SUPERSEDED
- ✅ **Work item format:** Priority, Status, Effort, Acceptance criteria

## Examples

See the `examples/` directory for real-world spec systems:
- **mfe-shell/** - Complete Angular+React federated architecture system (17 requirements)

## Integration with Copilot CLI

The `rfc-spec-init` skill uses this template system to:
- Create new spec directories in projects
- Migrate existing specifications
- Validate requirement consistency
- Generate requirement scaffolds

## Best Practices

1. **One requirement per file** - Modular, easier to version control
2. **Descriptive titles** - Clear what the requirement is
3. **Rationale matters** - Future developers need to understand why
4. **Work items are actionable** - Should be clear what to do
5. **Cross-link related** - Help navigation and understanding
6. **Keep superseded versions** - History is valuable for audit trails
7. **Status reflects reality** - Update status as work progresses
8. **Global uniqueness** - Prevent number collisions in conversations

## FAQ

**Q: Should I create one big REQUIREMENTS.md or split into files?**  
A: Always split into individual files. Easier to version control, review, and maintain.

**Q: How do I track work item progress?**  
A: Update the Status field in each work item: ⏳ PENDING → 🔄 IN_PROGRESS → ✅ DONE

**Q: Can I have 1000+ requirements?**  
A: Yes! Global numbering supports REQ-###.md (001-999). Organize into more categories if needed.

**Q: What if a requirement spans multiple categories?**  
A: Create separate requirements per category, use cross-links to connect them. For example, an architecture feature might be REQ-A001 (architecture) + REQ-F005 (feature) linked together.

**Q: How do I know when to supersede vs update?**  
A: Update in-place if it's a small clarification. Supersede if it's a material change (different approach, different implementation, breaking changes). Version numbers help.

---

**For more information:** See the complete methodology documentation in this directory and the `mfe-shell/` example.
