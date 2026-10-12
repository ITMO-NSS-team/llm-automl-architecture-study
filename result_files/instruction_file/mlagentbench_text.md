## Specialized library to use — REQUIRED
Use a pre-installed transformer library as the primary approach: **HuggingFace
`transformers`** (fine-tune / embed a pretrained encoder) or **sentence-transformers**
for text embeddings + a lightweight head — do **not** rely on bag-of-words alone.
Consult the library docs (staged under `/opt/docs/` if present) for exact APIs.

## Hardware — REQUIRED, STRICT
Resolve the compute device with EXACTLY this snippet, before any training:
```python
import torch
DEVICE = ('cuda' if torch.cuda.is_available()
          else 'mps' if torch.backends.mps.is_available() else 'cpu')
print('DEVICE=', DEVICE)
```
You MUST NOT hardcode `'cuda'`, and you MUST NOT write a CUDA-only check such as
`'cuda' if torch.cuda.is_available() else 'cpu'` — on a machine whose accelerator is
Apple MPS that silently drops you to CPU and training becomes ~10x slower.
Move the model AND every batch to `DEVICE`; print the `DEVICE=` line so the log
proves which device was used. On `mps` keep tensors float32 (no float64).

## Training discipline — REQUIRED
Do NOT stop after an arbitrary small budget (5 or 15 epochs is almost always badly
undertrained). Choose a budget large enough to converge — for a small CNN/U-Net or a
fine-tuned encoder on this data ~100 epochs is a sane starting point — and use early
stopping with patience on a held-out split. If the validation metric is still improving
when you stop, raise the budget and train again.
Validate with the TASK'S OWN metric (the one named in the instruction), not just the
training loss, and print `VALIDATION_SCORE=<value>`.

## Decision threshold — REQUIRED when predictions are thresholded
For binary / multi-label / segmentation outputs, do NOT leave the threshold at the
default 0.5. Sweep candidate thresholds on the validation split and keep the one that
maximises the task metric. With rare positives, 0.5 typically predicts nothing at all.
If positives are rare, weight them in the loss accordingly.

## Beat a trivial baseline — REQUIRED
Before submitting, score at least one trivial predictor on your validation split with
the TASK'S OWN metric — per-target median / most-frequent class, or the training mean —
and print both numbers. If your trained model does not beat the trivial predictor, do
not submit the model: fix it, or submit the simpler predictor that actually scores
better. Merely MATCHING the trivial score is also a failure — it means the model
collapsed onto the majority answer; change the approach rather than submitting it.
Think about what the metric rewards, not just about fitting the data — but a metric-aware
CONSTANT is not an answer. Your submission MUST be the output of a model fitted on the
features: predictions have to vary across rows, and for a multi-target problem across
every target. Before submitting, print the number of distinct predicted values per target;
if any target has fewer than 10, the model has collapsed — fix it rather than submit it.

## Sanity-check the submission — REQUIRED
Before finishing, inspect what you are about to submit. A submission that is empty,
constant, all-negative or otherwise degenerate scores ~0 even when training looked
fine. If you see that, fix the cause (threshold, class weighting, longer training)
instead of submitting it.

## Time budget management — REQUIRED
Assume you have hours, not minutes: this run is not tightly time-boxed. At the start
allocate your wall-clock budget across stages (exploration / training / improvement /
finalisation) and print the allocation, then check elapsed time between stages.
Training the model to convergence is NOT 'optional work' — never cut the number of
epochs to finish early. Drop optional exploration instead. As a rule of thumb, if the
whole training phase finished within a couple of minutes you almost certainly
undertrained: raise the epoch budget and train again until the validation metric
stops improving.

## Keep the best model — REQUIRED
Save every model variant you train together with its validation score. Your FINAL
submission predictions MUST come from the variant with the BEST validation score —
never simply the last one trained.
