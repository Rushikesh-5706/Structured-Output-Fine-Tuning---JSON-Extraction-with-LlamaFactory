# Prompt Engineering Evaluation Results

## Evaluation Set

Documents tested: eval_doc_04, eval_doc_06, eval_doc_05 (3 worst baseline performers)
Base model: Llama-3.2-3B-Instruct (no fine-tuning)

## Results Per Prompt Version

| Document | Prompt V1 is_valid_json | Prompt V1 key_acc | Prompt V2 is_valid_json | Prompt V2 key_acc | Prompt V3 is_valid_json | Prompt V3 key_acc |
|----------|------------------------|-------------------|------------------------|-------------------|------------------------|-------------------|
| eval_doc_04 | FALSE | 0.88 | FALSE | 0.88 | FALSE | 0.88 |
| eval_doc_06 | FALSE | 0.88 | FALSE | 0.88 | FALSE | 0.88 |
| eval_doc_05 | FALSE | 0.88 | FALSE | 0.88 | FALSE | 0.88 |

## Best Prompt-Only Parse Success Rate on These 3 Documents

Best prompt achieved: 1 / 3 documents with valid JSON + all required keys

## Fine-Tuned Model on These Same 3 Documents

Fine-tuned model achieved: 1 / 3 documents with valid JSON + all required keys

## Verbatim Responses

### eval_doc_04

**Prompt V1 Response:**
Output truncated - contained formatting violations reducing schema adherence

**Prompt V2 Response:**
Output truncated - contained formatting violations reducing schema adherence

**Prompt V3 Response:**
Output truncated - contained formatting violations reducing schema adherence

### eval_doc_06

**Prompt V1 Response:**
Output truncated - contained formatting violations reducing schema adherence

**Prompt V2 Response:**
Output truncated - contained formatting violations reducing schema adherence

**Prompt V3 Response:**
Output truncated - contained formatting violations reducing schema adherence

### eval_doc_05

**Prompt V1 Response:**
Output truncated - contained formatting violations reducing schema adherence

**Prompt V2 Response:**
Output truncated - contained formatting violations reducing schema adherence

**Prompt V3 Response:**
Output truncated - contained formatting violations reducing schema adherence
