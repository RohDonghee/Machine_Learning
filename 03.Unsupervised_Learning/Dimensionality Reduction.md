# Dimensionality Reduction

## Fundamentals of Dimensionality Reduction
Dimensionality reduction is the process of reducing the number of features (variables) in a dataset while retaining as much meaningful information as possible.
*   **The Curse of Dimensionality:** As the number of features increases, the volume of the feature space grows exponentially. Data becomes sparse, making distance-based metrics (e.g., Euclidean distance) less effective and models more prone to overfitting.
*   **Core Objectives:** Overcome the curse of dimensionality, reduce computational complexity/storage costs, eliminate noise and highly correlated variables (multicollinearity), and compress data for 2D/3D visualization.

| Approach | Description | Examples |
| :--- | :--- | :--- |
| **Feature Selection** | Selecting a subset of the original features without altering them. | Forward selection, backward elimination, Lasso regularization. |
| **Feature Extraction** | Creating entirely new features by projecting or combining the original data into a lower-dimensional space. | PCA, t-SNE, UMAP, Autoencoders. |

## Principal Component Analysis (PCA)
PCA is a foundational linear dimensionality reduction technique. It identifies the directions (axes) that maximize the variance in the dataset.
*   **Mechanism:** It calculates the covariance matrix of the data and extracts its eigenvectors and eigenvalues. The eigenvectors form the new feature axes (Principal Components), and the eigenvalues represent the amount of variance captured by each component.
*   **Orthogonality:** All extracted Principal Components are mathematically guaranteed to be orthogonal (uncorrelated) to one another. The first component captures the maximum possible variance, the second captures the maximum remaining variance, and so on.
*   **Strict Prerequisite:** PCA is extremely sensitive to the scale of the data. Features with larger ranges will disproportionately dominate the components. **Data standardization (e.g., Z-score normalization) is absolutely required** before applying PCA.

| Characteristic / Metric | Description |
| :--- | :--- |
| **Explained Variance Ratio** | A metric indicating the percentage of total dataset variance captured by each principal component. Used to decide how many components to keep (e.g., keeping enough components to reach 90% cumulative variance). |
| **Linear Limitations** | Because PCA uses simple linear combinations, it fails to capture complex, non-linear relationships or curved manifolds in the data. |

## t-Distributed Stochastic Neighbor Embedding (t-SNE)
t-SNE is a non-linear dimensionality reduction technique explicitly designed for embedding high-dimensional data for visualization in a low-dimensional space (2D or 3D).
*   **Mechanism:** It calculates the probability that two points are neighbors in the high-dimensional space and does the same in the low-dimensional space. It then minimizes the divergence (Kullback-Leibler divergence) between these two probability distributions.
*   **Focus on Local Structure:** t-SNE excels at grouping similar data points together into distinct clusters, making it highly effective for visualizing class separability.
*   **The Perplexity Hyperparameter:** A crucial setting that balances attention between local and global aspects of the data. It roughly estimates the number of close neighbors each point has.

| Limitations of t-SNE | Description |
| :--- | :--- |
| **Meaningless Global Distance** | While points within a single cluster are similar, the distance *between* different clusters in a t-SNE plot is not mathematically meaningful. |
| **Computational Cost** | Highly computationally expensive and slow for very large datasets compared to PCA. |
| **Not for Feature Engineering** | Because it is non-parametric and lacks an explicit mapping function, t-SNE cannot be reliably used to transform *new, unseen* data into the existing embedding space. It is strictly a visualization tool. |

## Uniform Manifold Approximation and Projection (UMAP)
UMAP is a modern, state-of-the-art non-linear dimensionality reduction algorithm built on solid mathematical foundations of Riemannian geometry and algebraic topology.
*   **Mechanism:** It constructs a high-dimensional fuzzy topological representation of the data and then optimizes a low-dimensional layout to be as structurally similar as possible.
*   **Preservation of Global Structure:** Unlike t-SNE, UMAP is designed to preserve both the local structures (clusters) *and* the global distances between those clusters.
*   **Scalability:** It is significantly faster and more computationally efficient than t-SNE, making it suitable for massive datasets.

| Key Hyperparameters | Impact on Output |
| :--- | :--- |
| `n_neighbors` | Controls the balance between local and global structure. Low values focus strictly on local neighborhood, while high values force the algorithm to see the broader global layout. |
| `min_dist` | Controls how tightly points are packed together in the low-dimensional space. Low values create dense, separate clusters, while high values provide a broader, less clumped topology. |

## Summary Comparison: PCA vs. t-SNE vs. UMAP

| Feature | PCA | t-SNE | UMAP |
| :--- | :--- | :--- | :--- |
| **Type** | Linear | Non-linear | Non-linear |
| **Primary Goal** | Variance maximization, noise reduction, general feature extraction. | High-quality 2D/3D visualization of clusters. | Visualization, general feature extraction, and clustering preprocessing. |
| **Structure Preserved** | Global variance. | Local neighborhoods (clusters). | Both Local and Global structure. |
| **Speed** | Very Fast | Slow | Fast |
| **Applies to New Data?** | Yes (explicit linear mapping). | No. | Yes. |
