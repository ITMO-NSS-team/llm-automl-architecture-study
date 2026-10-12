# imdb — improve the provided training script

Fill out train.py to 1) finetune DistilBERT on the IMDb dataset to determine whether a movie review is positive or negative and 2) save per class probabilities for test set examples to submission.csv. You can find skeleton code for loading the dataset and saving prediction to submission.csv in `train.py`.

## Data (already staged in `/workspace`)
The files referenced by `train.py` are in the working directory.

## Submission — REQUIRED
Write `submission.csv` with columns `id,label` (0 = negative, 1 = positive).

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
