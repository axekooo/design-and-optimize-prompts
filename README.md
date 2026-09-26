# Prompt Design and Optimization

A reusable skill for designing, reviewing, and improving text prompts through clear requirements, evidence boundaries, and task-specific evaluation.

The skill is written in English and uses general methods without provider presets or model-specific migration guidance. Deliverables follow the language and format requested for the task.

## What it does

- **Create prompts:** Turn business goals into clear input, output, and acceptance contracts.
- **Audit existing prompts:** Identify conflicting rules, unclear ownership, redundant instructions, and unsupported assumptions.
- **Propose candidates:** Preserve the baseline and describe the mechanism and possible regressions of each change.
- **Evaluate changes:** Compare outputs under controlled conditions and distinguish measured results from review or walkthroughs.

Simple requests receive a concise, copyable prompt. Production work can include a rule ownership table, candidate designs, test cases, and an evaluation plan.

## Use

Clone or download this repository:

```bash
git clone https://github.com/axekooo/design-and-optimize-prompts.git
```

Load [SKILL.md](SKILL.md) in your skill-compatible agent, or install this folder using that agent's skill installation workflow. Keep the referenced files with the skill.

Example request after installation:

```text
Use $design-and-optimize-prompts to review the prompt below.
First identify conflicting rules and assign clear ownership.
Then propose a candidate version and a paired evaluation plan.
Preserve the existing output contract.
```

For a smaller task:

```text
Use $design-and-optimize-prompts to write a short prompt
that rewrites a message politely while preserving refusals
and avoiding new commitments.
```

## Files

| File | Purpose |
| --- | --- |
| [SKILL.md](SKILL.md) | Main workflow and triggering description |
| [agents/openai.yaml](agents/openai.yaml) | Display and invocation metadata |
| [references/templates.md](references/templates.md) | Task contracts, prompt templates, and examples |
| [references/evaluation.md](references/evaluation.md) | Case selection, paired grading, and reporting |
| [references/sources.md](references/sources.md) | Sources for the general methods |
| [assets/icon.svg](assets/icon.svg) | Skill icon |

## Evaluation approach

The workflow separates static review, case walkthroughs, actual model evaluations, and live A/B experiments. It preserves the original prompt as a baseline and records untested proposals as candidates.
