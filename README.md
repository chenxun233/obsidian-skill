# Obsidian Skill Pack

This repo packages the current Obsidian workflows into one installable skill folder: `obsidian-workbench/`.

It replaces the old many-folder shape with one portable entry skill that bundles these modes:

- vault read/search mode
- durable note writing
- learning checklist ingest
- compiled wiki query and maintenance
- Markdown syntax fixes
- Bases `.base` editing
- Obsidian CLI and plugin debugging
- Code Styler CSS fixes

## Install From GitHub

After you upload this repo, install it with:

```bash
python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo <owner>/<repo> \
  --path obsidian-workbench
```

Or with a GitHub URL:

```bash
python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --url https://github.com/<owner>/<repo>/tree/main/obsidian-workbench
```

Then restart Codex so the new skill is discovered.

## Repo Layout

```text
obsidian-skill-pack/
├── README.md
└── obsidian-workbench/
    ├── SKILL.md
    ├── agents/openai.yaml
    └── references/
```

## Maintenance

Validate the packaged skill with:

```bash
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py obsidian-workbench
```
