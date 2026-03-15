# Requirements Index Template

**Status:** ACTIVE  
**Last Updated:** [DATE]  

Master index of all requirements in this project. Each requirement is tracked with its current status, category, and links to the full specification.

---

## Overview

**Total Requirements:** [NUMBER]

| Status | Count |
|--------|-------|
| ✅ ACTIVE | [#] |
| 💡 PROPOSED | [#] |
| 🔄 SUPERSEDED | [#] |
| **TOTAL** | **[#]** |

**Work Items Status:**

| Status | Count |
|--------|-------|
| ✅ DONE | [#] |
| ⏳ PENDING | [#] |
| 🔄 IN_PROGRESS | [#] |
| 🚫 BLOCKED | [#] |
| **TOTAL** | **[#]** |

---

## Quick Navigation

### By Category

- **[Architecture Requirements](#architecture-requirements-req-a)** (REQ-A###) — 4 requirements
- **[Feature Requirements](#feature-requirements-req-f)** (REQ-F###) — 9 requirements
- **[Documentation Requirements](#documentation-requirements-req-d)** (REQ-D###) — 4 requirements

### By Status

- **[Active](#active-requirements)** — Currently implemented or in development
- **[Proposed](#proposed-requirements)** — Planned for future
- **[Superseded](#superseded-requirements)** — Replaced by newer version

---

## Architecture Requirements (REQ-A)

Infrastructure, patterns, system design.

| ID | Title | Status | Version | Work Items |
|----|-------|--------|---------|-----------|
| [REQ-A001](architecture/REQ-A001.md) | [Requirement Title] | ACTIVE | 1.0 | [Details] |
| [REQ-A002](architecture/REQ-A002.md) | [Requirement Title] | ACTIVE | 1.0 | [Details] |
| [REQ-A003](architecture/REQ-A003.md) | [Requirement Title] | ACTIVE | 1.0 | [Details] |
| [REQ-A004](architecture/REQ-A004.md) | [Requirement Title] | ACTIVE | 1.0 | [Details] |

---

## Feature Requirements (REQ-F)

Functionality, capabilities, integrations.

| ID | Title | Status | Version | Work Items |
|----|-------|--------|---------|-----------|
| [REQ-F005](features/REQ-F005.md) | [Requirement Title] | ACTIVE | 1.0 | [Details] |
| [REQ-F006](features/REQ-F006.md) | [Requirement Title] | ACTIVE | 1.0 | [Details] |
| [REQ-F007](features/REQ-F007.md) | [Requirement Title] | PROPOSED | 1.0 | [Details] |
| [REQ-F008](features/REQ-F008.md) | [Requirement Title] | ACTIVE | 1.0 | [Details] |
| [REQ-F009](features/REQ-F009.md) | [Requirement Title] | PROPOSED | 1.0 | [Details] |
| [REQ-F010](features/REQ-F010.md) | [Requirement Title] | ACTIVE | 1.0 | [Details] |
| [REQ-F011](features/REQ-F011.md) | [Requirement Title] | PROPOSED | 1.0 | [Details] |
| [REQ-F012](features/REQ-F012.md) | [Requirement Title] | PROPOSED | 1.0 | [Details] |
| [REQ-F013](features/REQ-F013.md) | [Requirement Title] | PROPOSED | 1.0 | [Details] |

---

## Documentation Requirements (REQ-D)

Guides, specifications, documentation.

| ID | Title | Status | Version | Work Items |
|----|-------|--------|---------|-----------|
| [REQ-D014](documentation/REQ-D014.md) | [Requirement Title] | ACTIVE | 1.0 | [Details] |
| [REQ-D015](documentation/REQ-D015.md) | [Requirement Title] | ACTIVE | 1.0 | [Details] |
| [REQ-D016](documentation/REQ-D016.md) | [Requirement Title] | PROPOSED | 1.0 | [Details] |
| [REQ-D017](documentation/REQ-D017.md) | [Requirement Title] | ACTIVE | 1.0 | [Details] |

---

## Active Requirements

Currently implemented or being developed.

### Architecture
- ✅ [REQ-A001: Requirement Title](architecture/REQ-A001.md)
- ✅ [REQ-A002: Requirement Title](architecture/REQ-A002.md)
- ✅ [REQ-A003: Requirement Title](architecture/REQ-A003.md)
- ✅ [REQ-A004: Requirement Title](architecture/REQ-A004.md)

### Features
- ✅ [REQ-F005: Requirement Title](features/REQ-F005.md)
- ✅ [REQ-F006: Requirement Title](features/REQ-F006.md)
- ✅ [REQ-F008: Requirement Title](features/REQ-F008.md)
- ✅ [REQ-F010: Requirement Title](features/REQ-F010.md)

### Documentation
- ✅ [REQ-D014: Requirement Title](documentation/REQ-D014.md)
- ✅ [REQ-D015: Requirement Title](documentation/REQ-D015.md)
- ✅ [REQ-D017: Requirement Title](documentation/REQ-D017.md)

---

## Proposed Requirements

Planned for future implementation.

### Features
- 💡 [REQ-F007: Requirement Title](features/REQ-F007.md)
- 💡 [REQ-F009: Requirement Title](features/REQ-F009.md)
- 💡 [REQ-F011: Requirement Title](features/REQ-F011.md)
- 💡 [REQ-F012: Requirement Title](features/REQ-F012.md)
- 💡 [REQ-F013: Requirement Title](features/REQ-F013.md)

### Documentation
- 💡 [REQ-D016: Requirement Title](documentation/REQ-D016.md)

---

## Superseded Requirements

Replaced by newer versions (kept for audit trail).

| Old | New | Reason |
|-----|-----|--------|
| [REQ-A005-v1](archive/REQ-A005-v1.md) | [REQ-A005-v2](architecture/REQ-A005-v2.md) | [Reason for supersession] |

---

## Dependency Map

Requirements that depend on other requirements:

```
REQ-A001 (Native Federation)
  ├─ REQ-A002 (Shared Library) — shares dependencies
  ├─ REQ-F005 (MFE1) — uses federation
  └─ REQ-F006 (MFE2) — uses federation

REQ-A002 (Shared Library)
  ├─ REQ-F005 (MFE1) — consumes shared library
  └─ REQ-F010 (Testing) — tests shared library

REQ-D014 (Main Documentation)
  ├─ REQ-D015 (Container READMEs)
  ├─ REQ-D016 (Architecture Spec)
  └─ REQ-D017 (Copilot Instructions)
```

See individual requirement files for detailed dependency information.

---

## Work Item Summary

### By Priority

**🔴 CRITICAL** (blocks other work)
- [Work-001: Title](requirements/documentation/REQ-D015.md#work-001-title)
- [Work-002: Title](requirements/documentation/REQ-D015.md#work-002-title)

**🟠 HIGH** (should do before release)
- [Work-003: Title](requirements/features/REQ-F008.md#work-003-title)
- [Work-004: Title](requirements/architecture/REQ-A004.md#work-004-title)

**🟡 MEDIUM** (should do)
- [Work-005: Title](requirements/features/REQ-F009.md#work-005-title)

**🟢 LOW** (nice to have)
- [Work-006: Title](requirements/documentation/REQ-D016.md#work-006-title)

### By Status

**✅ DONE**
- [Work-001: Title](requirements/documentation/REQ-D015.md#work-001-title) — Completed 2026-03-14

**🔄 IN_PROGRESS**
- [Work-002: Title](requirements/features/REQ-F008.md#work-002-title) — Started 2026-03-14

**⏳ PENDING**
- [Work-003: Title](requirements/architecture/REQ-A004.md#work-003-title)
- [Work-004: Title](requirements/documentation/REQ-D015.md#work-004-title)
- [Work-005: Title](requirements/documentation/REQ-D016.md#work-005-title)

**🚫 BLOCKED**
- [Work-006: Title](requirements/features/REQ-F010.md#work-006-title) — Waiting for [requirement]

---

## How to Use This Index

### Finding a Requirement

1. **Know the category?** → Go to that section (Architecture/Features/Documentation)
2. **Know the number?** → Use Ctrl+F to search for "REQ-A001"
3. **Need to browse?** → Check "By Status" sections

### Tracking Work

1. Check "Work Item Summary" for current status
2. Click on work item to see full details
3. Update status as work progresses

### Planning

1. Review "Proposed Requirements" for upcoming work
2. Check dependency map before starting
3. Prioritize based on dependency order

### Quality Assurance

1. Check each requirement has all required sections
2. Verify all cross-references are valid
3. Validate work item acceptance criteria
4. Review superseded versions for audit trail

---

## Statistics

### Completion Status

- **Fully Implemented:** [#] requirements
- **Partially Implemented:** [#] requirements
- **Proposed:** [#] requirements
- **Superseded:** [#] requirements

### Work Progress

- **Total Work Items:** [#]
- **Completed:** [#] ([#]%)
- **In Progress:** [#]
- **Pending:** [#]
- **Blocked:** [#]

### Effort Estimates

- **Total Estimated:** [#] hours
- **Work Completed:** [#] hours ([#]%)
- **Work In Progress:** [#] hours
- **Work Remaining:** [#] hours

---

## Legend

| Symbol | Meaning |
|--------|---------|
| ✅ | Complete / Done / Active |
| ⏳ | Pending / Waiting |
| 🔄 | In Progress / Superseded |
| 💡 | Proposed / Future |
| 🚫 | Blocked |
| 🔴 | Critical Priority |
| 🟠 | High Priority |
| 🟡 | Medium Priority |
| 🟢 | Low Priority |

---

## Related Documents

- **../README.md** — Navigation hub for this spec system
- **../ARCHITECTURE.md** — System architecture overview
- **../GAP_ANALYSIS.md** — Issues and gaps discovered
- **Individual REQ files** — Full specification for each requirement

---

**Last Updated:** [DATE]  
**Next Review:** [DATE]  
**Maintained By:** [Name/Team]
