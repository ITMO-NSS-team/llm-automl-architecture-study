# feedback — improve the provided training script

Go through the data_description.txt file to understand the data and the machine learning task. You can summarize it in your research logs to keep track of what all you have to do. Then fill in the provided train.py script to train a language model to get a good performance. Finally, you should submit the predictions of your best model for the test set as a submission.csv as described in the evaluation_details.txt file.

## Data (already staged in `/workspace`)
The files referenced by `train.py` are in the working directory.

## Submission — REQUIRED
Write `submission.csv` with columns `text_id,cohesion,syntax,vocabulary,phraseology,grammar,conventions`.

Scoring: **MCRMSE** (LOWER is better) on a held-out split.

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
