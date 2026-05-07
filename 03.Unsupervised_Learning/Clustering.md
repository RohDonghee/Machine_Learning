# Clustering

## Fundamentals of Clustering
Clustering is a core Unsupervised Learning task aimed at grouping a set of unlabeled objects so that objects within the same group (cluster) are highly similar, while objects in different groups are dissimilar.

*   **Core Objective:** Maximize inter-cluster distances (separation) while minimizing intra-cluster distances (cohesion).
*   **Ambiguity:** Unlike supervised learning, there is no definitive "right" answer for clustering. The optimal number of clusters often depends on the business context and how the results will be used.

| Application Area | Description & Examples |
| :--- | :--- |
| **Data Understanding** | Discovering underlying structures. Examples include market segmentation (grouping customers by behavior) and grouping similar documents or genes. |
| **Data Summarization** | Reducing the size of large datasets by treating clusters as single units. Examples include image compression and geographic aggregations. |
| **Anomaly Detection** | Identifying outliers that sit far away from any normal clusters. Examples include credit card fraud detection and fake news detection. |

## Partitional Clustering: K-means
K-means is a partitional clustering approach that divides data objects into non-overlapping subsets (clusters).

*   **Algorithm Steps:**
    1. The number of clusters ($K$) must be specified in advance.
    2. Randomly initialize $K$ centroids (center points).
    3. Assign each data point to the cluster with the closest centroid.
    4. Update the centroids by computing the mean (or median) of the points assigned to each cluster.
    5. Repeat the assignment and update steps until the centroids no longer change (convergence).
*   **Initialization Dependency:** The final result is highly sensitive to the initial placement of centroids. Poor initialization can lead to suboptimal clustering. Solutions include multiple random runs, using domain knowledge, or selecting widely separated initial points.
*   **Data Normalization:** Since K-means relies heavily on distance measures (like Euclidean), attributes with different scales must be standardized (e.g., Z-scores) prior to clustering.

| Metric / Evaluation | Description & Usage |
| :--- | :--- |
| **WCSS (Within-Cluster Sum of Squares)** | Measures the sum of squared distances between points and their respective centroids. It improves (decreases) in each iteration. Used in the **"Elbow/Knee" method** to choose the optimal $K$ where WCSS stops decreasing significantly. |
| **Silhouette Score** | Measures both cohesion (closeness within a cluster, $a_i$) and separation (distance to the nearest neighboring cluster, $b_i$). Score ranges from -1 to 1. A score > 0.5 indicates reasonable clustering; > 0.7 indicates strong, well-separated clusters. |

| K-means Limitations | Solutions / Mitigations |
| :--- | :--- |
| **Differing Sizes/Densities** | Struggles when natural clusters have vastly different sizes or point densities. |
| **Non-globular Shapes** | Fails to accurately group clusters that have complex, non-spherical shapes. |
| **Sensitive to Outliers** | Outliers drastically distort the "mean" centroid calculation. **Solution:** Remove outliers before clustering or use the median instead of the mean for updates. |
| **Overcoming Method** | Create a large number of smaller sub-clusters initially, then merge them in a post-processing step. |

## Hierarchical Clustering
Hierarchical clustering produces a set of nested clusters organized as a tree, eliminating the need to specify the number of clusters ($K$) in advance.

*   **Bottom-Up (Agglomerative) Approach:** Starts with each individual data point as its own cluster. It recursively finds the closest pair of clusters and merges them until all points are fused into a single massive cluster.
*   **Dendrogram:** A tree-like diagram recording the sequence of merges. Lines connected lower down on the tree indicate points that were merged earlier (i.e., they are more similar). By drawing a horizontal cutoff line across the dendrogram, you can manually determine the desired number of clusters.

| Linkage Criteria (Cluster Distance) | Mechanism & Characteristics |
| :--- | :--- |
| **Single Linkage (MIN)** | Distance is measured between the two *closest* members of each cluster. It has a strong tendency to form long, elongated chains. |
| **Complete Linkage (MAX)** | Distance is measured between the two *farthest* members of each cluster. It creates tighter clusters but is highly sensitive to outliers. |
| **Average Linkage** | Distance is the average of all possible pair distances between the two clusters. It acts as a stable compromise between MIN and MAX. |

## Best Practices and Quality Assurance
Extracting meaningful results from clustering often requires heavy human intuition and data processing.

| Processing Phase | Key Actions & Desirable Features |
| :--- | :--- |
| **Pre/Post-processing** | Normalize data and remove outliers beforehand. Afterward, eliminate excessively small clusters, split overly "loose" clusters (high WCSS), and merge adjacent tight clusters. |
| **Cluster Separation** | A good model should exhibit a high ratio of between-cluster variation compared to within-cluster variation. |
| **Cluster Stability** | A reliable cluster structure should not drastically change when subjected to slight modifications in the input data. |
| **Interpretation** | Validate clusters using summary statistics or variables *not* used during the training phase. Assign human-understandable labels to the resulting groups. |
