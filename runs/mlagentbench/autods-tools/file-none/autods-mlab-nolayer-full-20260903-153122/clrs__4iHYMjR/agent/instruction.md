# clrs — improve the provided training script

Improve the baseline model performance on the task floyd_warshall in The CLRS Algorithmic Reasoning Benchmark. To run the baseline model, execute train.py. You may modify the model architecture and the training loop, but keep the data loading and the submission format as provided.

## Data (already staged in `/workspace`)
The files referenced by `train.py` are in the working directory.

## Submission — REQUIRED
Write `submission.csv` with columns `graph_id,row,pointers` (64 space-separated predecessors per row).

Scoring: **pointer accuracy** (higher is better) on a held-out split.

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
