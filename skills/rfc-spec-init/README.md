# RFC Specification System Initializer Skill

**Skill Name:** `rfc-spec-init`  
**Type:** Custom Agent (General-Purpose)  
**Location:** `~/.copilot/skills/rfc-spec-init/`  
**Status:** ✅ Ready to use  

---

## Purpose

Initialize a new RFC-style specification system in any project with a single command.

## Usage

Invoke this skill from within Copilot CLI:

```
@copilot-cli rfc-spec-init
```

Or using the skill tool:

```bash
copilot-cli skill invoke rfc-spec-init --target [project-path]
```

## What It Does

The skill will:

1. ✅ Create the spec directory structure
   ```
   spec/
   ├── requirements/
   │   ├── architecture/
   │   ├── features/
   │   └── documentation/
   ```

2. ✅ Copy core templates
   - README.md (navigation hub)
   - ARCHITECTURE.md (system overview)
   - GAP_ANALYSIS.md (issue tracking)
   - requirements/README.md (index)

3. ✅ Create a starter requirement
   - REQ-A001.md template
   - Shows example structure
   - Ready to customize

4. ✅ Validate the setup
   - Check naming conventions
   - Verify directory structure
   - List next steps

5. ✅ Provide guidance
   - Explain how to use the system
   - Link to full documentation
   - Show example workflows

## Output

```
✅ RFC Specification System Initialized!

Created:
  📁 spec/
  📁 spec/requirements/architecture/
  📁 spec/requirements/features/
  📁 spec/requirements/documentation/
  📄 spec/README.md
  📄 spec/ARCHITECTURE.md
  📄 spec/GAP_ANALYSIS.md
  📄 spec/requirements/README.md
  📄 spec/requirements/architecture/REQ-A001.md

Next steps:
  1. Edit spec/requirements/architecture/REQ-A001.md with your first requirement
  2. Update spec/requirements/README.md index
  3. Read ~/.copilot/rfc-spec-system/QUICKSTART.md for details
  4. Commit: git add spec/ && git commit -m "docs: Initialize RFC specification system"

Documentation:
  • ~/.copilot/rfc-spec-system/START-HERE.md
  • ~/.copilot/rfc-spec-system/QUICKSTART.md
  • ~/.copilot/rfc-spec-system/METHODOLOGY.md
```

## Parameters

| Parameter | Type | Required | Default | Purpose |
|-----------|------|----------|---------|---------|
| `target` | string | No | Current directory | Project path to initialize |
| `categories` | string | No | A,F,D | Requirement categories to create |
| `force` | boolean | No | false | Overwrite existing spec/ |

## Examples

### Example 1: Initialize in current project
```bash
# In your project root
@copilot-cli rfc-spec-init
```

### Example 2: Initialize in specific project
```bash
@copilot-cli rfc-spec-init --target /path/to/project
```

### Example 3: Initialize with custom categories
```bash
@copilot-cli rfc-spec-init --categories A,F,D,T,I
# Creates: Architecture, Features, Documentation, Testing, Infrastructure
```

### Example 4: Force reinitialize
```bash
@copilot-cli rfc-spec-init --force
# Overwrites existing spec/ (careful!)
```

## What Gets Copied

From `~/.copilot/rfc-spec-system/`:

| Source | Destination | Purpose |
|--------|-------------|---------|
| README.md | spec/README.md | Navigation hub |
| ARCHITECTURE-TEMPLATE.md | spec/ARCHITECTURE.md | System overview |
| GAP-ANALYSIS-TEMPLATE.md | spec/GAP_ANALYSIS.md | Issue tracking |
| REQUIREMENTS-INDEX-TEMPLATE.md | spec/requirements/README.md | Index template |
| REQ-TEMPLATE.md | spec/requirements/architecture/REQ-A001.md | Starter requirement |

## After Initialization

Your project will have:

```
your-project/
├── spec/                             # NEW
│   ├── README.md                     # Navigation (from template)
│   ├── ARCHITECTURE.md               # System overview template
│   ├── GAP_ANALYSIS.md     # Issue tracking template
│   └── requirements/                 # SINGLE SOURCE OF TRUTH
│       ├── README.md                 # Requirements index
│       ├── architecture/             # Category for arch reqs
│       │   └── REQ-A001.md          # Starter requirement
│       ├── features/                 # Category for feature reqs
│       └── documentation/            # Category for doc reqs
├── ... (your existing project files)
```

## Next Steps After Init

1. **Edit first requirement:**
   ```bash
   cd spec/requirements/architecture
   vim REQ-A001.md
   # Fill in your first requirement
   ```

2. **Update index:**
   ```bash
   vim spec/requirements/README.md
   # Add your requirement to the index table
   ```

3. **Read documentation:**
   ```bash
   cat ~/.copilot/rfc-spec-system/QUICKSTART.md
   ```

4. **Commit:**
   ```bash
   git add spec/
   git commit -m "docs: Initialize RFC specification system"
   ```

## Validation

The skill validates:
- ✅ Directory structure created correctly
- ✅ All templates copied successfully
- ✅ Naming conventions followed (REQ-A001.md format)
- ✅ Files are readable and properly formatted
- ✅ Relative paths work correctly

If validation fails, clear error messages will guide you to fix issues.

## Error Handling

| Error | Cause | Solution |
|-------|-------|---------|
| "spec/ already exists" | Directory present | Use `--force` to overwrite or remove spec/ manually |
| "Permission denied" | Can't write to directory | Check write permissions on project root |
| "Templates not found" | Missing ~/.copilot/rfc-spec-system/ | Re-install RFC system: see START-HERE.md |

## Integration

This skill integrates with:
- Copilot CLI for invocation
- Global RFC system in `~/.copilot/rfc-spec-system/`
- Project git repository (optional but recommended)
- Project README (links to spec/ index)

---

## For Skill Developers

**Skill Type:** General-Purpose Agent  
**Model:** Sonnet (full reasoning capability)  
**Tools Available:** File operations, bash, directory creation  
**Output Format:** Structured with checkmarks and next steps  

See `SKILL-IMPLEMENTATION.md` for technical details.
