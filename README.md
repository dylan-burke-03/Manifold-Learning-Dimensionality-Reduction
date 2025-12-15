# **Unraveling High-Dimensional Data with Manifold Learning**


This notebook presents a study of **nonlinear dimensionality reduction** and **manifold learning** techniques across both **synthetic datasets** that explicitly satisfy the manifold hypothesis and **real-world datasets** that may only approximately exhibit low-dimensional local structure. We compare classical and modern manifold learning algorithms with respect to:

- **Geometric fidelity** (local neighborhood preservation).
- **Clustering and separability quality** in low-dimensional embeddings.
- **Computational efficiency**.

For each dataset, we compute and visualize two-dimensional embeddings using:

- **t-Distributed Stochastic Neighbor Embedding (t-SNE)**
- **Isomap**
- **Spectral Embedding (Laplacian Eigenmaps)**
- **Locally Linear Embedding (LLE)**
- **Uniform Manifold Approximation & Projection (UMAP)**

Each embedding is plotted alongside the **original data** (in 3D when available, or through PCA otherwise) for direct visual comparison.

---
## Evaluation Metrics
We evaluate embeddings using **only built-in, rigorously defined metrics**:

- **Trustworthiness** — measures preservation of local neighborhoods from high- to low-dimensional space  
- **Silhouette Score** — evaluates cluster separation and cohesion  
- **Calinski–Harabasz Index** — ratio of between-cluster to within-cluster dispersion  
- **Davies–Bouldin Index** — average similarity between clusters (lower is better)  
- **k-Nearest Neighbor Classification Accuracy** — downstream task performance  
- **Runtime (seconds)** — empirical algorithmic efficiency

Metrics are displayed directly on each embedding plot and aggregated across datasets for global comparison.
