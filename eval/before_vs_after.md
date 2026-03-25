# Before vs After Fine-Tuning Comparison

## Methodology

Both evaluations used the same 20 held-out documents defined in
eval/held_out_documents.md. The same extraction prompt was used for
both the baseline and fine-tuned model. Temperature was set to 0.0 in both
cases to ensure deterministic output. The only variable that changed
between the two evaluation runs was the model weights.

## Results Table

| Metric | Baseline (base model) | Post Fine-Tuning | Change |
|--------|-----------------------|-----------------|--------|
| Parse success rate (valid JSON + all keys) | 15/20 = 75.0% | 20/20 = 100.0% | +25.0pp |
| Average key accuracy | 0.96 | 1.00 | +0.04 |
| Average value accuracy | 0.94 | 1.00 | +0.06 |
| Responses wrapped in markdown code fences | 6 | 0 | -6 |
| Responses with prose preamble before JSON | 2 | 0 | -2 |
| Responses with wrong or extra schema keys | 3 | 0 | -3 |
| Responses returning invalid JSON entirely | 0 | 0 | 0 |

## Analysis

The table above clearly identifies formatting compliance as the primary beneficiary of fine-tuning. The base model achieved 75% parse success, performing remarkably well at entity resolution, but failing on structural constraints (markdown fences, preamble inclusion, and handling non-standard labels). Fine-tuning forced the network into a rigorous structural compliance regime, achieving a 100% parse success rate.

We observed specific vulnerability in the base model regarding null handling for atypical labels (e.g. 'Taxable Amount' vs 'Subtotal'). The fine-tuning successfully imparted a schema-centric bias that caused to model to prioritize the strict schema keys mapping, safely handling edge cases that disrupted the base model.
