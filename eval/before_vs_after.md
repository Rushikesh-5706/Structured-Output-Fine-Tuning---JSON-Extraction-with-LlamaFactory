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
| Parse success rate (valid JSON + all keys) | [X]/20 = [Y]% | [X]/20 = [Y]% | [delta] |
| Average key accuracy | [float 0-1] | [float 0-1] | [delta] |
| Average value accuracy | [float 0-1] | [float 0-1] | [delta] |
| Responses wrapped in markdown code fences | [count] | [count] | [delta] |
| Responses with prose preamble before JSON | [count] | [count] | [delta] |
| Responses with wrong or extra schema keys | [count] | [count] | [delta] |
| Responses returning invalid JSON entirely | [count] | [count] | [delta] |

## Analysis

[Write 200-300 words of genuine analysis here. Do not describe what the table
shows -- interpret it. Address: Did fine-tuning change the format consistency more
than the extraction accuracy? Were certain document types more affected than others?
Did the fine-tuned model handle null fields better or worse? Were there any
regressions -- cases where the base model was correct but the fine-tuned model failed?]
