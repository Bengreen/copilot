---
name: rfc-spec-init
description: 'RFC-inspired specification system initialization. Scaffolds a complete, production-ready specification system for any project in under 1 minute. Creates modular requirements structure with RFC versioning, templates, architecture documentation, and tracking capabilities. Zero configuration needed.'
---

# RFC Specification System Initializer

## Overview

The RFC Spec Init skill scaffolds a complete specification system in any project. It creates:
- Modular requirements directory (architecture, features, documentation categories)
- RFC-inspired versioning and tracking  
- Starter requirement file (REQ-A001.md)
- Architecture template
- Full documentation index

**Time:** < 1 minute  
**Result:** Production-ready specification system

## Configuration Variables

${TARGET_DIR="current project|/path/to/project"} <!-- Where to initialize the system -->
${FORCE_OVERWRITE=false|true} <!-- Overwrite existing spec/ directory if present -->
${CATEGORIES="A,F,D"|custom list} <!-- Requirement categories (Architecture, Features, Documentation, etc.) -->
${INCLUDE_EXAMPLES=true|false} <!-- Include example requirements -->
${START_NUMBER=1} <!-- Starting number for first requirement -->

## Generated Prompt

"Initialize a complete RFC specification system in the target project using the provided templates and guidelines:

### 1. Project Setup
- Target directory: ${TARGET_DIR == "current project" ? "Initialize in current working directory" : "Initialize in ${TARGET_DIR}"}
- Create spec/ directory structure if it doesn't exist
${FORCE_OVERWRITE ? "- WARNING: Will overwrite existing spec/ directory - confirm this is intended" : "- If spec/ exists, verify structure and update only missing files"}

### 2. Directory Structure
Create the following structure:

\`\`\`
spec/
├── README.md                           # Navigation hub
├── ARCHITECTURE.md                     # System architecture template
├── GAP_ANALYSIS.md           # Issue tracking template  
└── requirements/
    ├── README.md                       # Requirements index
    ├── architecture/                   # REQ-A### files
    ├── features/                       # REQ-F### files
    └── documentation/                  # REQ-D### files (+ more as needed)
\`\`\`

### 3. File Creation
Using the templates from ~/.copilot/rfc-spec-system/:

1. **spec/README.md** - Use REQUIREMENTS-INDEX-TEMPLATE.md as base, customize for this project
2. **spec/ARCHITECTURE.md** - Use ARCHITECTURE-TEMPLATE.md template
3. **spec/GAP_ANALYSIS.md** - Use GAP-ANALYSIS-TEMPLATE.md template
4. **spec/requirements/README.md** - Use REQUIREMENTS-INDEX-TEMPLATE.md for requirements index
5. **spec/requirements/architecture/REQ-A001.md** - Create starter requirement using REQ-TEMPLATE.md

### 4. Template Customization
- Replace [PROJECT_NAME] with actual project name
- Update descriptions to match project context
- Set initial status to PROPOSED for REQ-A001
- Customize categories based on ${CATEGORIES}

### 5. Validation
Before completing, verify:
- ✓ All required directories exist
- ✓ All template files created
- ✓ All cross-references are valid
- ✓ README files have correct structure
- ✓ REQ-A001.md is properly formatted

**CRITICAL: Global Number Uniqueness Validation**
The RFC system uses GLOBAL unique numbering where each number (001-999) can appear ONLY ONCE across ALL categories:
- REQ-A001, REQ-A002, ... (Architecture)
- REQ-F005, REQ-F006, ... (Features)  
- REQ-D014, REQ-D015, ... (Documentation)
- Plus any custom categories

Before accepting any requirement number, validate:
- ✓ The number (e.g., "001", "005", "014") is NOT already used in ANY category
- ✓ Check all existing requirements across all categories
- ✓ If number is taken, find next available unique number
- ✓ Ensure no REQ-A001 AND REQ-F001 can coexist (001 is globally unique)

How to check:
```bash
# Extract all requirement numbers globally
ls spec/requirements/*/REQ-*.md | sed 's/.*REQ-[A-Z]\([0-9]*\).*/\1/' | sort -u > numbers_used.txt

# Extract unique numbers only (no duplicates)
sort -u numbers_used.txt > unique_numbers.txt

