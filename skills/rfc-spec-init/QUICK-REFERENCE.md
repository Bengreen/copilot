# RFC Spec Init Skill - Quick Reference

## Invoke the Skill

```bash
@copilot-cli rfc-spec-init
```

That's it! The skill handles everything else.

---

## What Happens When You Invoke It

1. ✅ Checks project setup
2. ✅ Creates spec/ directory structure
3. ✅ Copies all templates
4. ✅ Creates starter requirement file (REQ-A001.md)
5. ✅ Validates everything
6. ✅ Shows next steps

---

## Output Example

```
✅ RFC Specification System Initialized!

Created:
  📁 spec/requirements/architecture/
  📁 spec/requirements/features/
  📁 spec/requirements/documentation/
  📄 spec/README.md
  📄 spec/ARCHITECTURE.md
  📄 spec/GAP_ANALYSIS.md
  📄 spec/requirements/README.md
  📄 spec/requirements/architecture/REQ-A001.md

Next Steps:
  1. Edit spec/requirements/architecture/REQ-A001.md
  2. Update spec/requirements/README.md with your requirement
  3. Commit: git add spec/ && git commit -m "docs: Initialize RFC spec system"

Learn More: ~/.copilot/rfc-spec-system/QUICKSTART.md
```

---

## Then What?

1. **Edit the starter requirement:**
   ```bash
   vim spec/requirements/architecture/REQ-A001.md
   # Fill in your first requirement
   ```

2. **Add to index:**
   ```bash
   vim spec/requirements/README.md
   # Add your requirement to the table
   ```

3. **Commit:**
   ```bash
   git add spec/
   git commit -m "docs: Initialize RFC specification system"
   ```

4. **Start using:**
   - Add more requirements (REQ-A002, REQ-F005, etc.)
   - Track work items
   - Update status as you go

---

## Available with Other Flags

(Future enhancements)

```bash
@copilot-cli rfc-spec-init --target /other/project
@copilot-cli rfc-spec-init --force
@copilot-cli rfc-spec-init --categories A,F,D,T,I
```

---

## When to Use This Skill

✅ Starting a new project  
✅ Adding RFC-style specs to existing project  
✅ Migrating from another spec system  
✅ Setting up team standards  
✅ Scaffolding project documentation  

---

## Related Skills & Tools

- **rfc-spec-migrate** (future) — Migrate existing specs to RFC format
- **rfc-spec-validate** (future) — Validate spec system consistency
- Manual setup: `~/.copilot/rfc-spec-system/QUICKSTART.md`
- Full guide: `~/.copilot/rfc-spec-system/METHODOLOGY.md`

---

## Troubleshooting

**Q: "spec/ already exists"**  
A: Use existing or delete it, then retry

**Q: "Templates not found"**  
A: RFC system not installed. Run: `cat ~/.copilot/rfc-spec-system/START-HERE.md`

**Q: Permission errors**  
A: Check write permissions on project directory

---

**That's all you need to know!** Just invoke `@copilot-cli rfc-spec-init` and you're done. 🚀
