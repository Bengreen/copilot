---
name: gap-analysis
description: 'Comprehensive gap analysis across any area (documentation, architecture, features, processes, testing, infrastructure). Identifies issues, evaluates severity, links to requirements, and tracks resolution progress. Produces GAP_ANALYSIS.md file for project documentation and audit trail.'
---

# Comprehensive Gap Analysis Skill

## Overview

The Gap Analysis skill performs comprehensive analysis to identify gaps, issues, and discrepancies across any area of a project or system. It can analyze:

- **Documentation** - Missing docs, outdated content, unclear explanations
- **Architecture** - Design inconsistencies, missing diagrams, versioning issues
- **Features** - Incomplete implementations, missing edge cases, API inconsistencies
- **Processes** - Workflow gaps, unclear responsibilities, automation opportunities
- **Testing** - Coverage gaps, missing test types, untested scenarios
- **Infrastructure** - Deployment issues, monitoring gaps, configuration problems
- **Custom Areas** - Any project-specific concern

**Output:** Produces spec/GAP_ANALYSIS.md with all findings, severity levels, and links to requirements.

## Configuration Variables

${TARGET_AREA="Documentation|Architecture|Features|Processes|Testing|Infrastructure|[Custom]"} <!-- Area to analyze -->
${DEPTH="Quick Scan|Standard|Comprehensive|Deep Dive"} <!-- Analysis depth -->
${INCLUDE_RECOMMENDATIONS=true|false} <!-- Include fix recommendations -->
${LINK_TO_REQUIREMENTS=true|false} <!-- Link gaps to requirements -->
${AUTO_CREATE_REQUIREMENTS=false|true} <!-- Auto-create requirements for gaps -->
${SEVERITY_THRESHOLD="All|HIGH and above|CRITICAL only"} <!-- Which severities to include -->

## Generated Prompt

"Perform a comprehensive gap analysis on the specified area and document findings in spec/GAP_ANALYSIS.md:

### 1. Analysis Scope
- Target area: ${TARGET_AREA}
- Analysis depth: ${DEPTH}
- Consider: existing documentation, architecture, code, tests, processes, infrastructure

### 2. Gap Discovery
Identify gaps by:
- Comparing actual state vs. expected best practices
- Reviewing existing documentation for completeness
- Analyzing code for consistency and patterns
- Checking for missing processes or automation
- Evaluating test coverage and edge cases
- Assessing deployment and infrastructure setup
- **CRITICAL: Checking requirement cross-references for consistency**

Categories of gaps to look for:
- **Missing:** What should exist but doesn't
- **Incomplete:** What exists but is unfinished
- **Outdated:** What exists but is no longer accurate
- **Inconsistent:** What exists but conflicts with other areas
- **Unclear:** What exists but needs clarification
- **Broken:** What exists but doesn't work as expected
- **Broken References:** Requirements that reference non-existent files

### 3. Severity Assessment
For each gap, assign severity:
- 🔴 **CRITICAL** - Blocks other work, security/stability risk, requires immediate attention
- 🟠 **HIGH** - Significant impact, needed before release, blocks multiple items
- 🟡 **MEDIUM** - Moderate impact, improves quality/clarity, can be planned
- 🟢 **LOW** - Nice-to-have improvement, minimal impact, can be deferred

### 4. Documentation Structure
Create/update spec/GAP_ANALYSIS.md with:

\`\`\`
# GAP_ANALYSIS.md

**Analysis Date:** [TODAY]
**Analysis Type:** ${TARGET_AREA}
**Depth:** ${DEPTH}
**Status:** ACTIVE

## Executive Summary
- Total gaps found: [NUMBER]
- By severity: [breakdown]
- Blocking issues: [count]
- Recommendations: [count]

## Critical Issues (🔴)
### Gap #1: [Title]
- **Location:** [Where]
- **Status:** ⏳ PENDING
- **Description:** [What's missing]
- **Impact:** [Why it matters]
${INCLUDE_RECOMMENDATIONS ? "- **Recommended Fix:** [How to fix]" : ""}
${LINK_TO_REQUIREMENTS ? "- **Related Requirement:** [Link or REQ-### if exists]" : ""}

## High Priority Issues (🟠)
### Gap #[N]: [Title]
[Same structure as above]

## Medium Priority Issues (🟡)
### Gap #[N]: [Title]
[Same structure as above]

## Low Priority Issues (🟢)
### Gap #[N]: [Title]
[Same structure as above]

## Summary by Type
- Missing: [count]
- Incomplete: [count]
- Outdated: [count]
- Inconsistent: [count]
- Unclear: [count]
- Broken: [count]

## Resolution Path
| Gap # | Severity | Type | Status | Related Req |
|-------|----------|------|--------|-------------|
| #1 | 🔴 CRITICAL | Missing | ⏳ PENDING | [Link] |
| #2 | 🟠 HIGH | Incomplete | ⏳ PENDING | [Link] |
\`\`\`

### 5. Requirement Linking
${LINK_TO_REQUIREMENTS ? `For each gap, identify if a related requirement exists:
- If requirement exists: Link to it (e.g., "Related Requirement: REQ-D015")
- If no requirement: Note gap in "Action Items" section` : ""}

${AUTO_CREATE_REQUIREMENTS ? `### 6. Auto-Create Requirements
For CRITICAL and HIGH gaps without requirements:
- Create new requirement file: REQ-[CATEGORY][NUMBER].md
- Title: Gap summary
- Description: Full gap details from analysis
- Work Items: Include gap closure as first work item
- Status: PROPOSED
- Link back to this analysis` : ""}

### 7. Output Format
Use this structure for consistency:

**Status indicators:**
- ⏳ PENDING - Not started
- 🔄 IN_PROGRESS - Being worked on
- ✅ RESOLVED - Complete

**Severity emoji:**
- 🔴 CRITICAL
- 🟠 HIGH
- 🟡 MEDIUM
- 🟢 LOW

### 8. Validation Checklist
Before completing:
- ✓ All gaps documented with clear descriptions
- ✓ Severity levels assigned and justified
- ✓ Impact explained for each gap
- ✓ Recommendation provided (if enabled)
- ✓ Requirements linked (if applicable)
- ✓ Document date and analysis type recorded
- ✓ Status field indicates ACTIVE

### 9. Success Criteria
- spec/GAP_ANALYSIS.md created or updated with findings
- Each gap has: Title, Severity, Location, Status, Description, Impact
- Gaps are prioritized by severity
- Recommendations provided (if requested)
- Requirements linked or flagged for creation (if requested)
- Analysis is complete and traceable
- Next steps are clear for each gap

### 10. Next Steps Output
After analysis, provide:
- Summary of findings (count, severities)
- Top 3 critical/blocking items
- Recommended priority order
- Link to spec/GAP_ANALYSIS.md for full details
- Guidance for next action: 'Review gaps and create requirements for each'
- **CRITICAL: If any broken requirement references found, flag as CRITICAL issue**

## REFERENCE CONSISTENCY VALIDATION

**CRITICAL: Check for Broken Requirement References**

When analyzing Documentation area, ALWAYS check for broken references:

### Step 1: Detect Broken References
```bash
# Find all referenced requirements
grep -r "REQ-" spec/ | grep -oE "REQ-[A-Z][0-9]+" | sort -u > refs_found.txt

