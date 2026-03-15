# GAP_ANALYSIS.md Template

**Analysis Date:** [DATE]  
**Last Updated:** [DATE]  
**Status:** ACTIVE  
**Analysis Type:** [Documentation | Architecture | Features | Process | Testing | Infrastructure | Other]

This document records gaps, issues, and discrepancies discovered during comprehensive analysis. Gaps can span documentation, architecture, features, processes, testing coverage, infrastructure, or any other area. Each issue is tracked and linked to requirements/work items for resolution.

---

## Executive Summary

**Total Issues Found:** [NUMBER]

| Severity | Count | Status |
|----------|-------|--------|
| 🔴 CRITICAL | [#] | [# unresolved] |
| 🟠 HIGH | [#] | [# unresolved] |
| 🟡 MEDIUM | [#] | [# unresolved] |
| 🟢 LOW | [#] | [# unresolved] |

**Quick Stats:**
- Issues that block other work: [#]
- Issues that are nice-to-have: [#]
- Issues in progress: [#]
- Issues resolved: [#]

---

## Critical Issues (🔴)

### Issue #1: [Issue Title]

**Severity:** 🔴 CRITICAL  
**Location:** [File path or area]  
**Status:** ⏳ PENDING | 🔄 IN_PROGRESS | ✅ RESOLVED  

**Description:**
[What's wrong? Be specific.]

**Impact:**
- [Who is affected?]
- [What breaks?]
- [Why is it urgent?]

**Example/Evidence:**
[Show the problem with concrete examples or screenshots]

**Root Cause:**
[Why does this problem exist?]

**Related Work Item:**
[Link to requirement that will fix this]  
Example: REQ-D015: [Title](requirements/documentation/REQ-D015.md)

---

### Issue #2: [Issue Title]

[Repeat structure for each critical issue]

---

## High Priority Issues (🟠)

### Issue #[N]: [Issue Title]

**Severity:** 🟠 HIGH  
**Location:** [File path]  
**Status:** ⏳ PENDING | 🔄 IN_PROGRESS | ✅ RESOLVED  

**Description:**
[What's wrong?]

**Impact:**
- [Consequences]

**Related Work Item:**
[REQ-### that addresses this](link)

---

### Issue #[N+1]: [Issue Title]

[Repeat for each high-priority issue]

---

## Medium Priority Issues (🟡)

### Issue #[N]: [Issue Title]

**Severity:** 🟡 MEDIUM  
**Location:** [File path]  
**Status:** ⏳ PENDING | 🔄 IN_PROGRESS | ✅ RESOLVED  

**Description:**
[What's missing or unclear?]

**Impact:**
- [Moderate consequences]

**Related Work Item:**
[REQ-### that addresses this](link)

---

## Low Priority Issues (🟢)

### Issue #[N]: [Issue Title]

**Severity:** 🟢 LOW  
**Location:** [File path]  
**Status:** ⏳ PENDING | 🔄 IN_PROGRESS | ✅ RESOLVED  

**Description:**
[Nice-to-have improvement]

**Related Work Item:**
[REQ-### if applicable](link)

---

## Issue Categories

### By Type

#### Outdated Information
- [Issue #X: ...](section-above)
- [Issue #Y: ...](section-above)

#### Missing Documentation
- [Issue #X: ...](section-above)
- [Issue #Y: ...](section-above)

#### Inconsistency
- [Issue #X: ...](section-above)
- [Issue #Y: ...](section-above)

#### Unclear/Confusing
- [Issue #X: ...](section-above)
- [Issue #Y: ...](section-above)

#### Broken Links/References
- [Issue #X: ...](section-above)
- [Issue #Y: ...](section-above)

### By Location

#### Root Directory
- [Issue #X: README.md](section-above)
- [Issue #Y: Configuration](section-above)

#### Source Code Documentation
- [Issue #X: Code comments](section-above)

#### API Documentation
- [Issue #Y: API docs](section-above)

#### Deployment Documentation
- [Issue #Z: Docker, Kubernetes](section-above)

---

## Resolution Tracking

### Status Summary

| Issue | Status | Assigned To | Target Date |
|-------|--------|-------------|-------------|
| [Issue #1](section-above) | ⏳ PENDING | [Name] | [Date] |
| [Issue #2](section-above) | 🔄 IN_PROGRESS | [Name] | [Date] |
| [Issue #3](section-above) | ✅ RESOLVED | [Name] | [Date] |

### Progress Chart

```
PENDING:      ████░░░░░░ 40%  (Issues #1, #5, #7, #9)
IN_PROGRESS:  ██░░░░░░░░  20%  (Issues #2, #6)
RESOLVED:     ██░░░░░░░░  20%  (Issues #3, #4)
BLOCKED:      ██░░░░░░░░  20%  (Issues #8, #10)
```

---

## How Issues Link to Requirements

Each issue found should map to a requirement that will resolve it:

```
Issue Found
    ↓
Create Work Item in Requirement
    ↓
Document in "Work Items" section
    ↓
Link back from this analysis doc
    ↓
Resolve and mark ✅ DONE
    ↓
Update this analysis doc
```

### Mapping

| Issue | Category | Related Requirement | Work Item |
|-------|----------|-------------------|-----------|
| #1 | Documentation | REQ-D014 | DOC-001 |
| #2 | Missing | REQ-D015 | DOC-002 |
| #3 | Outdated | REQ-D014 | DOC-003 |

---

## How to Use This Document

### For Project Managers
1. Check "Executive Summary" for overall status
2. Review Critical/High issues for blocking items
3. Use "Status Summary" to track progress
4. Report on "Progress Chart" in standups

### For Developers
1. Find an unresolved issue
2. Look up the "Related Work Item"
3. Open the requirement file (e.g., REQ-D015.md)
4. See the work item details
5. Complete the work
6. Update status: ⏳ → 🔄 → ✅

### For QA
1. Check resolved issues (✅ status)
2. Verify the fix addresses the problem
3. Confirm from this document that issue is resolved

### For Documentation
1. Review all issues in your area
2. Plan work to address them
3. Collaborate with developers on fixes

---

## When to Update This Document

- ✅ When you find a new issue: Add it with details
- ✅ When work on an issue starts: Change status to 🔄 IN_PROGRESS
- ✅ When work is complete: Change status to ✅ RESOLVED and verify fix
- ✅ When context changes: Update description or impact
- ✅ Weekly: Review and update status summary

---

## Notes for Reviewers

[Any notes for people reading this analysis?]

- [Consideration 1]
- [Consideration 2]
- [Known limitations of this analysis]

---

## Related Documents

- **requirements/README.md** - Index of all 17+ requirements
- **requirements/architecture/REQ-A###.md** - Architecture requirements
- **requirements/features/REQ-F###.md** - Feature requirements
- **requirements/documentation/REQ-D###.md** - Documentation requirements
- **ARCHITECTURE.md** - System architecture overview

---

**Analysis conducted by:** [Name/Team]  
**Next review date:** [Date]  
**Point of contact:** [Name, Email]
