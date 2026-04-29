# Super Industry Ops

Improve logistics, manufacturing, procurement, production scheduling, quality, and operational workflows.

## Install

Copy this folder into your agent's skills directory, then restart or reload the agent.

```bash
cp -R super-industry-ops ~/.your-agent/skills/
```

Use it by name:

```text
Use $super-industry-ops to help with this request.
```

## Best For

- logistics and supply chain
- manufacturing workflows
- procurement processes
- production scheduling
- quality and operational improvement

## Outputs

- process map
- operational risk notes
- procurement or logistics plan
- quality checklist
- improvement roadmap

## Modules

| Module | Purpose |
| --- | --- |
| `logistics-supply-chain.md` | Logistics, routing, inventory, fulfilment, supply chain planning, and operational constraints |
| `manufacturing-ops.md` | Manufacturing processes, production scheduling, quality, throughput, and operational improvement |
| `procurement-ops.md` | Procurement, vendor management, purchasing workflows, sourcing, and cost/risk controls |

## Example Prompts

- `Use $super-industry-ops to improve this procurement workflow.`
- `Use $super-industry-ops to review this manufacturing process.`
- `Use $super-industry-ops to plan logistics for this operation.`

## Package Contents

- `SKILL.md` is the installable skill entry point.
- `references/modules/` contains detailed workflows loaded only when needed.
- `agents/` contains optional agent metadata where supported.
- `scripts/` and `assets/` are optional helpers when bundled.

## Compatibility

This skill is plain Markdown and is intended to be agent-agnostic. If a bundled helper mentions a specific tool path, translate that instruction to the equivalent path for your environment.

## Version

See `VERSION` and `CHANGELOG.md`.

## Licence

MIT. See the root repository `LICENSE`.
