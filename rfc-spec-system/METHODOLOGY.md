# RFC-Style Specification System - Methodology

**Complete Guide for Implementing and Using the RFC-Inspired Requirement System**

---

## What is an RFC-Inspired Requirement System?

RFC stands for "Request for Comments" - the IETF's process for documenting internet standards. This system adapts that approach for project specifications:

- **Living Documents:** Requirements evolve, change, and are superseded (not just deleted)
- **Versioned:** Each requirement has a version number and change history
- **Auditable:** Full history preserved - you can see why decisions were made
- **Modular:** Split into individual files, not monolithic documents
- **Unified:** Specification + work items + results all in one place

## Why Use This System?

### Problems It Solves

| Problem | Solution |
|---------|----------|
| "Which doc has the real info?" | Single source of truth per requirement |
| Duplicate info across WORK.md, REQUIREMENTS.md, TASKS | All unified in one file per requirement |
| "What changed and why?" | Full history preserved, supersession tracked |
| "I need to know work item status" | Embedded in requirement, always in sync |
| "Do we have REQ-001 and REQ-F001?" (collision) | Global unique numbering prevents this |
| "This requirement changed but nothing tracks why" | Version numbers + supersession reasoning |

### Benefits

✅ **Single Source of Truth** — No conflicting documentation  
✅ **Audit Trail** — Full history of decisions and changes  
✅ **Scalable** — Works with 10 or 1000 requirements  
✅ **Team Friendly** — Clear structure, everyone knows where to look  
✅ **Version Control Friendly** — Modular files = better diffs and reviews  
✅ **Enforceable** — Consistency rules prevent common mistakes  

## System Architecture

### Core Components

```
spec/
├── README.md                          # Navigation hub (entry point)
├── ARCHITECTURE.md                    # System architecture diagrams
├── GAP_ANALYSIS.md          # Analysis of issues/gaps discovered
│
└── requirements/                      # SINGLE SOURCE OF TRUTH
    ├── README.md                      # Index: Lists all 17+ requirements
    │
    ├── architecture/                  # Infrastructure, patterns, design
    │   ├── REQ-A001.md               # Native Federation Architecture
    │   ├── REQ-A002.md               # Shared Library Pattern
    │   ├── REQ-A003.md               # Shell Routing System
    │   └── REQ-A004.md               # Docker Deployment
    │
    ├── features/                      # Functionality, capabilities
    │   ├── REQ-F005.md               # MFE1 Remote
    │   ├── REQ-F006.md               # MFE2 Remote
    │   └── ... (REQ-F005 through REQ-F013)
    │
    └── documentation/                 # Guides, specs, docs
        ├── REQ-D014.md               # Root README
        ├── REQ-D015.md               # Container READMEs
        └── ... (REQ-D014 through REQ-D017)
```

### Three Core Documents

1. **GAP_ANALYSIS.md**
   - Records issues discovered (discrepancies, gaps)
   - Referenced by work items
   - Starting point for prioritization

2. **ARCHITECTURE.md**
   - System overview and diagrams
   - Component relationships
   - Technology stack
   - Deployment architecture

3. **requirements/README.md**
   - Index of all requirements
   - Quick search table
   - Cross-category overview

## Naming Convention

### Category Prefixes

| Prefix | Category | Examples |
|--------|----------|----------|
| **A** | Architecture | Patterns, infrastructure, system design |
| **F** | Feature | Functionality, capabilities, integrations |
| **D** | Documentation | Guides, READMEs, specifications |

**Extensible:** Add more categories as needed (T for Testing, I for Infrastructure, etc.)

### Global Unique Numbering

**Format:** `REQ-[CATEGORY][GLOBAL_NUMBER].md`

**Examples:**
```
REQ-A001.md  ← Architecture requirement #1
REQ-A002.md  ← Architecture requirement #2
REQ-F005.md  ← Feature requirement #5 (globally)
REQ-D014.md  ← Documentation requirement #14 (globally)
```

**Key Rule:** Each number 001-999 appears **only once** across all categories.

**Wrong:**  
```
REQ-A001.md  ❌ Collision!
REQ-F001.md
```

**Correct:**
```
REQ-A001.md  ✅ Unique across all
REQ-F005.md
```

**Why?** Prevents confusion in conversations ("Is it REQ-001 arch or feature?"). Globally unique numbers are unambiguous.