# Check if any number is duplicated
if [ $(wc -l < numbers_used.txt) -ne $(wc -l < unique_numbers.txt) ]; then
  echo "ERROR: Duplicate numbers found across categories!"
  comm -3 numbers_used.txt unique_numbers.txt
fi
```

Example of WRONG (duplicate numbers across categories):
  ❌ REQ-A001 (Architecture)
  ❌ REQ-F001 (Features) - DUPLICATE! Number 001 already used
  
Example of CORRECT (unique numbers globally):
  ✅ REQ-A001 (Architecture)
  ✅ REQ-F005 (Features) - 005 is unique
  ✅ REQ-D014 (Documentation) - 014 is unique

**CRITICAL: Cross-Reference Validation**
When creating starter requirements (REQ-A001.md):
- ✓ ANY reference to another requirement (e.g., "REQ-A002", "REQ-F005") MUST point to an actual file that exists
- ✓ Do NOT create placeholder references to non-existent files
- ✓ Only reference requirements that exist in the project
- ✓ If a related requirement doesn't exist yet, mark as "TODO: Create REQ-###" or use text description instead
- ✓ Use this pattern ONLY for existing files:
  ```markdown
  - [REQ-A002: Related Requirement](../path/to/REQ-A002.md)
  ```
- ✓ Use this pattern for planned but non-existent requirements:
  ```markdown
  - TODO: REQ-F005 (Planned requirement - not yet created)
  - Related: Feature - Component B integration (planned for Phase 2)
  ```

### 6. Output & Next Steps
On success, display:
- Summary of created files and directories
- Quick start instructions
- Link to spec/README.md
- Next steps: 'Edit spec/requirements/architecture/REQ-A001.md to add your first requirement'
- Link to ~/.copilot/rfc-spec-system/START-HERE.md for full documentation

On error, show:
- Clear error message
- Location where error occurred
- Suggested fix
- Contact/feedback instructions

### 7. Integration
- Confirm system is using templates from ~/.copilot/rfc-spec-system/
- Verify skill is reusable across projects
- No hardcoded paths or project-specific references
- System should work identically in any project

## Key Features
- **Zero Configuration:** Just invoke, it works
- **Autonomous:** Handles all scaffolding automatically
- **Reusable:** Works in any project, any time
- **Integrated:** Uses global RFC system templates
- **Fast:** Complete in < 1 minute
- **Validated:** Checks everything before completion
- **Reference-Safe:** Prevents broken cross-references (only links to existing files)
- **Globally Unique Numbers:** Ensures each number is unique across ALL categories (A, F, D, etc.)

## Usage Examples

### Basic Usage
\`\`\`bash
@copilot-cli rfc-spec-init
\`\`\`
Initializes in current project directory.

### Specific Project
\`\`\`bash
@copilot-cli rfc-spec-init --target /path/to/project
\`\`\`
Initializes in specified directory.

### Force Overwrite
\`\`\`bash
@copilot-cli rfc-spec-init --force
\`\`\`
Overwrites existing spec/ directory if present.

### Custom Categories
\`\`\`bash
@copilot-cli rfc-spec-init --categories A,F,D,T,I
\`\`\`
Creates categories: Architecture (A), Features (F), Documentation (D), Testing (T), Infrastructure (I).

## Success Criteria
- spec/ directory created with all subdirectories
- 8 files created (README.md files + 3 templates + REQ-A001.md)
- All cross-references valid (CRITICAL: No broken references to non-existent files)
- All requirement numbers globally unique (CRITICAL: No duplicate numbers across categories)
- Next steps clearly communicated
- User can immediately start editing REQ-A001.md

## Integration Notes
- Skill is stateless—each invocation is independent
- All templates loaded from ~/.copilot/rfc-spec-system/
- No modifications to any templates
- System works identically whether first time or Nth time in projects

## IMPORTANT: Requirement Number & Reference Consistency Guidelines

**CRITICAL RULE #1: Global Number Uniqueness**

Every requirement number (001-999) can appear ONLY ONCE across ALL categories:
- REQ-A001 - number 001 is used (globally unique)
- REQ-F001 would DUPLICATE number 001 (NOT ALLOWED)
- REQ-F005 - number 005 is unique (allowed)
- REQ-D014 - number 014 is unique (allowed)

This means:
- ✅ REQ-A001, REQ-F005, REQ-D014 (different numbers, valid)
- ❌ REQ-A001, REQ-F001 (same number 001, INVALID)
- ❌ REQ-D005, REQ-F005 (same number 005, INVALID)

### When Adding New Requirements:
1. Check all existing requirements across ALL categories
2. Extract all numbers currently in use (001-999)
3. Find next available unique number
4. Use that number with the appropriate category prefix

Example workflow:
```bash
# Check existing numbers
ls spec/requirements/*/REQ-*.md | sed 's/.*REQ-[A-Z]\([0-9]*\).*/\1/' | sort -n

