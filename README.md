# Cline Rule Library

A reusable library of development best practices for AI assistants, automatically fetched on-demand from GitHub repositories.

## How It Works

1. **Discovery** - AI assistant identifies when a task requires guidance (e.g., committing code, cleaning up files)
2. **Lookup** - Attempts to read rule from `.clinerules/.cache/author/repo/filename.md`
3. **Fetch** - If not found locally, runs `fetch-rule.sh <path>` to download from GitHub
4. **Application** - AI reads and applies the rule's guidance following Always/Never/Steps/Examples format

## Usage

### For AI Assistants

Include `.clinerules/fetch-rule.md` in your project. The AI will automatically:
- Scan available rules when relevant to current task
- Fetch missing rules from GitHub on-demand using `fetch-rule.sh`
- Apply rule guidance as authoritative instructions

### For Developers

**Add to your project:**
```bash
# Copy the fetch script
cp fetch-rule.sh scripts/

# Reference rules in .clinerules/
mkdir -p .clinerules
```

**Fetch a rule:**
```bash
./scripts/fetch-rule.sh .clinerules/pbierkortte/secure-minimal-python-devcontainer/add-header.md
```

## Benefits

- **On-Demand Loading** - Rules fetched only when needed (lazy/JIT pattern)
- **Shared Best Practices** - Reusable across projects and teams
- **Version Control** - Rules stored in GitHub, easily updated
- **AI-Optimized** - Structured format for consistent AI behavior
- **Minimal Footprint** - No manual file copying required

## Architecture

```
.clinerules/
├── .cache/              # Fetched rules cached locally
│   └── author/
│       └── repo/
│           └── *.md
└── fetch-rule.md        # Main documentation

fetch-rule.sh            # Fetches rules from GitHub raw URLs
```
