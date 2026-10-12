# house-price — improve the provided training script

Go through the data_description.txt file to understand the data and all the features. You can summarize it in your research logs to keep track of what all you have to do. Then fill in the provided train.py script to train a model and iterate over different models or feature selections to get a better performance. Never try to read any csv files directly. Do not forget to execute the changes you made to check for performance.

## Data (already staged in `/workspace`)
The files referenced by `train.py` are in the working directory. `train.py` runs as
provided — except for the marked section you must fill in.

## Submission — REQUIRED
Write `submission.csv` with columns `Id,SalePrice`.

Scoring: **MAE** (mean absolute error, LOWER is better) on a held-out split.

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
