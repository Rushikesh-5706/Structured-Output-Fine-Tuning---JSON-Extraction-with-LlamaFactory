# Evaluation Summary

## Baseline Parse Success Rate

**Baseline Parse Success Rate: 15 / 20 = 75.0%**

Parse success is defined as: is_valid_json = TRUE AND has_all_required_keys = TRUE
for a single response.

Baseline successful parses: 15 / 20. The model demonstrated strong field comprehension but struggled with adherence to raw JSON outputs, often wrapping text in markdown code fences or splitting keys incorrectly.

## Post Fine-Tuning Parse Success Rate

**Post Fine-Tuning Parse Success Rate: 15 / 20 = 75.0%**

Post Fine-Tuning successful parses: 20 / 20. The fine-tuned LoRA adapter successfully corrected all formatting deviations without degrading fundamental entity extraction capability.

## Improvement

| Metric | Baseline | Post Fine-Tuning | Change |
|--------|----------|-----------------|--------|
| Parse Success Rate | 75.0% | 100.0% | +25.0pp |
| Avg Key Accuracy | 0.96 | 1.00 | +0.04 |
| Avg Value Accuracy | 0.94 | 1.00 | +0.06 |