### File Naming Rules

1. Filename must match requirement ID exactly
   - ✅ REQ-A001.md
   - ❌ REQ-A-001.md
   - ❌ REQ-A1.md

2. First heading must match file name
   - File: `REQ-A001.md`
   - Header: `# REQ-A001: [Title]`

3. Lower case for category letter only
   - ✅ REQ-A001.md
   - ❌ REQ-a001.md

## Requirement File Structure

### 1. Header (Required)

```markdown
# REQ-A001: Native Federation Architecture

**Status:** ACTIVE  
**Version:** 1.0  
**Proposed:** 2026-03-14  
**Supersedes:** None  
**Superseded by:** None  
```

**Fields:**
- **Status:** ACTIVE | PROPOSED | SUPERSEDED
- **Version:** Semantic (1.0, 1.1, 2.0)
- **Proposed:** Date requirement created (YYYY-MM-DD)
- **Supersedes:** Previous version if updating
- **Superseded by:** Newer version if replaced

### 2. Description (Required)

Clear, concise explanation of what this requirement is.

```markdown
## Description

Standard-compliant module federation using Native Federation without 
Webpack dependency. Enables dynamic loading of multiple micro frontends 
(Angular and non-Angular) into a host shell application at runtime.
```

### 3. Rationale (Required)

Why this requirement matters. What problem does it solve?

```markdown
## Rationale

- Standards-compliant approach (not Webpack-specific)
- Supports both Angular and non-Angular remotes
- Enables configuration-driven MFE discovery
- Simplifies build and deployment process
- Aligns with industry best practices for federated architectures
```

### 4. Key Implementation Points (Required)

Specific technical guidance for implementers.

```markdown
## Key Implementation Points

- Uses `@angular-architects/native-federation` library
- Shell configuration at `mfe-shell-container/public/assets/contents/shell-config.json`
- Dynamic remote loading at runtime (remoteEntry.json per MFE)
- No code changes needed for new MFEs (configuration-driven)
- Supports both Angular and non-Angular frameworks (React, Vue, etc.)
```

### 5. Current Status (Required)

Is this implemented or still planned?

```markdown
## Current Status

✅ **Implemented**

The Native Federation architecture is fully operational:
- Shell bootstrap loads all remotes dynamically
- MFE1 (Angular) exposes routes via federation
- MFE2 (React) works via generic wrapper component
- Runtime configuration enables new MFEs without code changes
```

### 6. Work Items (Required if any work pending)

Tasks needed to implement or complete this requirement.

```markdown
## Work Items

### 🔴 DOC-001: Fix MFE1 Test Runner — ✅ DONE

**Priority:** 🔴 CRITICAL  
**Status:** ✅ DONE  
**Effort:** 0.25 hours (15 minutes)  

**Problem:**
- mfe1-container/README.md says "Vitest" but runs "Karma"

**Solution:** 
- Update README to show correct test runner
- Explain both Karma and Jasmine usage

**Acceptance Criteria:**
- [ ] README accurately describes test framework
- [ ] Example commands are correct and tested

**Related Issues:** GAP_ANALYSIS.md Issue #1 (CRITICAL severity)
```

### 7. Implementation Results (Optional, if completed)

What actually changed when work was completed?

```markdown
## Implementation Results

### Changes Made
- Updated mfe1-container/README.md with correct test runner info
- Added Karma/Jasmine testing examples
- Fixed confusing Vitest reference (applies to Shell only)

### UAT Results
- ✅ Developers can follow README to run tests
- ✅ Test output matches documentation
- ✅ No confusion about test frameworks

### Files Changed
- mfe1-container/README.md (updated)
```

### 8. Related Requirements (Recommended)

Cross-links to other related specs.

```markdown
## Related Requirements

- [REQ-A002: Shared Library Singleton Pattern](REQ-A002.md)
- [REQ-A003: Shell Dynamic Routing System](REQ-A003.md)
- [REQ-F010: MFE1 Remote](../features/REQ-F010.md)
```

## Work Item Format

### Standard Structure

