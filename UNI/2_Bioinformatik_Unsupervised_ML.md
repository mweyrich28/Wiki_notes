# Unsupervised Machine Learning
:unsupervised_machinelearning:machine_learning:
1. Vl →  [Slides](file:///home/malte/OneDriver/01_Studium/2.Semester/Einführung in die Bioinformatik II/Slides/Bioinf2-Lect03-Unsupervised_Machine_Learning.pdf)
2. Tutorium Slides: [Slides](file:///home/malte/OneDriver/01_Studium/2.Semester/Einführung in die Bioinformatik II/Tutorien/2_Ex_EiB2_unsupervised_learningstudents.pptx.pdf)

## Clustering and Graph based Clustering
*DEFINITIONS AND TERMINOLOGY*
- Clusters: groups of similar objects
- Clustering: process of grouping unlabeled objects into clusters
*WHY*
- Uncover hidden structures in data


### Prototype-based Clustering: K-means
:k_means:kmeans:
1. Choose k, k = number of clusters
2. Randomly select k points as cluster centers (centroids)
3. Assign each point to the closest cluster center (euclidean distance)
4. Update cluster centers as the mean of the assigned points (mean of x and y coordinate)
5. Repeat steps 3 and 4 until no point changes cluster membership

#### How to choose k?
:elbow_method:silhouette_score:
##### Elbow method
plot the sum of squared error (SSE) for some values of k. 
The SSE is defined as the sum of the squared distance between each member of the cluster 
and its centroid. The idea is to choose a small value of k that still has a low SSE, 
and the elbow usually represents where we start to have diminishing returns by increasing k.
![Elbow Plot](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/Machinelearning/elbow.png)

#### Silhouette score
Sc = (x - y) / max(x, y), where 
- *_x_*:= is the mean distance to the *instances of the next nearest cluster*.
- *_y_*:= is the mean distance to the *other points in the same cluster* and 
Sc measure how well each data point fits into its cluster. 
The silhouette value is a measure of how similar an object is to its own cluster 
(cohesion) compared to other clusters (separation). 
The silhouette ranges from −1 to +1, where a *high value* indicates that the object 
is *well matched to its own cluster* and poorly matched to neighboring clusters. 
*If most objects have a high value, then the clustering configuration is appropriate.* 
If many points have a low or negative value, then the clustering configuration may have too many or too few clusters.
![Silhouette Plot](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/Machinelearning/silhouette.png)

#### Important difference between hierarchical clustering and k-means clustering
*K-MEANS CLUSTERING:*
- Tries to put the data into the number of clusters you specify at the beginning (k)

*HIERARCHICAL CLUSTERING:*
- Does not require you to specify the number of clusters at the beginning
- Just tells you, pairwise, which data points are most similar to each other
- We decide where to prune 

#### When clould k-means clustering fail
- When clusters have *similar sizes*
- When clusters have *similar variance*
- When clusters are *nested*
- When clusters are isotropic (same shape and size)
- ![Tricky cases](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/Machinelearning/kmeans_challanges.png)

### Hierarchical Clustering
:hierarchical_clustering:
- Group similar objects into groups called clusters and build a hierarchy of clusters.
- Results in a *tree-based* representation of the objects, which is called a *dendrogram*.
*TWO APPROACHES:*
- *Agglomerative:* Start with each object in its own cluster and merge clusters bottom-up↑
- *Divisive:* Start with all objects in one cluster and split clusters top-down ↓

#### The linkage criteria
:linkage_criteria:
Further reading: https://stackabuse.com/hierarchical-clustering-with-python-and-scikit-learn/ 
- *Ward:* Minimizes the sum of squared differences within all clusters. 
  It is a variance-minimizing approach and in this sense is similar to the k-means objective function but
  tackled with an agglomerative hierarchical approach.
  ![Ward Linkage](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/Machinelearning/ward.png)
- *Single linkage:* Minimizes the distance between the closest observations of pairs of clusters.
- *Maximum/Complete linkage:* Minimizes the maximum distance between observations of pairs of clusters.
- *Average linkage:* Minimizes the average of the distances between all observations of pairs of clusters.
→  ![Linkage criteria](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/Machinelearning/linkage_criteria.png)

Example:
- The dissimilarity between A and B is the largest dissimilarity between any element of A and any element of B. 
  →  Maximum/Complete linkage
- The dissimilarity between A and B is the smallest dissimilarity between any element of A and any element of B. 
  →  Single linkage
- The dissimilarity between A and B is the average dissimilarity between any element of A and any element of B. 
  →  Average linkage

#### Exercise: Hierarchical Clustering
![Average dissimilarity](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/Machinelearning/exercise_hc.png)

### Density-based Clustering: DBSCAN
:density_based_clustering:dbscan:

*DBSCAN: Density-Based Spatial Clustering of Applications with Noise*
- Can identify nested clusters in high dimensional data

PARAMETERS:
- $\epsilon =$ highest distance between two points to be considered neighbors: 
  _Epsilon Neighborhood_ $N_{\epsilon}(q)$ 
  Set of points within $\epsilon$-neighborhood of q: $N_{\epsilon}(q) = \Big\{p \in D | dist(p,q) \leq \epsilon\Big\}$
- $minPts =$ minimum number of points to form a dense region

TERMINOLOGY:
- *Core point:* A point p is a core point if: at least minPts points are within distance $\epsilon$ of it (including p).
- ![Core Point](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/Machinelearning/core_piont.png)
- *Border point & Noise:* A point q is a border point if: it is within distance $\epsilon$ of a core point, but is not itself a core point.
- ![Border Point](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/Machinelearning/border_point.png)
- *Directly density-reachable (DDR)*: A point p is _directly density-reachable_ from a point q if: $p \in N_{\epsilon}(q)$ and q is a core point
- *Density-reachable (DR):* A point p is _density-reachable_ from a point q if there is a chain of DDR points $p_1, ..., p_n$ with $p_1 = q$ and $p_n = p$.
- *Density-connected (DC):* A point p is _density-connected_ to a point q if there is a point o such that both, p and q are density-reachable from o.
![Picture](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/Machinelearning/dbscan_term.png)

#### DBSCAN Algorithm: Step by step
1. Choose a value for $\epsilon$ and minPts
2. Initialize all points as unvisited and the number of clusters to 0 and pick a random point $p$ from the dataset
3. If $p$ has not been classified (to a cluster or noise):
	a) If $p$ is no core point: mark $p$ as noise
	b) If $p$ is a core point: gather all unclassified DR points into a new cluster C. 
	   Mark all points in C as visited.
