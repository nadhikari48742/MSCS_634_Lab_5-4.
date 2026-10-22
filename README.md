# Lab 5: Clustering Techniques Using DBSCAN and Hierarchical Clustering

**Student Name:** Nikhil  
**Course:** MSCS 634  
**Assignment:** Lab 5 — Clustering Techniques Using DBSCAN and Hierarchical Clustering

## Purpose

The purpose of this lab is to explore and compare two unsupervised learning methods: Agglomerative Hierarchical Clustering and DBSCAN. The analysis uses the Wine dataset provided by `sklearn.datasets`. The notebook examines the data, standardizes the features, visualizes clustering results, and evaluates DBSCAN results using silhouette, homogeneity, and completeness scores.

## Dataset and Preparation

The Wine dataset contains 178 observations and 13 numerical features. The notebook loads the data from `sklearn.datasets.load_wine()` and uses pandas to inspect the first rows, data types, and descriptive statistics. The features are standardized with `StandardScaler` before clustering because the measurements have different numeric scales.

The known Wine class labels are used only for external evaluation metrics. They are not provided to either clustering algorithm during model fitting.

## Methods

### Agglomerative Hierarchical Clustering

Agglomerative clustering starts with individual observations and repeatedly merges groups. The notebook tests `n_clusters` values of 2, 3, 4, and 5 using Ward linkage. Scatter plots show the assignments using alcohol and color intensity, and a dendrogram illustrates how groups merge at different distances.

### DBSCAN

DBSCAN identifies dense groups of observations and labels observations that do not belong to a dense region as noise (`-1`). The notebook tests several combinations of `eps` and `min_samples`, plots the resulting assignments, and highlights noise points.

The notebook reports these evaluation metrics where they are valid:

- **Silhouette score:** Measures how well observations fit within their assigned clusters compared with other clusters.
- **Homogeneity score:** Measures whether each cluster contains observations from a single reference Wine class.
- **Completeness score:** Measures whether observations from the same reference class are assigned to the same cluster.

For DBSCAN, noise observations are excluded from the metric calculations where possible, and the number of excluded noise points is shown. Silhouette scores are not calculated when the remaining assignments do not meet the metric's requirements.

## Key Insights

The notebook provides a comparison of how hierarchical clustering and DBSCAN behave on the standardized Wine dataset. Hierarchical clustering always returns the requested number of clusters, making it useful when the number of groups is specified in advance. The dendrogram helps illustrate the order and distances at which groups merge.

DBSCAN does not require the number of clusters to be selected in advance and can identify noise points. Its results depend on the `eps` and `min_samples` settings. Different settings can produce different numbers of clusters and noise points, so the metric table and visualizations should be considered together when interpreting the results.

The scatter plots show only alcohol and color intensity for readability, while both algorithms use all 13 standardized features. Therefore, the two-dimensional plots do not display every difference used by the clustering algorithms. Run all notebook cells to see the actual cluster sizes, plots, and metric values produced by the tested settings.

## Challenges and Decisions

- **Feature scaling:** Standardization was applied so features with larger numeric ranges would not dominate distance calculations.
- **Choosing parameters:** Several cluster counts and DBSCAN parameter combinations were tested rather than relying on one setting.
- **Visual interpretation:** Two features were selected for two-dimensional plots, while clustering used all 13 features.
- **Noise handling:** DBSCAN noise points were identified separately. Evaluation metrics were calculated on non-noise observations when possible, and invalid silhouette cases were reported as unavailable rather than forcing a score.
- **Comparing results:** The notebook considers visualizations, cluster sizes, and evaluation metrics together because no single metric fully describes clustering quality.

## Files

- `Nikhil_Lab_5_Clustering_DBSCAN_Hierarchical.ipynb` — Jupyter Notebook containing the code, visualizations, metric tables, and analysis.
- `README.md` — Description of the lab, methods, insights, and decisions.

## How to Run the Notebook

1. Install Python with Jupyter Notebook or JupyterLab.
2. Ensure these packages are available: `numpy`, `pandas`, `matplotlib`, `scikit-learn`, `scipy`, and `nbformat` (the last package is not needed to run the analysis itself).
3. Open the notebook in Jupyter.
4. Run all cells from top to bottom.
5. Review the plots and metric tables, and read the written analysis at the end.

## Conclusion

This lab demonstrates how two clustering algorithms can produce different views of the same dataset. Agglomerative Hierarchical Clustering provides a hierarchy of merges and allows a chosen number of clusters, while DBSCAN detects dense regions and can mark noise. The most useful method depends on the structure of the data, the selected parameters, and the goal of the analysis.