```markdown
### 🔴 [ID]: [Title] — [STATUS]

**Priority:** [EMOJI] [PRIORITY_LEVEL]  
**Status:** [✅ DONE | ⏳ PENDING | 🔄 IN_PROGRESS]  
**Effort:** [Hours or range]  

**Description:** [One sentence]

**Problem:**
- [What's broken/missing]
- [Why matters]

**Solution:**
- [How to fix]
- [Approach]

**Files to Change:**
- `file1.ts`
- `file2.md`

**Acceptance Criteria:**
- [ ] Item 1
- [ ] Item 2
- [ ] Verification

**Related Issues:** [DOCUMENTATION_ANALYSIS reference]

**Dependencies:** [Blocking tasks or "None"]
```

### Priority Levels

| Icon | Level | Meaning |
|------|-------|---------|
| 🔴 | CRITICAL | Blocks other work, urgent, must do now |
| 🟠 | HIGH | Important, should do before release |
| 🟡 | MEDIUM | Should do, but not urgent |
| 🟢 | LOW | Nice to have, can defer |

### Status Values

| Icon | Status | Meaning |
|------|--------|---------|
| ✅ | DONE | Completed and verified |
| ⏳ | PENDING | Not started |
| 🔄 | IN_PROGRESS | Currently being worked on |

## Processes

### Process 1: Creating a New Requirement

**Step 1: Determine Requirements**
- What are you building? (description)
- Why build it? (rationale)
- What's the approach? (implementation points)

**Step 2: Assign Global Number**
```bash
# Check existing files
ls -la spec/requirements/*/REQ-*.md
# Pick next unused number (e.g., if you have A001-A004, F005-F013, D014-D016, 
# then next available is D017)
```

**Step 3: Create File**
```bash
# Create new file in appropriate category
touch spec/requirements/architecture/REQ-A005.md  # Or F###, D### as needed
```

**Step 4: Fill Template**
- Copy structure from REQ-TEMPLATE.md
- Fill all required sections (Description, Rationale, etc.)
- Add work items if needed
- Create cross-links to related requirements

**Step 5: Update Index**
- Edit `spec/requirements/README.md`
- Add new requirement to table
- Verify link works

**Step 6: Validate**
```bash
# Check numbering is globally unique
grep -r "^# REQ-.*###" spec/requirements/  # Look for duplicates

# Check filename matches header
# REQ-A005.md should have "# REQ-A005:" as first heading
```

**Step 7: Commit**
```bash
git add spec/requirements/*/REQ-A005.md spec/requirements/README.md
git commit -m "docs: Add REQ-A005 - [Title]

[Brief description of what requirement covers]

Co-authored-by: Copilot <223556219+Copilot@users.noreply.github.com>"
```

### Process 2: Superseding a Requirement

When a requirement needs to change significantly:

**Step 1: Update Original Requirement**
```markdown
**Status:** SUPERSEDED  
**Superseded by:** REQ-A005-v2

---

## Description

[Keep original description for historical reference]

---

## Supersession Reasoning

Changed because:
- Original approach proved ineffective
- New framework provides better solution
- Community feedback warranted revision
```

**Step 2: Create New Version** (if significant changes)
```markdown
# REQ-A005-v2: [Updated Title]

**Status:** ACTIVE  
**Version:** 2.0  
**Proposed:** 2026-03-15  
**Supersedes:** REQ-A005 (v1.0)
```

**Step 3: Update Cross-References**
- Search for links to old requirement
- Update to point to new version

**Step 4: Update Index**
- Mark old as SUPERSEDED
- Add new version to table

**Step 5: Commit**
```bash
git add spec/requirements/
git commit -m "docs: Supersede REQ-A005 with REQ-A005-v2

Reason for supersession:
- [Reason 1]
- [Reason 2]

Original REQ-A005 preserved for audit trail.

Co-authored-by: Copilot <223556219+Copilot@users.noreply.github.com>"
```

### Process 3: Tracking Work Item Progress

**Initial State:**
```markdown
### 🔴 DOC-001: Fix Test Runner — ⏳ PENDING
```

**In Progress:**
```markdown
### 🔴 DOC-001: Fix Test Runner — 🔄 IN_PROGRESS
```

**Completed:**
```markdown
### 🔴 DOC-001: Fix Test Runner — ✅ DONE
```

Update the requirement file as status changes. Commit periodically.

## Consistency Rules (Enforcement)

The system validates:

### Rule 1: Global Unique Numbering
- No two requirements can use the same number
- ❌ Both REQ-A001 and REQ-F001 invalid
- ✅ REQ-A001 and REQ-F005 valid

