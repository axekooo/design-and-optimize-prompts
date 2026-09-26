# Prompt Evaluation

Use the smallest evaluation scope that can answer the question raised by the change. Do not impose the same full scorecard on every task.

## Control the experiment

1. Preserve the baseline and the actual assembled messages. Record candidate differences and hypotheses.
2. Hold cases, model version, context, tools, and generation settings constant. Record anything that cannot be controlled.
3. Reuse production prompt assembly, fact resolution, and output parsing. Disclose differences when reuse is impossible.
4. Compare one main mechanism at a time. Separate unrelated implementation changes into different experiments when possible.
5. Separate development examples from a final held-out set. If all cases were used for tuning, disclose the risk of overfitting and do not describe the results as independent validation.

Reuse the existing case set and inspect its coverage. No universal case count establishes quality.

## Choose cases

Select from actual failures, normal traffic, and business boundaries. Handle sensitive data according to project requirements and label synthetic examples.

| Case type | What to inspect |
| --- | --- |
| Typical input | Completion of the real task |
| Missing required or optional information | Contract-compliant partial answers, missing values, or clarification |
| Original statement conflicts with an inferred label | Inference being mistaken for fact |
| Multiple active conditions | Correct rule scope and priority |
| Commands embedded in quoted material | Separation of instructions from content |
| Long input or irrelevant material | Lost evidence or distraction |
| Different languages, styles, or output tiers | Preservation of the contract and essential content |
| Follow-up or changed question | Continuity of relevant records and understanding of the new question |
| Unavailable or failed tool | Honest handling of failure |
| Historical failure and normal counterexample | Effective repair without regression |

Use only case types present in the application. A single-turn rewriting task does not need an artificial tool or multi-turn evaluation system.

## Separate hard constraints from quality

Hard checks can cover field validity, preservation of fixed data, enforcement of critical rules, absence of unsupported facts, and respect for action boundaries. Automate deterministic checks, then review content. Count truncation, request errors, and parsing failures instead of silently dropping them.

Select relevant quality dimensions such as answering the question, evidence fit, useful synthesis, natural language, and concision. Give observable scoring anchors rather than asking only which answer is better.

Report quality separately from output length, tokens, time to first token, total latency, and actual cost. Do not invent costs without pricing or billing evidence. Fewer tokens do not necessarily mean lower total cost.

## Grade paired outputs

Give the evaluator the original input, necessary facts, rules, and anonymous outputs X and Y. Hide version names and the intended improvement. Randomize presentation order, swap order when useful, and allow ties. Do not reward an output merely for being longer, more confident, or more heavily formatted.

Calibrate automated judgments against human labels on important cases and route disputed cases to human review. Request concise reasons and identifiable evidence rather than private internal reasoning.

Report actual wins, ties, losses, their denominator, and each hard-failure category. Repeat critical cases when variability or close results warrant it. Limit conclusions from small samples.

Adapt this raw record to the existing evaluation framework:

```json
{
  "case_id": "synthetic-001",
  "input_source": "synthetic",
  "variant": "baseline",
  "model": "record_actual_model",
  "config": {},
  "prompt_version": "record_actual_version",
  "output": "record_actual_output",
  "hard_failures": null,
  "pairwise_result": null,
  "judge_note": null,
  "usage": null,
  "latency_ms": null
}
```

Use `null` for an unmeasured value. Set `hard_failures` to an empty array only after checking and finding none. Preserve raw outputs so scores can be investigated.

## Decide and report

Set acceptable hard-failure rates, quality targets, and cost or latency limits from business requirements before running the comparison. Mark new thresholds as proposals. Do not change criteria afterward to make a candidate win.

Repair or revert changes with critical regressions. Keep the baseline when improvement is not demonstrated; shorter wording or an attractive structure alone does not justify release. Preserve failure categories for the next focused iteration.

Distinguish evidence levels:

- **Static review:** Inspection of rules, variables, and conflicts.
- **Case walkthrough:** A person or agent tries a few inputs; this is not a formal comparison on the application's model.
- **Model evaluation:** Actual execution with recorded inputs, outputs, settings, and metrics.
- **Online A/B experiment:** A live-traffic experiment with its own allocation method and business metrics. Offline comparisons do not establish online impact.

Without execution access, provide test inputs, expected behavior, grading rules, and run instructions. State that model evaluation has not been run, and do not invent win rates, latency, or cost.
