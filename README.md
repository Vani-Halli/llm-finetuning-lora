# Fine-Tuning Gemma 3 (270M) with LoRA for PII Detection

Fine-tuned Google's Gemma 3 (270M) language model using LoRA (Low-Rank Adaptation) for detecting and masking Personally Identifiable Information (PII) in text.

## Project Goal

Train the model to detect and mask PII in text, making it effective for Data Loss Prevention (DLP) and privacy-preserving applications.

## Dataset

Used the **AI4Privacy PII Masking** dataset from Hugging Face.

| Split | Samples |
|-------|---------|
| Training | 10,000 |
| Validation | 2,000 |
| Test | 1,000 |

**Columns used:**
- `source_text` → Original text containing PII
- `target_text` → Masked version of the text
- `privacy_mask` → JSON object describing masked entities

## Model Configuration

### Training Parameters
| Parameter | Value |
|-----------|-------|
| Epochs | 3 |
| Batch Size | 16 |
| Max Sequence Length | 256 |
| Gradient Accumulation Steps | 64 |

### LoRA Parameters
| Parameter | Value |
|-----------|-------|
| LoRA Rank (r) | 32 |
| LoRA Alpha | 64 |
| Target Modules | q_proj, v_proj, k_proj, o_proj |
| LoRA Dropout | 0.1 |

### Optimization
| Parameter | Value |
|-----------|-------|
| Learning Rate | 2e-4 |
| Warmup Ratio | 0.01 |
| LR Scheduler | Cosine |
| Optimizer | paged_adamw_8bit |
| Weight Decay | 0.001 |

## Results

| Metric | Before | After |
|--------|--------|-------|
| Mean Token Accuracy | 0.42 | 0.56 |
| Training Loss | 3.2 | 2.2 |

**Key Improvements:**
- Better PII detection with consistent identification and masking
- Improved accuracy on validation and test sets
- Reduced false positives
- Better generalization on unseen examples

## Files

| File | Description |
|------|-------------|
| `llm-finetuning-lora.ipynb` | Main fine-tuning notebook |
| `dataset-splitting.ipynb` | Dataset preparation and splitting |

## Tools Used

- Python
- PyTorch
- Hugging Face Transformers
- PEFT (Parameter-Efficient Fine-Tuning)
- LoRA
- Weights & Biases
- Google Colab / Kaggle

## How to Run

1. Open `dataset-splitting.ipynb` in Google Colab
2. Run all cells to prepare the dataset
3. Open `llm-finetuning-lora.ipynb` in Google Colab
4. Run all cells to fine-tune the model

## Author

**Vani Nagappa Halli**
- GitHub: [Vani-Halli](https://github.com/Vani-Halli)
- LinkedIn: [Vani Halli](https://linkedin.com/in/vani-halli)
