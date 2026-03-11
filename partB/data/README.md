# Dataset Information for Part B

## Dataset Used: Synthetic time-series (random-walk with embedded sine query)

### How to Obtain
This dataset is generated programmatically using NumPy. No manual download is required. The dataset is created at runtime inside the notebooks using:

```python
import numpy as np

SEED = 42
rng = np.random.default_rng(SEED)

m = 128
T_len = 2000
x = np.linspace(0, 2 * np.pi, m)
Q = np.sin(2 * x) + 0.1 * rng.normal(size=m)
base = rng.normal(0, 0.6, T_len).cumsum()

embed_start = 700
T = base.copy()
T[embed_start:embed_start + m] = Q + 0.05 * rng.normal(size=m)

np.savez("partB/data/synthetic_series.npz", T=T, Q=Q, embed_start=embed_start)
```

### How It Is Used
- **task 1 1.ipynb, task 1 2.ipynb, task 1 3.ipynb**: Only markdown cells, no dataset needed.
- **task 2 1.ipynb**: Dataset justification and preprocessing are documented.
- **task 2 2.ipynb**: UCR-DTW subsequence search implementation applied to this dataset.
- **task 2 3.ipynb**: Results, comparison plot, and reproducibility checklist.
- **task 3 1.ipynb**: Ablation experiments comparing full UCR-DTW vs ablated components.
- **task 3 2.ipynb**: Failure mode analysis using `failure_series.npz` (near-constant series).

### Dataset Properties
- **Series length**: 2000
- **Query length**: 128
- **Candidate subsequences**: 1873 (2000 - 128 + 1)
- **Features per sample**: 128 time points
- **Signal type**: 1D continuous time series
- **No manual steps required**: All data is generated in-memory
