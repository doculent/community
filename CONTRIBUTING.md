# Contributing

We welcome contributions to the Doculent open-source skills collection. Whether it's a new skill, an improvement to an existing one, or a bug fix — we want to hear from you.

## Adding a New Skill

Each skill lives in its own directory under `skills/`:

```
skills/your-skill-name/
├── SKILL.md    # Skill definition (YAML frontmatter + Claude Code instructions)
└── README.md   # Human-readable docs (install, usage, examples)
```

### SKILL.md Format

```yaml
---
name: your-skill-name
version: 1.0.0
description: |
  What the skill does. This text is used for discoverability
  in Claude Code, so be specific and practical.
allowed-tools:
  - Read
  - Write
  - Edit
  - Bash
  - Glob
  - Grep
metadata:
  tags: relevant, search, keywords
  author: Your Name or Org
  license: MIT
---

# Skill Title

Instructions for Claude Code to execute the skill...
```

### README.md Format

Each skill README should include:

1. **One-line description** — what it does
2. **Install command** — `claude install doculent/community/skills/your-skill-name`
3. **Dependencies** — any system tools required
4. **Usage examples** — real commands with real output
5. **How it works** — brief technical explanation

### Guidelines

- Keep skills focused on document intelligence — parsing, extraction, analysis, transformation
- Include realistic usage examples with sample output
- Document all external dependencies
- Test with multiple document types and edge cases before submitting
- Don't add unnecessary dependencies — prefer tools already available in Claude Code

## Improving Existing Skills

- Open an issue first to discuss the change
- Keep backward compatibility — don't break existing usage patterns
- Update the README if behavior changes
- Add tests or examples that demonstrate the improvement

## Pull Request Process

1. Fork the repository
2. Create a branch (`git checkout -b feature/your-improvement`)
3. Make your changes
4. Test the skill in Claude Code
5. Open a pull request with a clear description

## Reporting Issues

Open an issue with:
- The skill name
- What you expected
- What actually happened
- Your OS and Claude Code version

## Code of Conduct

Be respectful. Write clear commit messages. Help others when you can.
