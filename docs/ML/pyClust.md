Clustering is a type of unsupervised learning that allows us to find groups of similar objects, objects that are more related to each other than to the objects in other groups. This is often used when we don’t have access to the ground truth, in other words, the labels are missing.

Examples of business use cases include the grouping of documents, music, and movies based on their contents, or finding customer segments based on purchase behavior as a basis for recommendation engines.

The goal of clustering is to separate the data into groups, or clusters, with more similar traits to each other than to the data in the other clusters.

In general, there are four types:

+ **Centroid based models** - each cluster is represented by a single mean vector (e.g., [k-means](#k-means)),

+ **Connectivity based models** - built based on distance connectivity (e.g., hierarchical clustering)

+ **Distribution based models** - built using statistical distributions (e.g., Gaussian mixtures)

+ **Density based models** - clusters are defined as dense areas (e.g., DBSCAN)

## K-means

The algorithm has gained great popularity because it is easy to implement and scales well to large datasets. However, it is difficult to predict the number of clusters, it can get stuck in local optimums, and it can perform poorly when the clusters are of varying sizes and density.

One major shortcoming of k-means is that the random initial guess for the centroids can result in bad clustering, and k-means++ algorithm addresses this obstacle by specifying a procedure to initialize the centroids before proceeding with the standard k-means algorithm. In scikit-learn, the initialization mechanism is set to k-means++, by default.

**Pre-processing: Standardization**

``` py
from sklearn.cluster import KMeans
from sklearn.datasets import load_wine

wine = load_wine()
from sklearn.preprocessing import StandardScaler
# instantiate the scaler
scale = StandardScaler()
# compute the mean and std to be used later for scaling
scale.fit(X)
# StandardScaler(copy=True, with_mean=True, with_std=True)
X_scaled = scale.transform(X)
```