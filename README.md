# Structured Output Fine-Tuning for JSON Document Extraction

Fine-tuning Llama 3.2 3B to reliably extract structured JSON from business
documents -- a practical evaluation of LoRA-based supervised fine-tuning versus
prompt engineering for format consistency in production document pipelines.

---

## Project Overview

This project evaluates whether fine-tuning a small language model with LoRA produces
more reliable structured JSON extraction from business documents than prompt engineering
alone. The core hypothesis is that format compliance (producing parseable JSON with
correct schema keys and proper data types) is a learned behavior that benefits more
from weight updates than from instruction prompting. The evaluation compares a baseline
Llama 3.2 3B-Instruct model against the same model fine-tuned on 80 curated examples
across two document types: invoices and purchase orders.

---

## Repository Structure

```
project/
|-- schema/
|   |-- invoice_schema.md          # JSON schema specification for invoices
|   +-- po_schema.md               # JSON schema specification for purchase orders
|-- data/
|   |-- curated_train.jsonl        # 80 curated training examples (JSONL format)
|   +-- curation_log.md            # Manual curation decisions for all examples
|-- eval/
|   |-- held_out_documents.md      # 20 test documents with ground truth
|   |-- baseline_responses.md      # Verbatim base model outputs
|   |-- baseline_scores.csv        # Scored baseline results
|   |-- finetuned_responses.md     # Verbatim fine-tuned model outputs
|   |-- finetuned_scores.csv       # Scored fine-tuned results
|   |-- before_vs_after.md         # Side-by-side comparison
|   |-- summary.md                 # Parse success rates before and after
|   +-- failures/
|       |-- failure_01.md          # Failure analysis 1
|       |-- failure_02.md
|       |-- failure_03.md
|       |-- failure_04.md
|       +-- failure_05.md
|-- prompts/
|   |-- prompt_iterations.md       # Three prompt engineering attempts
|   +-- prompt_eval.md             # Results of prompt experiments
|-- screenshots/
|   |-- training_config.png        # LlamaFactory UI configuration panel
|   +-- loss_curve.png             # Training loss curve at completion
|-- training_config.md             # Hyperparameter choices with justifications
|-- report.md                      # Prompting vs fine-tuning analysis
+-- README.md
```

---

## Setup and Installation

### Requirements

- Python 3.9 or higher
- Mac with 8GB RAM (tested on Apple Silicon and Intel)
- LlamaFactory
- Hugging Face account with access to meta-llama/Llama-3.2-3B-Instruct

### Installation

```bash
pip install 'llamafactory[torch]' datasets huggingface_hub pandas jsonschema
```

If installing from source:

```bash
git clone https://github.com/hiyouga/LLaMA-Factory.git
cd LLaMA-Factory
pip install -e ".[torch]"
cd ..
```

### Launch the Web UI

```bash
llamafactory-cli webui
```

Open http://localhost:7860 in your browser.

---

## Dataset

| Dataset | Purpose | Source |
|---------|---------|--------|
| CORD v2 | Primary invoice and receipt training examples | naver-clova-ix/cord-v2 |
| SROIE 2019 | Secondary receipt examples | AdamCodd/sroie2019 |
| Invoices Donut v1 | Purchase order training examples | katanaml-org/invoices-donut-data-v1 |

Training set: 80 manually curated examples (50 invoices, 30 purchase orders)
Test set: 20 held-out documents not present in training data

---

## Results

| Metric | Baseline | Fine-Tuned |
|--------|----------|-----------|
| Parse Success Rate | [X]% | [Y]% |
| Average Key Accuracy | [X] | [Y] |
| Average Value Accuracy | [X] | [Y] |

[Fill in these numbers after completing evaluations.]

---

## Fine-Tuning Configuration

| Parameter | Value | Justification |
|-----------|-------|--------------|
| Method | LoRA (SFT) | Parameter-efficient; feasible on 8GB RAM |
| LoRA Rank | 16 | Balanced capacity for dual-schema task |
| LoRA Alpha | 32 | Standard 2x rank scaling |
| Learning Rate | 2e-4 | Center of stable range for LoRA on small datasets |
| Epochs | 3 | Sufficient for 80 examples without overfitting |
| Batch Size | 2 | Memory limit on 8GB RAM |
| Quantization | 4-bit | Required to fit 3B model in 8GB |

Full justification for each parameter is in training_config.md.

---

## Key Findings

[Fill in after completing all evaluations with 3-5 sentences on the most important
numeric and qualitative findings.]

---

## Reproducing the Evaluation

To validate the training data:

```bash
python3 -c "
import json
errors = []
with open('data/curated_train.jsonl') as f:
    for i, line in enumerate(f, 1):
        try:
            obj = json.loads(line.strip())
            json.loads(obj['output'])
        except Exception as e:
            errors.append(f'Line {i}: {e}')
print(f'Total examples: {i}')
print('Errors:', errors if errors else 'None')
"
```

To score model responses against ground truth, compare parsed JSON outputs against
the ground truth defined in eval/held_out_documents.md using the metrics defined
in the CSV column headers (is_valid_json, has_all_required_keys, key_accuracy,
value_accuracy).