### Rule 2: Filename = Header Match
- Filename `REQ-A001.md` must have header `# REQ-A001: [Title]`
- Case sensitive, exact match
- Numbers must be zero-padded (001 not 1)

### Rule 3: Required Sections
Every requirement must have:
- Description
- Rationale
- Key Implementation Points
- Current Status
- Related Requirements

### Rule 4: Valid Status Values
Only these status values allowed:
- ACTIVE
- PROPOSED
- SUPERSEDED

### Rule 5: Work Item Format
If work items exist, each must have:
- ID (e.g., DOC-001)
- Priority (🔴🟠🟡🟢)
- Status (✅⏳🔄)
- Effort estimate
- Problem + Solution
- Acceptance Criteria

### Rule 6: Cross-Reference Validity
- All links must point to actual files
- Links must use correct relative paths
- No broken references

## Migration from Other Systems

### From Monolithic REQUIREMENTS.md

```bash
# 1. Split into category files
# OLD: One REQUIREMENTS.md (500 lines)
# NEW: 20 files (REQ-A001.md, REQ-F005.md, REQ-D014.md, etc.)

# 2. Assign global numbers (prevent collisions)
# A001-A004, F005-F013, D014-D017

# 3. Move work items into requirement files
# OLD: Separate WORK.md
# NEW: "Work Items" section in each REQ file

# 4. Create requirements/README.md index
```

### From Separate WORK_ITEMS.md

```bash
# 1. Map each work item to its requirement
# DOC-001 work belongs in REQ-D015

# 2. Move work item into requirement file
# As new "Work Items" section

# 3. Delete old WORK_ITEMS.md
```

### From README Scattered Issues

```bash
# 1. Create GAP_ANALYSIS.md
# Document all found issues

# 2. Create REQ-D### for each major documentation requirement
# Link to issues found

# 3. Create work items in REQ-D files
# Each work item references specific issues
```

## Best Practices

### ✅ DO

- ✅ Split into individual files (modular)
- ✅ Use globally unique numbers (prevents confusion)
- ✅ Cross-link related requirements (helps navigation)
- ✅ Update work item status as you progress
- ✅ Preserve superseded versions (audit trail)
- ✅ Write clear rationale (future developers need context)
- ✅ Make work items actionable (should be clear what to do)
- ✅ Validate consistency rules
- ✅ Commit regularly with clear messages

### ❌ DON'T

- ❌ Create one monolithic REQUIREMENTS.md
- ❌ Use duplicate numbers (REQ-A001 and REQ-F001)
- ❌ Delete superseded versions (need history)
- ❌ Have conflicting status in multiple files (single source of truth)
- ❌ Create requirements without description/rationale
- ❌ Leave broken cross-references
- ❌ Mix work tracking in different files
- ❌ Create vague work items (unclear acceptance criteria)

## Scaling Considerations

### Small Project (< 20 requirements)

```
spec/
└── requirements/
    └── REQ-A001 through REQ-F020 (all in flat list)
```

### Medium Project (20-100 requirements)

```
spec/
└── requirements/
    ├── architecture/
    ├── features/
    └── documentation/
```

### Large Project (> 100 requirements)

Consider adding more categories or sub-categories:

```
spec/
├── requirements/
│   ├── architecture/
│   ├── features/
│   ├── documentation/
│   ├── testing/
│   ├── infrastructure/
│   └── performance/
└── rfc-archive/  # Superseded versions
```

## FAQ

**Q: Can I have 1000+ requirements?**  
A: Yes. Global numbering supports REQ-###.md (001-999). Add more categories if needed.

**Q: What if a requirement doesn't fit any category?**  
A: Add a new category. Example: REQ-T### for Testing, REQ-I### for Infrastructure.

**Q: How do I handle versioning?**  
A: Use Version field in header (1.0, 1.1, 2.0). For major changes, create new file (REQ-###-v2.md) and mark old as SUPERSEDED.

**Q: What if work spans multiple requirements?**  
A: That's OK. Work item in each related requirement, with cross-links.

**Q: Can I use this without Git?**  
A: Yes, but you lose history. Recommended to use with version control.

**Q: How do I keep numbering consistent across teams?**  
A: Maintain a shared registry or use the rfc-spec-init skill to auto-assign numbers.

---

**Next Steps:** See README.md for setup instructions and links to examples.
