# RFC Specification System - Consistency Validation Guide

Quick reference for validating requirement files and spec systems.

## CRITICAL: Global Number Uniqueness

**Each requirement number (001-999) MUST be unique across ALL categories.**

### Number Uniqueness Validation Checklist

- [ ] **Each number (001-999) appears only ONCE globally**
- [ ] **No REQ-A001 AND REQ-F001 (same number in different categories)**
- [ ] **New requirements use next available unique number**
- [ ] **Run uniqueness validation before committing**

### How to Validate Global Number Uniqueness

Run this before committing:

```bash
# Extract all requirement numbers from all categories
ls spec/requirements/*/REQ-*.md | sed 's/.*REQ-[A-Z]\([0-9]*\).*/\1/' | sort > all_numbers.txt

# Check for duplicates
duplicates=$(sort all_numbers.txt | uniq -d)

if [ -n "$duplicates" ]; then
  echo "ERROR: Duplicate requirement numbers found:"
  echo "$duplicates"
  
  # Show which files have the duplicate numbers
  for dup in $duplicates; do
    echo "Number $dup is used in:"
    ls spec/requirements/*/REQ-*$dup.md
  done
  
  exit 1
fi

echo "✅ All numbers are globally unique"
```

### Valid Examples:

**CORRECT - All numbers globally unique:**
```
REQ-A001, REQ-A002, REQ-A003, REQ-A004  (numbers 001-004)
REQ-F005, REQ-F006, REQ-F007, REQ-F008  (numbers 005-008)
REQ-D014, REQ-D015, REQ-D016, REQ-D017  (numbers 014-017)
```

Each number (001, 002, 003... 017) appears exactly ONCE globally.

### Invalid Examples:

**WRONG - Duplicate numbers across categories:**
```
REQ-A001, REQ-F001  ← DUPLICATE! Number 001 used twice
REQ-D005, REQ-F005  ← DUPLICATE! Number 005 used twice
```

This violates the global uniqueness rule.

## CRITICAL: Cross-Reference Validation

**ALL requirement references MUST point to existing files.**

### Reference Validation Checklist

- [ ] **Every REQ-### reference in the system points to an actual file**
- [ ] **No broken links to non-existent requirements**
- [ ] **If requirement doesn't exist yet, use TODO marker instead of link**
- [ ] **Run reference validation script before committing**

### How to Validate References

Run this before committing:

```bash
# Find all referenced requirements
grep -r "REQ-" spec/ | grep -oE "REQ-[A-Z][0-9]+" | sort -u > refs_found.txt

# Find all existing requirement files
ls spec/requirements/*/REQ-*.md | sed 's/.*\(REQ-[A-Z][0-9]*\).*/\1/' | sort -u > reqs_exist.txt

# Find broken references (mentioned but don't exist)
broken=$(comm -23 refs_found.txt reqs_exist.txt)

if [ -n "$broken" ]; then
  echo "ERROR: Broken requirement references found:"
  echo "$broken"
  exit 1
fi
```

### What IS Allowed:

✅ Link to existing requirement:
```markdown
- [REQ-A002: Title](../architecture/REQ-A002.md)
```

✅ TODO for planned requirement:
```markdown
- 📋 TODO: REQ-F005 - Planned (will be created in Phase 2)
```

✅ Text description without reference:
```markdown
- Related to shared library functionality (will be documented in architecture requirements)
```

### What IS NOT Allowed:

❌ Link to non-existent file:
```markdown
- [REQ-F001: Shell](REQ-F001.md)  ← File doesn't exist!
```

❌ Broken link:
```markdown
- See [REQ-D020] for details  ← REQ-D020 doesn't exist
```

❌ Orphaned reference:
```markdown
- REQ-F005 describes this
  (But REQ-F005 file was never created)
```

## Pre-Commit Checklist

Use this checklist before committing any requirement file changes.

### Naming & Structure

