# **Unraveling High-Dimensional Data with Manifold Learning**


This notebook presents a study of **nonlinear dimensionality reduction** and **manifold learning** techniques across both **synthetic datasets** that explicitly satisfy the manifold hypothesis and **real-world datasets** that may only approximately exhibit low-dimensional local structure. We compare manifold learning algorithms with respect to:

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

# Mathematical Foundations
---

## Manifolds

A **manifold** is a topological space $\mathcal{M}=(X,\tau)$ that is

1. **Hausdorff**: for each $x,y\in X$ with $x\not=y$, there exists open sets $U_x, U_y$ such that $U_x\cap U_y=\phi.$

2. **Second-Countable**: the topology $\tau$ admits a countable basis.

3. **Locally Euclidean of Dimension $n$**: for each $x\in X$, there exists some open neighborhood $U_x\in\tau$ and a homeomorphism $\varphi: U\mapsto U'\subset\mathbb{R}^n$. Such a homeomorphism $\varphi$ is called a chart of $\mathcal{M}$.

### $C^k$-Diffeomorphisms & Atlases

Given two charts $(U,\varphi)$ and $(V,\psi)$ with $U\cap V\not=\phi$, the **transition map** is given by the map $\omega_{\varphi,\psi}:\psi\circ\varphi^{-1}:\varphi(U\cap V)\mapsto\psi(U\cap V)$. A **$C^k$-diffeomorphism** requires that

1. $\omega$ is bijective.
2. $\omega\in C^k(\varphi[U\cap V])$.
3. $\omega^{-1}\in C^k(\psi[U\cap V])$.

Two charts $(U,\varphi), (V,\psi)$ are said to be **$C^k$-smoothly compatible** if the transition map $\omega_{\varphi,\psi}$ is a $C^k$-diffeomorphism.


An **atlas** $\mathcal{A}$ on $\mathcal{M}$ is an indexed family collection of charts that cover $\mathcal{M}$. An atlas $\mathcal{A}=\{(U_i,\varphi_i)_{i\in I}\}$ is a **$C^k$-atlas** if any two charts in $\mathcal{A}$ are $C^k$-smoothly compatible. A **maximal $C^k$-atlas** $\mathcal{A}$ satisfies:

1. $\mathcal{A}$ is a $C^k$-atlas.
2. For any other $C^k$-atlas $\mathcal{B}$, $\mathcal{A}\not\subseteq\mathcal{B}$.
