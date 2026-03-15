# Gap Analysis Skill - Quick Reference

## One-Liner

Identify gaps across any area and generate spec/GAP_ANALYSIS.md with findings.

## Basic Usage

```bash
@copilot-cli gap-analysis --area [Area]
```

## Common Commands

| Task | Command |
|------|---------|
| Analyze Documentation | `@copilot-cli gap-analysis --area Documentation` |
| Analyze Architecture | `@copilot-cli gap-analysis --area Architecture` |
| Analyze Testing | `@copilot-cli gap-analysis --area Testing` |
| Analyze Processes | `@copilot-cli gap-analysis --area Processes` |
| Analyze Infrastructure | `@copilot-cli gap-analysis --area Infrastructure` |
| Comprehensive Analysis | `@copilot-cli gap-analysis --area [Area] --depth comprehensive` |
| With Recommendations | `@copilot-cli gap-analysis --area [Area] --recommendations` |
| Auto-Create Requirements | `@copilot-cli gap-analysis --area [Area] --auto-requirements` |
| Quick Scan Only | `@copilot-cli gap-analysis --area [Area] --depth quick` |

## Parameters

```
--area [Area]              Area to analyze (required)
--depth [Level]            Analysis depth: quick, standard, comprehensive, deep
--recommendations          Include fix recommendations
--auto-requirements        Auto-create requirements for gaps
--link-requirements        Link gaps to existing requirements (default: on)
--severity-threshold [L]   Filter: all, HIGH+, CRITICAL
```

## Output

Creates/updates: **spec/GAP_ANALYSIS.md**

Contains:
- Summary of findings
- Gaps organized by severity
- Impact and description for each
- Status tracking
- Links to related requirements

## Severity Levels

- **CRITICAL** (🔴) - Blocks work, immediate attention
- **HIGH** (🟠) - Significant impact, needed soon
- **MEDIUM** (🟡) - Moderate impact, can be planned
- **LOW** (🟢) - Nice-to-have, can be deferred

## Workflow

1. Run analysis: `@copilot-cli gap-analysis --area [Area]`
2. Review spec/GAP_ANALYSIS.md
3. Create requirements for CRITICAL/HIGH gaps
4. Track progress in requirements
5. Mark gaps RESOLVED when done

## Tips

- **Start with**: `@copilot-cli gap-analysis --area Documentation` to test
- **For priorities**: Use `--severity-threshold HIGH` to focus on critical items
- **For fixes**: Add `--recommendations` to get suggested fixes
- **For workflow**: Add `--auto-requirements` to auto-create requirements
- **For deep dive**: Use `--depth comprehensive` for thorough analysis

## FAQ

**Q: What areas can I analyze?**
A: Documentation, Architecture, Features, Processes, Testing, Infrastructure, or custom areas

**Q: Where does output go?**
A: spec/GAP_ANALYSIS.md in your project

**Q: Can it create requirements automatically?**
A: Yes, use `--auto-requirements` flag

**Q: How are gaps prioritized?**
A: By severity: CRITICAL > HIGH > MEDIUM > LOW

**Q: How do I track fixes?**
A: Link gaps to requirements, update status as work progresses

## Next Steps

After running gap analysis:
1. Review findings in spec/GAP_ANALYSIS.md
2. Prioritize by severity
3. Create requirements for CRITICAL/HIGH gaps
4. Assign work to team members
5. Track progress in requirements
