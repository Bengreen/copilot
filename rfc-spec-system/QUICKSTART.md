# RFC Specification System - Quick Start Guide

Get up and running with the RFC-style specification system in 5 minutes.

## What You Get

A specification system with:
- **Modular requirements** (one file per requirement)
- **Global unique numbering** (no collisions)
- **Unified content** (spec + work items + results in one file)
- **RFC-style versioning** (track changes and supersessions)
- **Architecture documentation** (system overview with diagrams)
- **Gap analysis** (centralized problem analysis)

## 5-Minute Setup

### Step 1: Create spec/ Directory

```bash
# In your project root
mkdir -p spec/requirements/{architecture,features,documentation}
```

### Step 2: Copy Core Files

```bash
# Copy templates from global RFC system
cp ~/.copilot/rfc-spec-system/README.md spec/
cp ~/.copilot/rfc-spec-system/REQ-TEMPLATE.md spec/

# Create key documents
touch spec/ARCHITECTURE.md
touch spec/GAP_ANALYSIS.md
touch spec/requirements/README.md
```

### Step 3: Create First Requirement

```bash
# Use template
cp spec/REQ-TEMPLATE.md spec/requirements/architecture/REQ-A001.md

# Edit REQ-A001.md with your first requirement
# Replace placeholders: [CATEGORY], [NUMBER], [Title], etc.
```

### Step 4: Update Index

Edit `spec/requirements/README.md`:

```markdown
# Requirements Index

## Overview
- **Total Requirements:** 1
- **Status:** 1 ACTIVE, 0 PROPOSED, 0 SUPERSEDED

## Architecture Requirements (REQ-A###)

| ID | Title | Status | Category |
|----|-------|--------|----------|
| [REQ-A001](architecture/REQ-A001.md) | Your Requirement Title | ACTIVE | Architecture |

## Feature Requirements (REQ-F###)

(None yet)

## Documentation Requirements (REQ-D###)

(None yet)
```

### Step 5: Commit

```bash
git add spec/
git commit -m "docs: Initialize RFC specification system"
```

**Done!** You now have a working spec system. 🎉

## What to Do Next

### Option 1: Add More Requirements

1. Create new file: `spec/requirements/features/REQ-F005.md`
2. Copy REQ-TEMPLATE.md structure
3. Fill in your requirement details
4. Update `spec/requirements/README.md` index
5. Commit

### Option 2: Populate ARCHITECTURE.md

Document your current system:

```markdown
# System Architecture

## High-Level Overview

[Describe your system at 30,000 feet]

## Key Components

[List main components and relationships]

## Technology Stack

[Frameworks, languages, tools]

## Deployment

[How the system runs]
```

### Option 3: Create GAP_ANALYSIS.md

Record issues and gaps discovered:

```markdown
# gap analysis

## Issues Discovered

### Issue #1: README is out of date
- **Severity:** HIGH
- **Location:** root/README.md
- **Description:** References outdated API endpoints
- **Affected Requirements:** REQ-D001

### Issue #2: Missing getting started guide
- **Severity:** MEDIUM
- **Location:** (missing)
- **Description:** New developers don't know how to start
- **Affected Requirements:** REQ-D002
```

Then create work items in requirements to address each issue.

## Understanding the Structure

```
spec/
├── README.md                         # Navigation hub (YOU ARE HERE)
├── ARCHITECTURE.md                   # System overview with diagrams
├── GAP_ANALYSIS.md         # Gap analysis
└── requirements/                     # SINGLE SOURCE OF TRUTH
    ├── README.md                     # Index of all requirements
    ├── architecture/                 # A-category requirements
    │   └── REQ-A001.md              # Your first requirement
    ├── features/                     # F-category requirements (to be added)
    └── documentation/                # D-category requirements (to be added)
```

## Common Tasks

### Creating a New Requirement

```bash
# 1. Decide: Is it architecture (A), feature (F), or documentation (D)?
# 2. Pick next global number (e.g., 002 if you already have 001)
# 3. Create file
cp spec/REQ-TEMPLATE.md spec/requirements/features/REQ-F005.md

# 4. Edit the file with your requirement
# 5. Update spec/requirements/README.md to add it to index
# 6. Commit
git add spec/
git commit -m "docs: Add REQ-F005 - Your Feature Title"
```

