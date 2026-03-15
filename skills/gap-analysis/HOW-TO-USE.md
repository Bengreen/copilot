# Gap Analysis Skill - How to Use

## Overview

The gap-analysis skill performs comprehensive analysis to identify gaps across any area of your project. Each gap is documented, prioritized, and linked to requirements for tracking.

## When to Use Gap Analysis

Use this skill when you want to:
- Identify missing documentation
- Find architecture inconsistencies
- Discover incomplete features
- Locate process gaps
- Measure testing coverage gaps
- Find infrastructure issues
- Analyze any custom area

## Basic Usage

### Step 1: Identify Your Area

Decide what to analyze. Common options:
- **Documentation** - README files, API docs, guides
- **Architecture** - Design, patterns, diagrams
- **Features** - Completeness, edge cases, consistency
- **Processes** - Workflows, responsibilities, automation
- **Testing** - Coverage, test types, scenarios
- **Infrastructure** - Deployment, monitoring, config
- **Custom** - Any project-specific area

### Step 2: Run Analysis

```bash
@copilot-cli gap-analysis --area Documentation
```

The skill will:
1. Analyze the specified area
2. Identify gaps, issues, discrepancies
3. Evaluate severity for each gap
4. Link to existing requirements (if any)
5. Create spec/GAP_ANALYSIS.md with findings

### Step 3: Review Results

Open spec/GAP_ANALYSIS.md to see:
- Executive summary
- Gaps organized by severity
- Detailed description of each gap
- Impact and recommended fixes
- Links to related requirements
- Next steps

### Step 4: Take Action

For each gap:
1. Review description and impact
2. Prioritize by severity
3. Create or link to requirement
4. Assign to team member
5. Track progress

## Advanced Usage

### Comprehensive Analysis with Recommendations

```bash
@copilot-cli gap-analysis --area Architecture --depth comprehensive --recommendations
```

This will:
- Perform in-depth analysis
- Include detailed recommendations for fixes
- Cover all levels of detail
- Take longer but be more thorough

### Auto-Create Requirements for Gaps

```bash
@copilot-cli gap-analysis --area Infrastructure --auto-requirements
```

This will:
- Find CRITICAL and HIGH gaps
- Auto-create requirements for gaps without them
- Link each gap to its requirement
- Provide clear action items

### Quick Scan for Priority Issues Only

```bash
@copilot-cli gap-analysis --area Testing --depth quick --severity-threshold HIGH
```

This will:
- Do a quick scan (5-10 min vs 20-30 min)
- Only include HIGH and CRITICAL gaps
- Focus on blocking issues
- Provide quick priority overview

### Multiple Areas in Sequence

Analyze different areas at different times:

```bash
# Day 1: Documentation
@copilot-cli gap-analysis --area Documentation --recommendations

# Day 2: Architecture
@copilot-cli gap-analysis --area Architecture --depth comprehensive

# Day 3: Testing
@copilot-cli gap-analysis --area Testing --auto-requirements
```

Each analysis updates GAP_ANALYSIS.md with new findings.

## Detailed Workflow

### Workflow 1: Review and Plan

1. Run basic analysis:
   ```bash
   @copilot-cli gap-analysis --area [Area]
   ```

2. Review GAP_ANALYSIS.md:
   - Check executive summary
   - Identify CRITICAL/HIGH gaps
   - Understand impact

3. In team meeting:
   - Present findings
   - Discuss priorities
   - Plan work

4. Create requirements:
   - For each CRITICAL gap
   - For priority HIGH gaps
   - Link to GAP_ANALYSIS.md

5. Assign and track:
   - Assign work items to team
   - Update status in requirements
   - Track progress

### Workflow 2: Comprehensive Audit

1. Run comprehensive analysis:
   ```bash
   @copilot-cli gap-analysis --area [Area] --depth comprehensive --recommendations
   ```

2. Review all findings:
   - Note all gaps
   - Understand fixes
   - Plan approach

3. Create audit trail:
   - Document in GAP_ANALYSIS.md
   - Create requirements
   - Assign owners

4. Execute and close:
   - Complete each gap
   - Update status
   - Mark RESOLVED

### Workflow 3: Quick Priority Focus

1. Run quick scan:
   ```bash
   @copilot-cli gap-analysis --area [Area] --depth quick --severity-threshold HIGH
   ```

2. Handle blocking issues:
   - Address CRITICAL gaps immediately
   - Create requirements for HIGH gaps
   - Create emergency plan

