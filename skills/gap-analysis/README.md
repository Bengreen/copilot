# Gap Analysis Skill

Perform comprehensive gap analysis across any area of your project. Identify issues, evaluate severity, link to requirements, and track resolution.

## What It Does

The gap-analysis skill performs deep analysis to identify gaps in:
- **Documentation** - Missing, outdated, or unclear content
- **Architecture** - Design inconsistencies, missing diagrams
- **Features** - Incomplete implementations, missing edge cases
- **Processes** - Workflow gaps, unclear responsibilities
- **Testing** - Coverage gaps, missing test types
- **Infrastructure** - Deployment, monitoring, configuration issues
- **Custom Areas** - Any project-specific concerns

## Quick Start

Analyze any area:

```bash
@copilot-cli gap-analysis --area Documentation
```

## Output

Creates or updates **spec/GAP_ANALYSIS.md** with:
- All gaps discovered
- Severity levels (CRITICAL, HIGH, MEDIUM, LOW)
- Detailed descriptions and impact
- Status tracking
- Links to related requirements
- Clear next steps

## Usage Examples

### Analyze Documentation
```bash
@copilot-cli gap-analysis --area Documentation
```

### Analyze Architecture (Comprehensive)
```bash
@copilot-cli gap-analysis --area Architecture --depth comprehensive
```

### Analyze Testing with Recommendations
```bash
@copilot-cli gap-analysis --area Testing --recommendations
```

### Analyze Infrastructure and Auto-Create Requirements
```bash
@copilot-cli gap-analysis --area Infrastructure --auto-requirements
```

## Parameters

| Parameter | Options | Default |
|-----------|---------|---------|
| `--area` | Documentation, Architecture, Features, Processes, Testing, Infrastructure, Custom | Documentation |
| `--depth` | Quick, Standard, Comprehensive, DeepDive | Standard |
| `--recommendations` | Flag | Off |
| `--auto-requirements` | Flag | Off |
| `--link-requirements` | Flag | On |
| `--severity-threshold` | All, HIGH+, CRITICAL | All |

## Output Format

Each gap includes:
- Title - Clear description
- Severity - CRITICAL, HIGH, MEDIUM, LOW
- Location - Where the gap exists
- Status - PENDING, IN_PROGRESS, RESOLVED
- Description - What's missing/wrong
- Impact - Why it matters
- Category - Missing, Incomplete, Outdated, Inconsistent, Unclear, Broken
- Recommendation - How to fix (if enabled)
- Related Requirement - Link to REQ-### (if exists)

## Integration with RFC System

Works seamlessly with RFC specification system:
- Gaps stored in spec/GAP_ANALYSIS.md
- Each gap can link to requirements
- Auto-create requirements for CRITICAL/HIGH gaps
- Requirements track gap closure as work items
- Full audit trail and traceability

## Workflow

1. **Run Analysis**
   ```bash
   @copilot-cli gap-analysis --area [Area]
   ```

2. **Review Findings**
   - Check spec/GAP_ANALYSIS.md
   - Prioritize by severity
   - Understand impact

3. **Create Requirements** (if needed)
   - For CRITICAL/HIGH gaps without requirements
   - Use `--auto-requirements` to auto-create

4. **Track Progress**
   - Update gap status in GAP_ANALYSIS.md
   - Link work items in requirements
   - Close gaps as they're resolved

5. **Verify**
   - Mark gaps RESOLVED when complete
   - Update GAP_ANALYSIS.md with verification

## Questions?

See QUICK-REFERENCE.md or HOW-TO-USE.md for detailed usage.
