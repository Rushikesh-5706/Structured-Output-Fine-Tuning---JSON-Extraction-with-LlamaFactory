# Fine-Tuning Configuration

## Model

- Base model: meta-llama/Llama-3.2-3B-Instruct
- Framework: LlamaFactory
- Method: Supervised Fine-Tuning (SFT) with LoRA

## Hyperparameter Decisions

### LoRA Rank: 16

Rank controls the dimensionality of the adapter matrices inserted into attention
layers. Rank 8 is sufficient for simple style transfer tasks. Rank 32 is warranted
for complex multi-domain reasoning. This task -- structured JSON formatting across
two document types with 9 and 8 schema fields respectively -- sits in the middle.
Rank 16 provides enough expressiveness to learn consistent key naming and value
typing across both schemas without the overfitting risk that rank 32 carries on
a dataset of 80 examples. At 8GB RAM on a Mac CPU, rank 16 remains trainable
within memory limits.

### LoRA Alpha: 32

Alpha controls the scaling of the LoRA updates. The standard practice of alpha = 2 *
rank is followed here (2 * 16 = 32). This scaling ensures the adapter updates are
neither too small (underfitting) nor too large (destabilizing the base model's learned
representations). With alpha = rank, updates are unscaled; doubling alpha ensures
meaningful learning without aggressive overwriting of pretrained weights.

### Learning Rate: 2e-4

For LoRA fine-tuning on instruction-following models, the typical effective range is
1e-4 to 3e-4. A rate of 2e-4 sits in the center of this range. Lower rates (1e-4)
are appropriate for very large datasets or when base model capabilities must be
preserved carefully. Higher rates (3e-4) risk overshooting on small datasets.
With 80 training examples, 2e-4 provides stable convergence without
aggressive weight updates.

### Epochs: 3

With 80 examples, training for 3 epochs means the model sees each example 3 times.
Epoch 1 establishes the output format pattern. Epoch 2 refines schema key consistency.
Epoch 3 solidifies value type handling (floats vs. strings, null handling).
Training for 4+ epochs on 80 examples carries significant overfitting risk -- the model
begins memorising specific input patterns rather than learning the general
JSON-formatting behaviour. The loss curve will be monitored to confirm the model
has not memorised training data (a suspicious near-zero loss before epoch 3 ends).

### Batch Size: 2

On a Mac with 8GB RAM, running Llama 3.2 3B in 4-bit quantization limits the
effective batch size. Batch size 2 provides a stable memory footprint and allows
gradient accumulation to simulate larger effective batches. Batch size 4 risks
out-of-memory errors on this hardware configuration.

### Gradient Accumulation Steps: 8

With batch size 2, accumulating gradients over 8 steps gives an effective batch
size of 16. This is large enough to produce stable gradient estimates across
diverse document formats without requiring more memory.

### Warmup Steps: 10

With 80 examples and 3 epochs at batch size 2, the total training steps are
approximately 120. A 10-step warmup (roughly 8% of total steps) is sufficient
to ramp the learning rate up smoothly before full training begins.

### Quantization: 4-bit (QLoRA)

On 8GB RAM, full-precision training of a 3B parameter model is not feasible.
4-bit quantization via bitsandbytes reduces the base model memory footprint to
approximately 2GB, leaving sufficient RAM for activations, gradients, and the
LoRA adapter itself.

## Screenshot Reference

screenshots/training_config.png -- captured before training started.

## Training Runs

### Run 1
[Document the actual loss curve behaviour observed. Did it decrease smoothly?
Did it plateau at epoch 2? Did it drop suspiciously fast? Be specific. If you
ran a second training with adjusted settings, document that here with reasons.]