3. Full analysis later:
   ```bash
   @copilot-cli gap-analysis --area [Area] --depth comprehensive
   ```

4. Complete all gaps:
   - CRITICAL first
   - HIGH next
   - MEDIUM/LOW as planned

## Example Analysis

### Scenario: Documentation Gap Analysis

```bash
@copilot-cli gap-analysis --area Documentation --recommendations
```

Output in spec/GAP_ANALYSIS.md:

```
# GAP_ANALYSIS.md

Analysis Type: Documentation
Analysis Date: 2026-03-15
Depth: Comprehensive

## Executive Summary
- Total gaps: 8
- CRITICAL: 1, HIGH: 2, MEDIUM: 3, LOW: 2
- Blocking issues: 1

## Critical Issues

### Gap #1: Missing API Documentation
- Location: mfe-shell-container/src/app/services/
- Description: SharedHttpService has no API documentation
- Impact: Developers cannot use service effectively
- Recommended Fix: Create docs/api/shared-http-service.md
- Status: PENDING

## High Priority Issues

### Gap #2: Outdated Setup Guide
...
```

Then create requirement:
- Title: "REQ-D018: Document SharedHttpService API"
- Work Item: "Create API documentation"
- Link: "Related to GAP_ANALYSIS.md Gap #1"

## Parameters Explained

### --area [Area]
Specifies what to analyze. Options:
- Documentation, Architecture, Features, Processes, Testing, Infrastructure
- Custom area name

### --depth [Level]
How thorough the analysis should be:
- **quick** - 5-10 minutes, obvious issues only
- **standard** - 15-20 minutes, comprehensive
- **comprehensive** - 30+ minutes, very thorough
- **deep** - 60+ minutes, exhaustive

### --recommendations
When enabled, each gap includes "How to fix" recommendations.

### --auto-requirements
When enabled:
- For each CRITICAL/HIGH gap without requirement
- Auto-creates new REQ-[CATEGORY][#].md file
- Links back to GAP_ANALYSIS.md

### --link-requirements
When enabled (default), gaps link to existing requirements.
Use `--no-link-requirements` to disable.

### --severity-threshold [Level]
Filter which gaps to include:
- **all** - Include all gaps
- **HIGH** - Include HIGH and CRITICAL only
- **CRITICAL** - Include CRITICAL only

## Tips and Best Practices

### Tip 1: Start with Documentation
Documentation gaps are usually easier to fix and provide quick wins.

```bash
@copilot-cli gap-analysis --area Documentation
```

### Tip 2: Use Recommendations for Planning
```bash
@copilot-cli gap-analysis --area [Area] --recommendations
```
This helps team understand what needs to be done.

### Tip 3: Auto-Create for Urgent Gaps
```bash
@copilot-cli gap-analysis --area [Area] --auto-requirements
```
This creates actionable requirements automatically.

### Tip 4: Deep Dive Before Major Release
```bash
@copilot-cli gap-analysis --area [Area] --depth comprehensive
```
Ensure nothing is missed before release.

### Tip 5: Quick Check Weekly
```bash
@copilot-cli gap-analysis --area [Area] --depth quick
```
Quick pulse check on priority issues.

## Common Questions

**Q: How long does analysis take?**
A: Depends on depth and area:
- Quick: 5-10 min
- Standard: 15-20 min
- Comprehensive: 30+ min

**Q: Can I analyze multiple areas?**
A: Yes, run multiple analyses. Each updates GAP_ANALYSIS.md with new findings.

**Q: How are gaps linked to requirements?**
A: If requirement exists, gap includes link. If not, gap is flagged as "Needs requirement".

**Q: Can I auto-create requirements?**
A: Yes, use `--auto-requirements` flag.

**Q: How do I track gap closure?**
A: Via requirements - each gap becomes work item with status tracking.

**Q: What if I disagree with a gap?**
A: Edit GAP_ANALYSIS.md to remove or update gaps. Document your rationale.

## Next Steps After Analysis

1. **Review** - Read spec/GAP_ANALYSIS.md thoroughly
2. **Discuss** - Team meeting to review findings
3. **Prioritize** - Decide what to fix first
4. **Create Requirements** - For CRITICAL and HIGH gaps
5. **Assign** - Give work to team members
6. **Track** - Update status as progress is made
7. **Close** - Mark RESOLVED when gaps are fixed
