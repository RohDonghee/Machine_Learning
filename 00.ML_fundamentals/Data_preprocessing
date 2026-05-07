```markdown
# 1. Data and Data Preprocessing

## 1.1 Definition and Characteristics of Data
Data is fundamentally a collection of data objects and their corresponding attributes.
*   **Data Object:** A collection of attributes representing an entity. It is also referred to as a record, point, case, sample, or instance.
*   **Attribute:** A specific property or characteristic of an object (e.g., the eye color of a person or the temperature). It is also known as a variable, field, feature, or dimension.
*   **Key Characteristics of Data:** The overall structure and behavior of data are determined by its dimensionality (number of attributes), sparsity (where only the presence of non-zero values counts), resolution (where data patterns depend strongly on the scale), and size.

| Attribute Type | Description | Examples |
| :--- | :--- | :--- |
| **Discrete** | Has a finite or countably infinite set of values. They are often represented as integer variables. | Zip codes, car numbers, or binary attributes (0/1). |
| **Continuous** | Has real numbers as attribute values. Practically, they can only be measured and represented using a finite number of digits. | Temperature, height, weight. |
| **Asymmetric** | Attributes where only the presence of a non-zero value is regarded as important. | Words present in documents, items present in customer transactions. |

## 1.2 Types of Datasets
Datasets can be categorized based on how the data is structured and related.

| Dataset Category | Specific Types | Characteristics & Examples |
| :--- | :--- | :--- |
| **Record Data** | Data Matrix | Points in a multi-dimensional space with a fixed set of numeric attributes. Represented by an $m \times n$ matrix ($m$ objects, $n$ attributes). |
| | Document Data | Uses Bag-of-words (BOW) representation; each term becomes an attribute, and its value is the term frequency in the document. |
| | Transaction Data | Consists of a set of items involved in a single event (e.g., a set of products purchased by a customer during one shopping trip). |
| **Graph Data** | General Graphs | Made up of nodes (entities) and edges (relations). Example: Web pages connected by links. |
| | Molecular Structures | Nodes represent atoms (e.g., Carbon), and edges represent the connectedness (bonds) of atoms. |
| **Ordered Data** | Sequential/Genomic | Data where the sequence or order of elements is essential (e.g., the exact order of genes in DNA). |
| | Spatio-Temporal | Data that manages and tracks both spatial and temporal (time) information (e.g., average monthly temperature of oceans over time). |

## 1.3 Data Quality
The quality of data is paramount in data analysis; you cannot gain good analysis results from poor data, regardless of how advanced the machine learning or deep learning methods are. 

*   **Impact of Poor Quality:** Poor data quality negatively affects data processing efforts. It is essential to detect data problems and perform data cleaning before starting any serious analysis.

| Quality Issue | Description | Common Handling Methods |
| :--- | :--- | :--- |
| **Noise** | A modification or distortion of original values (e.g., the distortion of a person's voice on a poor phone line). | Filtering or smoothing techniques are typically required to reduce interference. |
| **Outliers** | Data objects with characteristics that are considerably different from most other objects in the dataset. | Remove them if they act as interfering noise. Keep them if the goal is anomaly detection (e.g., credit card fraud detection). |
| **Missing Values** | Occurs when information is not collected (e.g., survey refusal) or an attribute is not applicable to an object. | Eliminate affected data objects/variables, estimate values using mean/median/interpolation, or ignore them during analysis. |
| **Duplicate Data** | Data objects that are exact or near-duplicates of one another, often caused by merging heterogeneous data sources. | Conduct data cleaning to remove duplicates, unless there is a specific domain reason to keep them. |

## 1.4 Measures of Proximity: Similarity and Distance
Proximity metrics quantify how alike or different data objects are. These measures dictate the behavior of clustering and classification algorithms like K-Nearest Neighbors.

*   **Similarity Measure:** A numerical measure indicating how alike two data objects are. Its value is higher when objects are more alike and often falls within the range $$.
*   **Dissimilarity (Distance) Measure:** A numerical measure indicating how different two data objects are. Its value is lower when objects are more alike.
*   **Properties of a Metric:** For a distance to be considered a formal mathematical "metric", it must satisfy Positivity ($d(x,y) \ge 0$), Symmetry ($d(x,y) = d(y,x)$), Identity-discerning ($d(x,y) = 0$ iff $x = y$), and the Triangle Inequality ($d(x,z) \le d(x,y) + d(y,z)$).

| Measure | Formula / Concept | Key Characteristics & Use Cases |
| :--- | :--- | :--- |
| **Euclidean Distance (L2)** | $d(x, y) = \sqrt{\sum_{k=1}^{n} (x_k - y_k)^2}$ | Standard straight-line distance in Euclidean space. It is highly influenced by measurement scale, so standardization is strictly required. |
| **Manhattan Distance (L1)** | $d(x, y) = \sum_{k=1}^{n} \|x_k - y_k\|$ | Also known as Taxicab distance; measures the distance traveling strictly along orthogonal axes. |
| **Minkowski Distance** | $d(x, y) = (\sum_{k=1}^{n} \|x_k - y_k\|^p)^{1/p}$ | Generalized version of Euclidean and Manhattan distances ($p=1$ is Manhattan, $p=2$ is Euclidean, $p \to \infty$ is Supremum/L$\infty$). |
| **Cosine Similarity** | $\cos(v_1, v_2) = \frac{v_1 \cdot v_2}{\|v_1\| \|v_2\|}$ | Measures the inner product space angle. It is invariant to scaling and highly effective for document comparison (word frequencies). |
| **Pearson Correlation** | $\frac{\text{covariance}(x,y)}{\text{std}(x) \cdot \text{std}(y)}$ | Invariant to both scaling and translation. Useful for comparing the "shape" of time series, but fails to capture certain non-linear relationships. |
| **Entropy** | $H(X) = -\sum p_i \log_2 p_i$ | Average amount of information contained in a dataset (measured in bits). The less certain an outcome, the more information (entropy) it contains. |
| **Mutual Information** | $I(X, Y) = H(X) + H(Y) - H(X, Y)$ | Information one variable provides about another. Can handle non-linear relationships but is computationally intensive. |

## 1.5 Data Preprocessing Techniques
Preprocessing improves the quality of the raw data and transforms it to be more suitable for specific data mining tasks.

*   **Curse of Dimensionality:** When dimensionality increases, data becomes increasingly sparse. A large number of features requires exponentially more data samples for training, which can degrade algorithmic performance.

| Preprocessing Technique | Description | Main Purpose & Features |
| :--- | :--- | :--- |
| **Aggregation** | Combining two or more attributes (or objects) into a single attribute (or object). | Reduces data size, changes the scale (e.g., aggregating days into months), and creates more "stable" data by reducing variability. |
| **Sampling** | Selecting a representative subset of data. Types include Simple Random Sampling (with/without replacement) and Stratified Sampling. | Used when processing the entire dataset is too expensive or time-consuming. The sample must have approximately the same properties as the original data. |
| **Discretization** | The process of converting a continuous attribute into an ordinal/categorical attribute. | Often done using an equal interval width or equal frequency approach in both supervised and unsupervised settings. |
| **Binarization** | Mapping a continuous or categorical attribute into one or more binary variables. | A key step for techniques like Bag-of-words document representation. |
| **Attribute Transformation** | A function that maps the entire set of values of an attribute to a new set of replacement values. | Includes Normalization and Standardization ($z$-score: subtracting the mean and dividing by the standard deviation) to adjust scale differences. |
| **Dimensionality Reduction** | Techniques to reduce the amount of time and memory required by finding a projection that captures the largest amount of variation. | Helps avoid the "curse of dimensionality" and eliminates noise. Principal Components Analysis (PCA) is the most common technique. |
| **Feature Subset Selection** | Selecting only the most relevant features by removing redundant and irrelevant features. | Streamlines data (e.g., dropping student ID when predicting GPA, or removing tax if purchase price is already known). |
| **Feature Creation** | Creating new attributes that capture important information much more efficiently than the original attributes. | Includes feature extraction (e.g., edges from images), feature construction (e.g., mass/volume = density), and mapping to a new space (e.g., Fourier analysis). |
```
