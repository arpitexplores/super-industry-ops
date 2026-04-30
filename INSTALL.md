# Installation

SUPER Skills are portable Markdown skills. Install the skill folder into any AI agent setup that supports local skill files, custom instruction folders, or reusable Markdown workflows.

## Download ZIP

If you do not use git:

1. Open this GitHub repository.
2. Select **Code**.
3. Select **Download ZIP**.
4. Unzip the download.
5. Rename the extracted folder from `super-industry-ops-main` to `super-industry-ops`.
6. Copy the renamed `super-industry-ops` folder into your agent's skills directory.
7. Restart or reload your agent.

## Install One Skill With A Terminal

Copy the full skill folder into your agent's skills directory:

```bash
cp -R super-industry-ops ~/.your-agent/skills/
```

This repository is the `super-industry-ops` skill. Keep the full `super-industry-ops` folder together when installing it.

After copying the folder, restart or reload your agent so it can discover the new skill.

## Use A Skill

Ask your agent to use the skill by name:

```text
Use $super-industry-ops to help with this request.
```

You can also describe the task naturally. If your agent supports skill discovery, it should route the request to the matching `SKILL.md` file.

## Folder Structure

A SUPER Skill is installed as one folder:

```text
super-industry-ops/
|-- SKILL.md
|-- references/
|   `-- modules/
|-- examples/
|-- VERSION
`-- CHANGELOG.md
```

Keep the full folder together. The top-level `SKILL.md` is the entry point, and the `references/modules/` files provide deeper workflows when needed.

## Install Multiple Skills

Install only the skills you need. For example, a website launch workflow might use:

- `super-design-core` for UI and UX direction
- `super-design-quality` for accessibility and responsive QA
- `super-seo-foundation` for technical SEO
- `super-seo-growth` for AI SEO, GEO, and content visibility
- `super-marketing-execution` for landing page copy and campaign launch assets

Each skill is self-contained, so missing related skills will not break the installed skill. Related skills simply provide deeper coverage when installed together.

## Updating

To update a skill, replace the old skill folder with the newer release folder, then restart or reload your agent.

Before replacing a folder, preserve any local edits you made inside it.

## Compatibility

These skills avoid platform-specific requirements. They are designed for AI coding agents, local assistant setups, and Markdown-based workflow systems that can read a `SKILL.md` entry point.
