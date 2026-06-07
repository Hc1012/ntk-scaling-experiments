# ntk-scaling-experiments

Independent reproduction and gate-budget scaling study of [ntkmirror](https://github.com/leochlon/ntkmirror) (Hassana Labs), run on a free Colab T4.

## What this is

ntkmirror adapts frozen language models without changing weights — it learns a small set of per-channel "dials" applied during the forward pass. Controllers compose by addition because different tasks' dials are near-orthogonal.

Two questions not covered by the repository:

1. Does accuracy keep improving as gate budget scales up, and does composability survive?
2. Does NTK-duality (reachability) scale the same way as accuracy?

## Key finding

They diverge. Accuracy improves monotonically from 256 to 5,000 gates with no plateau. Reachability (measured via `dual-diagnose`) improves steeply to ~1,024 gates, then saturates. Gates added beyond that improve task performance through something other than better approximating the fine-tuning field.

## Results

| Gates | Maths NLL ↓ | Realized residual ↓ |
|-------|------------|---------------------|
| 256   | 0.593      | 10.17               |
| 512   | 0.580      | 9.19                |
| 1024  | 0.572      | 4.24                |
| 2000  | 0.560      | 4.90                |
| 3500  | 0.547      | 3.66                |
| 5000  | 0.540      | 4.43                |

## Full writeup

[hc1012.github.io/ntk-scaling-experiments](https://hc1012.github.io/ntk-scaling-experiments/)

## Files

- `index.html` — formatted writeup with embedded charts
- Raw data in `sweep_results.json` and `reachability_results.json` (add these)

## Model and hardware

Qwen2.5-0.5B-Instruct, free Colab T4 GPU.