# Find all existing requirement files  
ls spec/requirements/*/REQ-*.md | sed 's/.*\(REQ-[A-Z][0-9]*\).*/\1/' | sort -u > reqs_exist.txt

# Find broken references
broken=$(comm -23 refs_found.txt reqs_exist.txt)
```

### Step 2: Report Broken References as CRITICAL Gap
If broken references found, add to GAP_ANALYSIS.md:

```
### Gap #[CRITICAL]: Broken Requirement References

**Severity:** 🔴 CRITICAL
**Location:** spec/requirements/
**Type:** Inconsistent
**Status:** ⏳ PENDING

**Description:**
The following requirements are referenced in the specification but their files do not exist:
- REQ-F001 (referenced in 5 files)
- REQ-F002 (referenced in 3 files)
- REQ-F003 (referenced in 4 files)

This creates broken links and inconsistent cross-references.

**Impact:**
- Team cannot navigate between related requirements
- Documentation is unreliable
- May indicate incomplete requirement planning

**Recommended Fix:**
For each broken reference, either:
1. Create the missing requirement file, OR
2. Remove/update the reference to link to existing file, OR
3. Convert to TODO marker for planned (not yet created) requirements

**Related Requirement:**
This is a documentation/process issue - create REQ-D###: "Fix broken requirement references"
```

### Step 3: Document Pattern for Future Prevention
Include in output:

**Prevention Guidance for Team:**
- ✅ Only reference requirements that exist
- ✅ Use TODO markers for planned requirements
- ✅ Update references when creating new requirements
- ✅ Run validation check before committing changes

### Reference Patterns (Correct vs. Incorrect):

**CORRECT:**
```markdown
- [REQ-A002: Shared Library](../path/REQ-A002.md)
```

**CORRECT (Planned):**
```markdown
- 📋 TODO: REQ-F005 - Planned requirement (not yet created)
```

**INCORRECT (Broken):**
```markdown
- [REQ-F001: Shell](REQ-F001.md)  ← File doesn't exist!
```

## Usage Examples

### Basic Gap Analysis
\`\`\`bash
@copilot-cli gap-analysis --area Documentation
\`\`\`
Analyzes documentation gaps with standard depth.

### Deep Dive Analysis
\`\`\`bash
@copilot-cli gap-analysis --area Architecture --depth comprehensive
\`\`\`
Comprehensive architecture analysis.

### With Recommendations
\`\`\`bash
@copilot-cli gap-analysis --area Testing --recommendations
\`\`\`
Testing gap analysis with fix recommendations.

### Auto-Create Requirements
\`\`\`bash
@copilot-cli gap-analysis --area Infrastructure --auto-requirements
\`\`\`
Analyze and auto-create requirements for gaps found.

### Quick Scan
\`\`\`bash
@copilot-cli gap-analysis --area Processes --depth quick
\`\`\`
Quick scan for process gaps.

## Integration with RFC System

This skill integrates with the RFC specification system:
- Gaps are documented in spec/GAP_ANALYSIS.md
- Each gap links to requirements (existing or new)
- Requirements track gap closure as work items
- Full audit trail of gap discovery and resolution
- Gaps inform requirement priorities

## Success Indicators
- ✅ Gaps identified across the specified area
- ✅ Issues ranked by severity
- ✅ Clear descriptions with impact analysis
- ✅ Linked to requirements (existing or flagged for creation)
- ✅ Gap_ANALYSIS.md updated with findings
- ✅ Team has clear visibility of issues
- ✅ Priority and next steps are obvious
"

