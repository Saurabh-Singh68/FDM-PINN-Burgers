# Current Experimental Results

These values were extracted from the uploaded Jupyter HTML export.

## AD-PINN

- Epochs: 10,000
- Optimizer: Adam
- Learning rate: 1e-3
- Training time: 242.59 s
- Final total loss: 6.888920e-04
- Relative L2 error: 3.631237e-02

## FDM step-size study

| h | Relative L2 Error | PDE Residual MSE | Training Time (s) |
|---:|---:|---:|---:|
| 1e-1 | 4.366016e-01 | 1.775516e-02 | 74.17 |
| 1e-2 | 1.992037e-01 | 1.247763e-02 | 54.23 |
| 1e-3 | 2.291760e-01 | 1.041085e-02 | 51.50 |

## Reproducibility note

The current AD and FDM experiments use different epoch counts, so the recorded times are not yet a fair speed comparison. A controlled experiment is required before making a computational-efficiency claim.