4. Repeat steps 2 and 3 until all points are classified

Video: https://www.youtube.com/watch?v=RDZUdRSDOok

#### DBSCAN Pitfalls
DBSCAN is sensitive to the choice of $\epsilon$:
- If $\epsilon$ is too small, a large part of the data will not be clustered and marked as noise
- If $\epsilon$ is too large, clusters will merge and the majority of objects will be in the same cluster
- Clusters of varying densities: choose different $\epsilon$ for different clusters

### Graph-based Clustering
:graph_based_clustering:louvain_method:modularity:

#### Louvain Method
- A method for detecting communities in large networks
- It maximizes a modularity score for each community
- Very fast modularity-based algorithm for detecting communities
- Reveals a hierarchical decomposition of the network, which is useful for understanding which scale of communities exist in the network

##### Modularity
- A measure of the quality of a particular division of a network into communities
- Fraction of edges that fall within the given clusters minus the expected fraction if edges were distributed at random
- The higher the modularity, the better the division into communities

Given two nodes A and B:
- $Q_{AB} := A_{AB} - \frac{k_{A} \cdot k_{B}}{m}$, if $Q_{AB} \ge 0$: join
- $A_{AB}$ := Weight of connection between A and B
- $k_{A}$  := Sum of weights of all connections of A
- $k_{B}$  := Sum of weights of all connections of B
- $m$      := Sum of all weights in the network

#### Phases-Louvain Clustering
:phases_louvain_clustering:

*Phase 1 - Step 0:*
- Each node is assigned to its own community
- Choose a start node and calculate the modularity gain of moving it to each of its neighbors communities
*Phase 1 - Step 1:*
- Start node joins the node/community that gives the highest modularity gain
- Repeat step 0 and 1 for all nodes
*Phase 1 - Step 2:*
- This leads to communities that can be aggregated into super-communities
*Phase 2:*
- Repeat step 1 and 2 until no further improvement is possible

##### EXAMPLE
![Calculating Modularity](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/Machinelearning/Louvian_Method/Louvian.png)
- *Note: Images of Phase 1: Step 0-1 are referring to the graph on Slide 58*
![Phase 1 Step 0](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/Machinelearning/Louvian_Method/Phase1_0.png) After joining AC into a community, 
  we don't have to check the edges of A anymore
- ![Phase 1 Step 1](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/Machinelearning/Louvian_Method/Phase1_1.png)
- ![Phase 1 Step 2](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/Machinelearning/Louvian_Method/Phase1_2.png)
