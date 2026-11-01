---
name: kernel-skill-index
description: Find GPU kernel skills in the private Sun-Conure/kernel_skill catalog by hardware model, compute type, or optimization technique. Use when a KDA task needs this personal skill library or the user asks to consult kernel_skill.
---

# Private Kernel Skill Index

Catalog: [Sun-Conure/kernel_skill](https://github.com/Sun-Conure/kernel_skill) (private).

This entry routes to the separately maintained library. Access to its contents requires a GitHub identity with repository permission.

## Open the catalog

Reuse an existing authorized checkout when one is available. Otherwise, from the KDA repository root:

```bash
gh repo clone Sun-Conure/kernel_skill skills/kernel_skill
```

`skills/kernel_skill/` is an optional, ignored local checkout. The index is available in a normal KDA clone; fetching the private catalog is a separate step.

Read the catalog's root `SKILL.md`, then select the relevant index:

| Task information | Path relative to the catalog root | GitHub link |
| --- | --- | --- |
| Hardware model, architecture, compiler target | `queries/by-hardware.md` | [Hardware index](https://github.com/Sun-Conure/kernel_skill/blob/main/queries/by-hardware.md) |
| Operator or compute type | `queries/by-compute.md` | [Compute index](https://github.com/Sun-Conure/kernel_skill/blob/main/queries/by-compute.md) |
| Optimization technique or performance symptom | `queries/by-technique.md` | [Technique index](https://github.com/Sun-Conure/kernel_skill/blob/main/queries/by-technique.md) |

Follow the selected entry to its canonical skill and load only the references needed for the task. Catalog classifications distinguish general methods, instruction contracts, and historical measurements; check the actual target and evidence before applying advice.

## Use within KDA

- Do implementation work in the task workspace and preserve its correctness, determinism, and performance contract.
- Use this catalog for task-relevant guidance, KernelWiki for its supported architecture knowledge, and ncu-report-skill for profiling evidence when available.
- Record the catalog revision when its guidance informs an experiment or result.
- If repository access is unavailable, report that limitation and continue with permitted sources. Private catalog contents remain governed by their own repository permissions and terms.
