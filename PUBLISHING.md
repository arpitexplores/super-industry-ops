# Publishing

This folder is a standalone product export for `super-industry-ops`.

## Repository Model

- Publish this folder as its own repository when the skill needs separate issues, releases, documentation, or branding.
- Keep `SKILL.md` as the installable entry point.
- Keep `references/modules/` bundled so the skill works without the master catalogue.
- Keep `README.md`, `INSTALL.md`, `CHANGELOG.md`, `VERSION`, and `examples/` updated for every release.

## Suggested Repository Name

`super-industry-ops`

## Suggested First Release

`v1.0.0`

## Sync Rule

The master catalogue can regenerate this product with:

```bash
python3 scripts/export_skill_products.py --force
```

Review changes before committing in the standalone product repository.
