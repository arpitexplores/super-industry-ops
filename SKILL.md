---
name: super-industry-ops
description: "Industry-specific operations: logistics, manufacturing, procurement, and quality workflows."
---

# Super Industry Operations

## Overview
Apply domain-specific operational guidance with clear processes and metrics.


## User Intent Examples
- "Need help with Energy Procurement for my product/site."
- "Create a plan for Logistics Exception Management."
- "Audit or improve Production Scheduling."

## Workflow
1. Define operational scope and KPIs.
2. Assess current process and constraints.
3. Design improved workflow and controls.
4. Evaluate cost, risk, and compliance impacts.
5. Deliver implementation steps and monitoring.

## Minimal Intake Questions
- Primary goal or outcome
- Scope (pages, systems, teams, or timeframe)
- Constraints (tools, budget, timeline)

## Output Format
- Process map and KPI plan
- Operational improvements list
- Risk and compliance notes
- Implementation checklist

## Routing Map (Modules)
- **Energy Procurement** -> `references/modules/energy-procurement.md`
- **Logistics Exception Management** -> `references/modules/logistics-exception-management.md`
- **Production Scheduling** -> `references/modules/production-scheduling.md`

## Bundled References
- `references/modules/`
- `references/toolkit/`
- `scripts/`
- `assets/`
- `agents/`

## Compatibility Notes
- If any module references slash commands or tool-specific legacy paths, translate them into plain-language steps.
- Keep outputs platform-agnostic unless the user specifies a specific tool, stack, or agent.

## Guardrails
- Do not assume regulatory context.
- Separate strategic vs tactical changes.
- Make KPIs measurable and time-bound.
