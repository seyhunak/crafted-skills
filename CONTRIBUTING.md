# Contributing to Crafted Agent Skills

Thank you for your interest in contributing! This project follows the [Agent Skills](https://github.com/agentskills/agentskills) specification.

## Adding a New Skill

1. Create a new folder under `skills/` with a kebab-case name
2. Add a `SKILL.md` file with the required frontmatter (`name`, `description`)
3. Optionally add `scripts/`, `references/`, or `assets/` directories
4. Update the root `README.md` to list your new skill

### Skill Structure

```
skills/your-skill-name/
├── SKILL.md          # Required: metadata + instructions
├── scripts/          # Optional: executable code
├── references/       # Optional: documentation
└── assets/           # Optional: templates, resources
```

### SKILL.md Frontmatter

At minimum, include:

```yaml
---
name: your-skill-name
description: "One-line description of what this skill does and when to use it"
---
```

## Adding a New Agent to an Existing Skill

If you've created a new AI flow and want to add it to the `crafted-mcp` skill:

1. Deploy the flow to the Crafted AI server
2. Add an entry to the appropriate domain table in `skills/crafted-mcp/SKILL.md`
3. Include: Agent name, tool name, and "Use When" description

## Development Workflow

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/your-feature`
3. Make your changes
4. Test with your AI tool (Cursor, Claude, etc.)
5. Commit: `git commit -m 'Add: your feature description'`
6. Push: `git push origin feature/your-feature`
7. Open a Pull Request

## Code of Conduct

Be respectful, constructive, and inclusive. We're all here to build better AI tools.

## Questions?

Open an issue or reach out at hello@we-crafted.com.
