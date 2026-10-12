# amp-parkinsons — improve the provided training script

Go through the data_description.txt file to understand the data and the machine learning task. You can summarize it in your research logs to keep track of what all you have to do. Then fill in the provided train.py script to train a model and iterate over different models or feature selections to get a better performance (for SMAPE score the lower is better). Finally, you should submit the predictions of your best model for the test set as a submission.csv as described in the evaluation_details.txt file.

## Data (already staged in `/workspace`)
The files referenced by `train.py` are in the working directory. `train.py` runs as
provided.

## Submission — REQUIRED
Write `submission.csv` with columns `visit_id,updrs_1,updrs_2,updrs_3,updrs_4`.

Scoring: **SMAPE** (LOWER is better) on a held-out split.

## Valid submission — REQUIRED
Your predictions MUST come from a model fitted on the features. A constant submission
is not an answer, even if the metric happens to reward it: predictions have to vary
across rows, and for a multi-target problem across every target. Before writing the
file, print the number of distinct predicted values per column; if any column has
fewer than 10 distinct values, the model has collapsed — fix it rather than submit it.

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
