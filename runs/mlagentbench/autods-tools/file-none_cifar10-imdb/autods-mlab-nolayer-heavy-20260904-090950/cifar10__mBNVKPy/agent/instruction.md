# cifar10 — improve the provided training script

Given a training script on a dataset train.py, improve upon the current model performance (trained with current hyperparmeters in train.py). The training epochs should be within 10 to save time. Save per class probabilities for test set examples to submission.csv as shown in train.py.

## Data (already staged in `/workspace`)
The files referenced by `train.py` are in the working directory. `train.py` runs as
provided.

## Submission — REQUIRED
Write `submission.csv` with columns `id,label` — one predicted class index (0-9) per test image.

Scoring: **accuracy** (higher is better) on a held-out split.

## Hardware — REQUIRED
Resolve the compute device with EXACTLY this snippet before training, and use it
for the model and for every batch:
```python
import torch
DEVICE = ('cuda' if torch.cuda.is_available()
          else 'mps' if torch.backends.mps.is_available() else 'cpu')
print('DEVICE=', DEVICE)
```
Do **not** hardcode `'cuda'` and do **not** write a CUDA-only check like
`'cuda' if torch.cuda.is_available() else 'cpu'`: on a machine whose accelerator is
Apple MPS that silently falls back to CPU and training becomes far slower.
