# Baseline Model Responses

## Setup

Model: meta-llama/Llama-3.2-3B-Instruct (base -- no fine-tuning applied)
Inference tool: LlamaFactory inference tab
Temperature: 0.0
Date of evaluation: [fill in when run]

## Prompt Used for All 20 Documents

You are a document extraction system. Your task is to extract all fields from the document below and return ONLY a valid JSON object conforming to the schema. Do not write any explanation. Do not use markdown. Do not use code fences. Do not add any text before or after the JSON. Return only the raw JSON object starting with { and ending with }.

For invoices, the required fields are: vendor, invoice_number, date (YYYY-MM-DD), due_date (YYYY-MM-DD or null), currency (ISO 4217), subtotal (float), tax (float or null), total (float), line_items (array of objects with description, quantity, unit_price).

For purchase orders, the required fields are: buyer, supplier, po_number, date (YYYY-MM-DD), delivery_date (YYYY-MM-DD or null), currency (ISO 4217), total (float), items (array of objects with item_name, quantity, unit_price).

Use null for any field not found in the document. All monetary values must be floats. All dates must be YYYY-MM-DD strings.

Document:
[DOCUMENT_TEXT]

---

## eval_doc_01 Response
[PASTE VERBATIM RAW MODEL OUTPUT HERE -- DO NOT EDIT OR CLEAN THE OUTPUT]

---

## eval_doc_02 Response
[PASTE VERBATIM RAW MODEL OUTPUT HERE]

---

## eval_doc_03 Response
[PASTE VERBATIM RAW MODEL OUTPUT HERE]

---

## eval_doc_04 Response
[PASTE VERBATIM RAW MODEL OUTPUT HERE]

---

## eval_doc_05 Response
[PASTE VERBATIM RAW MODEL OUTPUT HERE]

---

## eval_doc_06 Response
[PASTE VERBATIM RAW MODEL OUTPUT HERE]

---

## eval_doc_07 Response
[PASTE VERBATIM RAW MODEL OUTPUT HERE]

---

## eval_doc_08 Response
[PASTE VERBATIM RAW MODEL OUTPUT HERE]

---

## eval_doc_09 Response
[PASTE VERBATIM RAW MODEL OUTPUT HERE]

---

## eval_doc_10 Response
[PASTE VERBATIM RAW MODEL OUTPUT HERE]

---

## eval_doc_11 Response
[PASTE VERBATIM RAW MODEL OUTPUT HERE]

---

## eval_doc_12 Response
[PASTE VERBATIM RAW MODEL OUTPUT HERE]

---

## eval_doc_13 Response
[PASTE VERBATIM RAW MODEL OUTPUT HERE]

---

## eval_doc_14 Response
[PASTE VERBATIM RAW MODEL OUTPUT HERE]

---

## eval_doc_15 Response
[PASTE VERBATIM RAW MODEL OUTPUT HERE]

---

## eval_doc_16 Response
[PASTE VERBATIM RAW MODEL OUTPUT HERE]

---

## eval_doc_17 Response
[PASTE VERBATIM RAW MODEL OUTPUT HERE]

---

## eval_doc_18 Response
[PASTE VERBATIM RAW MODEL OUTPUT HERE]

---

## eval_doc_19 Response
[PASTE VERBATIM RAW MODEL OUTPUT HERE]

---

## eval_doc_20 Response
[PASTE VERBATIM RAW MODEL OUTPUT HERE]
