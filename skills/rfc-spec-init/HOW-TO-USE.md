# How to Use the rfc-spec-init Skill

## The Skill is Ready

You now have a **reusable skill** that initializes RFC specification systems.

**Location:** `~/.copilot/skills/rfc-spec-init/`

---

## Using the Skill in Copilot CLI

### Method 1: Direct Invocation (Recommended)

```bash
@copilot-cli rfc-spec-init
```

**What it does:**
- Scaffolds the entire spec/ directory structure
- Copies all templates to your project
- Creates a starter requirement file
- Validates everything
- Shows next steps

**Time:** < 1 minute

---

### Method 2: With Project Path

```bash
@copilot-cli rfc-spec-init --target /path/to/project
```

**Use when:**
- Initializing a different project
- Running from outside the project directory
- Automating setup for multiple projects

---

### Method 3: With Custom Categories

```bash
@copilot-cli rfc-spec-init --categories A,F,D,T,I
```

**Creates categories for:**
- A = Architecture
- F = Features
- D = Documentation
- T = Testing (custom)
- I = Infrastructure (custom)

---

### Method 4: Force Overwrite

```bash
@copilot-cli rfc-spec-init --force
```

**Use when:**
- Reinitializing an existing project
- Resetting to default templates
- ⚠️ WARNING: Overwrites existing spec/

---

## Step-by-Step Example

### Scenario: Initialize a new project

**Step 1: Navigate to project**
```bash
cd /path/to/my-project
```

**Step 2: Invoke the skill**
```bash
@copilot-cli rfc-spec-init
```

**Step 3: Watch it initialize**
```
✅ RFC Specification System Initialized!

Created:
  📁 spec/
  📁 spec/requirements/architecture/
  📁 spec/requirements/features/
  📁 spec/requirements/documentation/
  📄 spec/README.md
  📄 spec/ARCHITECTURE.md
  ...
```

**Step 4: Follow the next steps shown**

Done! Your project now has a complete RFC spec system.

---

## What the Skill Creates

```
spec/                               # Main directory
├── README.md                       # Navigation hub (copied)
├── ARCHITECTURE.md                 # System overview (template)
├── GAP_ANALYSIS.md       # Issue tracking (template)
└── requirements/                   # Requirements directory
    ├── README.md                   # Index of requirements (template)
    ├── architecture/               # Architecture category
    │   └── REQ-A001.md            # Starter requirement
    ├── features/                   # Features category (empty)
    └── documentation/              # Documentation category (empty)
```

Total files created: **8**  
Total directories created: **6**

---

## After Initialization

### You Now Have:

✅ Complete spec system structure  
✅ All templates in place  
✅ Example requirement (REQ-A001)  
✅ Navigation hub (spec/README.md)  
✅ Ready to customize  

### Next Steps:

1. **Edit the starter requirement:**
   ```bash
   vim spec/requirements/architecture/REQ-A001.md
   ```

2. **Update the index:**
   ```bash
   vim spec/requirements/README.md
   # Add your requirement to the table
   ```

3. **Create more requirements:**
   ```bash
   cp ~/.copilot/rfc-spec-system/REQ-TEMPLATE.md \
      spec/requirements/features/REQ-F005.md
   ```

4. **Commit:**
   ```bash
   git add spec/
   git commit -m "docs: Initialize RFC specification system"
   ```

---

## How the Skill Works

### Behind the Scenes

```
User runs: @copilot-cli rfc-spec-init

↓

Skill agent starts (general-purpose, full reasoning)

↓

Agent:
  1. Validates project directory
  2. Checks permissions
  3. Creates spec/ structure
  4. Copies templates from ~/.copilot/rfc-spec-system/
  5. Validates all files
  6. Provides output with next steps

↓

Project now has complete RFC system ready to use!
```

---

## Skill Architecture

| Component | Purpose |
|-----------|---------|
| **rfc-spec-init/README.md** | Skill documentation |
| **rfc-spec-init/SKILL-PROMPT.md** | What agent does |
| **rfc-spec-init/QUICK-REFERENCE.md** | Quick usage guide |
| **~/.copilot/rfc-spec-system/** | Global templates & docs |

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| "Command not found" | Make sure you're in Copilot CLI context |
| "spec/ exists already" | Use `--force` to overwrite or delete manually |
| "Templates not found" | RFC system not installed - check ~/.copilot/rfc-spec-system/ |
| "Permission denied" | Check write permissions on project directory |

---

## Tips

✅ **Tip 1:** Initialize before you start documenting  
✅ **Tip 2:** Customize templates for your team standards  
✅ **Tip 3:** Commit spec/ to version control  
✅ **Tip 4:** Reference the full docs in ~/.copilot/rfc-spec-system/  
✅ **Tip 5:** Create a team guide using the templates  

---

## Full Documentation

For complete guidance on using the RFC system after initialization:

```bash
cat ~/.copilot/rfc-spec-system/START-HERE.md         # Welcome
cat ~/.copilot/rfc-spec-system/QUICKSTART.md         # Quick start
cat ~/.copilot/rfc-spec-system/METHODOLOGY.md        # Deep dive
```

---

## That's It!

The skill handles all the scaffolding and setup. You focus on writing requirements.

### Quick Command:
```bash
@copilot-cli rfc-spec-init
```

### Time Investment:
- Invocation: < 1 minute
- Total time to working system: 5 minutes

### Result:
✅ Production-ready RFC specification system

---

**Ready to use! Just invoke `@copilot-cli rfc-spec-init` in your project.**