### Tracking Work Items

```markdown
## Work Items

### 🔴 WORK-001: Something to do — ⏳ PENDING

**Priority:** 🔴 CRITICAL
**Status:** ⏳ PENDING
**Effort:** 2-4 hours

**Problem:**
- What needs to be done?

**Solution:**
- How to do it?

**Acceptance Criteria:**
- [ ] Done
```

Update status as work progresses: ⏳ PENDING → 🔄 IN_PROGRESS → ✅ DONE

### Checking for Issues

Run validation script:

```bash
# Copy from global system
cp ~/.copilot/rfc-spec-system/validate-spec-system.sh .

# Run it
./validate-spec-system.sh

# Should see: "✅ All validations passed!"
```

## Key Concepts

### Status Values

| Status | Meaning | Use When |
|--------|---------|----------|
| ACTIVE | Currently implemented or being worked on | This is the current approach |
| PROPOSED | Planned for future implementation | We want to do this, but not yet |
| SUPERSEDED | Replaced by a newer requirement | We changed our approach |

### Global Unique Numbers

Each number (001-999) appears only once:

```
REQ-A001  ✅ Unique
REQ-F005  ✅ Unique (not REQ-F001)
REQ-D014  ✅ Unique (not REQ-D001)
```

Why? Prevents confusion in conversations about requirements.

### Categories

| Prefix | Type | Examples |
|--------|------|----------|
| A | Architecture | System design, patterns, infrastructure |
| F | Features | Functionality, capabilities, integrations |
| D | Documentation | Guides, specs, README files |

Feel free to add more: T (Testing), I (Infrastructure), P (Performance)...

## Common Mistakes

❌ **Don't:** Create one huge REQUIREMENTS.md
✅ **Do:** Split into individual REQ-###.md files

❌ **Don't:** Use the same number twice (REQ-A001 and REQ-F001)
✅ **Do:** Use unique global numbers (REQ-A001 and REQ-F005)

❌ **Don't:** Update work item status in separate WORK.md file
✅ **Do:** Update status directly in requirement file

❌ **Don't:** Keep broken cross-references
✅ **Do:** Validate all links work

## File Naming Rules

```
✅ CORRECT:
   - File: REQ-A001.md
   - Header: # REQ-A001: Title
   - Number: zero-padded (001, 002, not 1, 2)

❌ WRONG:
   - File: REQ-A-001.md (don't use dash)
   - File: REQ-a001.md (category must be uppercase)
   - File: REQ-A1.md (number must be 3 digits)
```

## When to Use Each Section

| Section | When to Use | Example |
|---------|-------------|---------|
| Description | Always | "Native Federation architecture..." |
| Rationale | Always | "Standards-compliant, supports mixed frameworks..." |
| Key Implementation Points | Always | "Uses @angular-architects/native-federation..." |
| Current Status | Always | "✅ Implemented" or "⏳ Proposed" |
| Work Items | If there's work to do | List all tasks with priority/effort |
| Implementation Results | If completed | Document what changed and UAT results |
| Related Requirements | If there are related specs | Cross-link to other REQ-###.md files |

## Need Help?

- **Understanding the methodology?** → Read `~/.copilot/rfc-spec-system/METHODOLOGY.md`
- **Validating your spec system?** → Read `~/.copilot/rfc-spec-system/VALIDATION.md`
- **See a real example?** → Check `~/.copilot/rfc-spec-system/examples/mfe-shell/`
- **Stuck on naming?** → See "File Naming Rules" section above

## Next Steps

1. **✅ Create your first requirement** (REQ-A001)
2. **Add a few more** as you identify them
3. **Document your architecture** in ARCHITECTURE.md
4. **Track issues** in GAP_ANALYSIS.md
5. **Create work items** for each task
6. **Use the system!** Update status as you work

---

**Questions?** Reference the full documentation in `~/.copilot/rfc-spec-system/`