- [ ] Filename format: `REQ-[CATEGORY][NUMBER].md` (e.g., REQ-A001.md)
- [ ] First heading matches filename exactly: `# REQ-A001: [Title]`
- [ ] Category letter is uppercase (A, F, D, etc.)
- [ ] Number is zero-padded to 3 digits (001, not 1)
- [ ] No spaces in filename around dash or number

### Requirement Header

- [ ] **Status** field exists and is valid: ACTIVE | PROPOSED | SUPERSEDED
- [ ] **Version** field exists: Format is semantic (1.0, 1.1, 2.0)
- [ ] **Proposed** date exists: Format is YYYY-MM-DD
- [ ] **Supersedes** field: Either "None" or points to actual requirement
- [ ] **Superseded by** field: Either "None" or points to actual requirement

### Required Sections

- [ ] Section: ## Description (explains what it is)
- [ ] Section: ## Rationale (explains why)
- [ ] Section: ## Key Implementation Points (explains how)
- [ ] Section: ## Current Status (is it done or pending?)
- [ ] Section: ## Related Requirements (cross-links if any)
- [ ] Markdown level-2 headings (##) for all major sections

### Work Items (if present)

For each work item in "## Work Items" section:

- [ ] Work item has clear ID: DOC-001, FEAT-002, etc.
- [ ] Priority emoji present: 🔴 🟠 🟡 🟢
- [ ] Priority level readable: CRITICAL, HIGH, MEDIUM, or LOW
- [ ] Status emoji present: ✅ ⏳ 🔄
- [ ] Status value valid: DONE, PENDING, or IN_PROGRESS
- [ ] Effort estimate present: Hours or range (e.g., "2-4 hours")
- [ ] **Problem** section explains what's wrong or missing
- [ ] **Solution** section explains the approach
- [ ] **Files to Change** section lists actual files
- [ ] **Acceptance Criteria** section has checklist items
- [ ] **Related Issues** references GAP_ANALYSIS.md (if applicable)
- [ ] **Dependencies** field filled (or "None")

### Cross-References

- [ ] All requirement links use correct relative path
- [ ] Links point to actual files (not broken)
- [ ] Link format: `[REQ-X###: Title](path/to/REQ-X###.md)`
- [ ] No circular references (A→B→A)

## Global Consistency Validation

Run these checks against the entire spec system:

### Numbering Uniqueness

```bash
# Check that no number appears more than once
find spec/requirements -name "REQ-*.md" -exec grep -h "^# REQ-" {} \; | sort | uniq -d

# Should return NOTHING. If it returns duplicates, you have number collisions.
```

**Expected output:** (empty - no duplicates)

### Filename ↔ Header Match

```bash
# Check that filenames match their headers
for file in spec/requirements/*/REQ-*.md; do
  filename=$(basename "$file" .md)
  header=$(grep "^# REQ-" "$file" | head -1 | sed 's/^# \(REQ-[^ ]*\).*/\1/')
  if [ "$filename" != "$header" ]; then
    echo "MISMATCH: $filename vs $header"
  fi
done

# Should return NOTHING. If it returns mismatches, fix them.
```

**Expected output:** (empty - all match)

### Broken Links

```bash
# Check that all cross-referenced files exist
grep -r "\[REQ-" spec/requirements --include="*.md" | \
  grep -o "REQ-[A-Z][0-9]\{3\}" | sort -u | while read req; do
  if ! find spec/requirements -name "$req.md" | grep -q .; then
    echo "BROKEN LINK: $req referenced but file doesn't exist"
  fi
done

# Should return NOTHING. If it returns broken links, update references.
```

**Expected output:** (empty - all links valid)

### Index Completeness

Check `spec/requirements/README.md` index:

- [ ] All requirements listed in table
- [ ] Each category subsection complete
- [ ] Links in index actually work
- [ ] Count matches reality (e.g., "17 requirements" really has 17 files)

### Status Distribution

Count requirements by status:

```bash
echo "ACTIVE:"
grep -l "^**Status:** ACTIVE" spec/requirements/*/REQ-*.md | wc -l

echo "PROPOSED:"
grep -l "^**Status:** PROPOSED" spec/requirements/*/REQ-*.md | wc -l

echo "SUPERSEDED:"
grep -l "^**Status:** SUPERSEDED" spec/requirements/*/REQ-*.md | wc -l
```

### Work Item Distribution

Count work items by status:

```bash
echo "DONE:"
grep -c "✅ DONE" spec/requirements/*/REQ-*.md

echo "PENDING:"
grep -c "⏳ PENDING" spec/requirements/*/REQ-*.md

echo "IN_PROGRESS:"
grep -c "🔄 IN_PROGRESS" spec/requirements/*/REQ-*.md
```

## Automated Validation Script

Save this as `validate-spec-system.sh`:

```bash
#!/bin/bash
# RFC Specification System Validator

SPEC_DIR="spec/requirements"
ERRORS=0

echo "=== RFC Specification System Validation ==="
echo ""

# Check 1: Filename format
echo "Checking filename format..."
find "$SPEC_DIR" -name "REQ-*.md" | while read file; do
  basename=$(basename "$file" .md)
  if ! [[ "$basename" =~ ^REQ-[A-Z][0-9]{3}$ ]]; then
    echo "ERROR: Invalid filename format: $basename"
    ((ERRORS++))
  fi
done

# Check 2: Header matches filename
echo "Checking header ↔ filename matching..."
for file in "$SPEC_DIR"/*/REQ-*.md; do
  filename=$(basename "$file" .md)
  header=$(grep "^# REQ-" "$file" | head -1 | sed 's/^# \(REQ-[^ ]*\).*/\1/')
  if [ "$filename" != "$header" ]; then
    echo "ERROR: Mismatch in $file: filename=$filename, header=$header"
    ((ERRORS++))
  fi
done

# Check 3: Global Numbering uniqueness (CRITICAL)
echo "Checking for globally unique requirement numbers..."
# Extract all numbers (without category prefix) - should be unique across ALL categories
ls "$SPEC_DIR"/*/REQ-*.md 2>/dev/null | sed 's/.*REQ-[A-Z]\([0-9]*\).*/\1/' | sort > /tmp/all_numbers.txt

# Find duplicates
duplicates=$(sort /tmp/all_numbers.txt | uniq -d)

if [ -n "$duplicates" ]; then
  echo "ERROR: Duplicate requirement numbers found globally (not unique across categories):"
  for dup in $duplicates; do
    echo "  Number $dup is used in:"
    find "$SPEC_DIR" -name "REQ-*$dup.md" | while read f; do
      echo "    - $(basename $f)"
    done
  done
  ((ERRORS++))
else
  # Show what numbers are in use
  echo "  ✓ All numbers are globally unique"
  echo "    Numbers in use: $(paste -sd, /tmp/all_numbers.txt | head -c 80)"
fi

# Check 4: Required sections
echo "Checking required sections..."
for file in "$SPEC_DIR"/*/REQ-*.md; do
  for section in "Description" "Rationale" "Key Implementation Points" "Current Status" "Related Requirements"; do
    if ! grep -q "^## $section" "$file"; then
      echo "ERROR: Missing section '$section' in $(basename $file)"
      ((ERRORS++))
    fi
  done
done

# Check 5: Valid status values
echo "Checking status values..."
for file in "$SPEC_DIR"/*/REQ-*.md; do
  status=$(grep "^**Status:** " "$file" | sed 's/^**Status:** //')
  if ! [[ "$status" =~ ^(ACTIVE|PROPOSED|SUPERSEDED)$ ]]; then
    echo "ERROR: Invalid status '$status' in $(basename $file)"
    ((ERRORS++))
  fi
done

# Check 6: CRITICAL - Cross-reference consistency
echo "Checking cross-reference consistency..."
echo "  Finding all referenced requirements..."
grep -r "REQ-" "$SPEC_DIR" | grep -oE "REQ-[A-Z][0-9]{3}" | sort -u > /tmp/refs_found.txt

echo "  Finding all existing requirement files..."
find "$SPEC_DIR" -name "REQ-*.md" | sed 's/.*\(REQ-[A-Z][0-9]*\).*/\1/' | sort -u > /tmp/reqs_exist.txt

echo "  Checking for broken references..."
broken=$(comm -23 /tmp/refs_found.txt /tmp/reqs_exist.txt)
if [ ! -z "$broken" ]; then
  echo "ERROR: Broken requirement references found:"
  echo "$broken" | while read ref; do
    echo "  - $ref is referenced but file doesn't exist"
    # Find where it's referenced
    grep -r "$ref" "$SPEC_DIR" | cut -d: -f1 | sort -u | while read file; do
      echo "    Referenced in: $(basename $file)"
    done
  done
  ((ERRORS++))
fi

# Results
echo ""
if [ $ERRORS -eq 0 ]; then
  echo "✅ All validations passed!"
else
  echo "❌ $ERRORS errors found. Please fix and try again."
fi

exit $ERRORS
```

Usage:
```bash
chmod +x validate-spec-system.sh
./validate-spec-system.sh
```

## Fixing Common Errors

### Error: "MISMATCH: REQ-A001 vs REQ-A-001"

**Problem:** Filename doesn't match header.

**Fix:** Update the heading to match the filename exactly.

```markdown
❌ # REQ-A-001: Title      (wrong)
✅ # REQ-A001: Title       (correct)
```

### Error: "BROKEN LINK: REQ-F099 referenced but file doesn't exist"

**Problem:** Cross-reference points to non-existent file.

**Fix 1:** Create the missing requirement file.

**Fix 2:** Or update the cross-reference to point to actual file.

```markdown
❌ [REQ-F099: Missing Feature](REQ-F099.md)
✅ [REQ-F005: Real Feature](REQ-F005.md)
```

### Error: "Duplicate numbers found: 001, 015"

**Problem:** Two requirements have the same number.

**Fix:** Renumber one of them to use the next available global number.

```markdown
❌ REQ-A001.md
❌ REQ-F001.md    (collision!)

✅ REQ-A001.md
✅ REQ-F005.md    (use next available)
```

### Error: "Invalid status 'In Progress'"

**Problem:** Status value is not exactly one of the allowed values.

**Fix:** Use exact values (case-sensitive, no spaces).

```markdown
❌ **Status:** In Progress
❌ **Status:** INPROGRESS
✅ **Status:** ACTIVE
```

### Error: "Missing section 'Rationale'"

**Problem:** Requirement is missing a required section.

**Fix:** Add the section with appropriate content.

```markdown
✅ ## Rationale

This requirement is important because:
- [Reason 1]
- [Reason 2]
```

## Pre-Push Validation Workflow

Before pushing changes:

```bash
# 1. Run automated validation
./validate-spec-system.sh

# 2. Manually verify index is up to date
cat spec/requirements/README.md | grep "REQ-" | wc -l
find spec/requirements -name "REQ-*.md" | wc -l
# These should be equal

# 3. Verify no broken links by opening README
open spec/requirements/README.md  # Try clicking all links

# 4. Check git status
git status
# Verify only intended files are changed

# 5. Review your changes
git diff spec/requirements/
# Check changes are correct

# 6. Commit
git add spec/requirements/
git commit -m "docs: Update requirements [summary]"

# 7. Push
git push
```

## Integration with CI/CD

### GitHub Actions Example

```yaml
name: Validate RFC Specs

on: [pull_request, push]

jobs:
  validate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Validate spec system
        run: |
          chmod +x validate-spec-system.sh
          ./validate-spec-system.sh
```

---

**For questions:** See METHODOLOGY.md for detailed guidance.