# If you see: 001 002 003 004 005 006 007 008 009 010 011 012 013 014 015 016 017
# Next available: 018
# Create: REQ-[CATEGORY]018.md (e.g., REQ-F018.md, REQ-D018.md, etc.)
```

### Validation Check:
```bash
# Find all requirement numbers (no category prefix)
ls spec/requirements/*/REQ-*.md | sed 's/.*REQ-[A-Z]\([0-9]*\).*/\1/' | sort > all_numbers.txt

# Check for duplicates (should be zero)
if [ $(wc -l < all_numbers.txt) -ne $(sort -u all_numbers.txt | wc -l) ]; then
  echo "ERROR: Duplicate numbers found!"
  sort | uniq -d all_numbers.txt
fi
```

**CRITICAL RULE #2: Reference Consistency**

Every requirement reference in the system MUST point to an existing file.

### When Creating Requirements:
- ✅ DO reference other requirements IF those files exist
- ✅ DO use "Related Requirements" section to link to existing files
- ✅ DO mark TODO references that will be created later
- ❌ DO NOT create "broken" references to non-existent files
- ❌ DO NOT reference REQ-### that don't exist yet

### Reference Pattern Examples:

**CORRECT - File exists:**
```markdown
## Related Requirements
- [REQ-A002: Shared Library](../architecture/REQ-A002.md)
- [REQ-F005: Shell Loading](../features/REQ-F005.md)
```

**CORRECT - File planned but doesn't exist yet:**
```markdown
## Related Requirements
- ✅ [REQ-A002: Shared Library](../architecture/REQ-A002.md) - EXISTS
- 📋 TODO: REQ-F005 - Planned (Shell loading) - NOT YET CREATED
- 📋 TODO: REQ-F006 - Planned (MFE1 Loading) - NOT YET CREATED
```

**WRONG - Broken reference:**
```markdown
- [REQ-F001: MFE Shell](REQ-F001.md)  ← This file doesn't exist!
```

### Best Practices for Reference Maintenance:

1. **When Initializing (rfc-spec-init):**
   - Only create references in starter file if target files exist
   - Use TODO markers for planned but non-existent requirements

2. **When Adding New Requirements:**
   - Update all existing requirements that reference this new requirement
   - Change TODO→ [LINK] to create the cross-reference
   - Test that links work (files exist before linking)

3. **When Deleting Requirements:**
   - Search for all references to the requirement being deleted
   - Remove or update those references
   - Never leave broken links

4. **Regular Maintenance:**
   - Use validation script: `@copilot-cli gap-analysis --area Documentation` includes reference validation
   - Check spec/GAP_ANALYSIS.md for "Broken Reference" issues
   - Fix broken references immediately

5. **Team Communication:**
   - When planning requirements: List them as TODO first
   - When creating requirements: Update all TODO→ LINK references
   - Document requirement dependencies clearly

### How to Validate References (Manual Check):

```bash
# Find all referenced requirements
grep -r "REQ-" spec/ | grep -oE "REQ-[A-Z][0-9]+" | sort -u > refs_found.txt

# Find all existing requirement files
ls spec/requirements/*/REQ-*.md | sed 's/.*\(REQ-[A-Z][0-9]*\).*/\1/' | sort -u > reqs_exist.txt

# Find broken references (mentioned but don't exist)
comm -23 refs_found.txt reqs_exist.txt
```

### If You Find Broken References:

1. Run the validation check above
2. For each broken reference:
   - Option A: Create the missing requirement file
   - Option B: Remove or update the reference to a TODO marker
   - Option C: Link to related existing requirement instead
3. Update GAP_ANALYSIS.md to mark as RESOLVED
4. Commit with message: "docs: Fix broken requirement references"
"

