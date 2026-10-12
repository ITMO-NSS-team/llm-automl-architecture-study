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
Think about what the metric rewards, not just about fitting the data. For example
SMAPE applies its maximum penalty whenever the true value is 0 and your prediction is
non-zero — however small — so for a target that is often exactly 0, predicting exactly
0 on those rows can matter more than fitting the non-zero rows precisely.

## Sanity-check the submission — REQUIRED
Before finishing, inspect what you are about to submit. A submission that is empty,
constant, all-negative or otherwise degenerate scores ~0 even when training looked
fine. If you see that, fix the cause (threshold, class weighting, longer training)
instead of submitting it.

## Keep the best model — REQUIRED
Save every model variant you train together with its validation score. Your FINAL
submission predictions MUST come from the variant with the BEST validation score —
never simply the last one trained.
