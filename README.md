# DiRe - JAX

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)


<!-- CI status from GitHub Actions -->
[![CI](https://img.shields.io/github/actions/workflow/status/sashakolpakov/dire-jax/pylint.yml?branch=main&label=CI&logo=github)](https://github.com/sashakolpakov/dire-jax/actions/workflows/pylint.yml) <!-- Docs status from GitHub Actions -->
[![Docs](https://img.shields.io/github/actions/workflow/status/sashakolpakov/dire-jax/deploy_docs.yml?branch=main&label=Docs&logo=github)](https://github.com/sashakolpakov/dire-jax/actions/workflows/deploy_docs.yml) <!-- Docs health via HTTP ping -->
[![Docs](https://img.shields.io/website-up-down-green-red/https/sashakolpakov.github.io/dire-jax?label=API%20Documentation)](https://sashakolpakov.github.io/dire-jax/)






### A new DImensionality REduction package written in JAX 

We offer a new dimension reduction tool called DiRe - JAX that is benchmarked against the existing approaches: UMAP (original and Rapids.AI versions), and tSNE (Rapids.AI version)

### Quick start

Do either

```bash    
pip install dire-jax
```

if you need to install the main DiRe class only

```bash
pip install dire-jax[utils]
```

if you also need the benchmarking utilities.

> **Note**: For GPU or TPU acceleration, JAX needs to be specifically installed with hardware support. See the [JAX documentation](https://github.com/google/jax#installation) for more details on enabling GPU/TPU support.


Then, do the imports

```python
from dire_jax import DiRe
from dire_jax.dire_utils import display_layout
```

and afterwards, for example, try this: 

```python
from sklearn.datasets import make_blobs

n_samples  = 100_000
n_features = 1_000
n_centers  = 12
features_blobs, labels_blobs = make_blobs(n_samples=n_samples, n_features=n_features, centers=n_centers, random_state=42)

reducer_blobs = DiRe(dimension=2,
                     n_neighbors=16,
                     init_embedding_type='pca',
                     max_iter_layout=32,
                     min_dist=1e-4,
                     spread=1.0,
                     cutoff=4.0,
                     n_sample_dirs=8,
                     sample_size=16,
                     neg_ratio=32,
                     verbose=False,)

_ = reducer_blobs.fit_transform(features_blobs)
reducer_blobs.visualize(labels=labels_blobs, point_size=4)

```

The output should look similar to

![12 blobs with 100k points in 1k dimensions embedded in dimension 2](images/blobs_layout.png)

### Documentation 

Please refer to the DiRe API [documentation](https://sashakolpakov.github.io/dire-jax/) for more instructions. 

### Working paper

Our working paper is available in the repository. [![View PDF](https://img.shields.io/badge/View-PDF-red?logo=adobe)](
  https://github.com/sashakolpakov/dire-jax/blob/main/working_paper/dire_paper.pdf
)

 Also, check out the Jupyter notebook with benchmarking results. [![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](
  https://colab.research.google.com/github/sashakolpakov/dire-jax/blob/main/tests/dire_benchmarks.ipynb
)


### Benchmarking and utilities

In order to run the Jupyter notebook in the ./tests folder, you need to install some extras:
```bash
pip install dire-jax[utils]
```

This installation will give you access to the utilities (metrics and benchmarking routines) that are 
specifically implemented to be used together with DiRe. However, some of them rely on external packages (especially for
persistent homology computations) that may have longer runtimes. 

### Contributing

Please follow the [contibuting guide](https://sashakolpakov.github.io/dire-jax/contributing.html). Thanks!

### Acknowledgement 

This work is supported by the Google Cloud Research Award number GCP19980904.
