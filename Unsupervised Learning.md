# 1.1 Introduction to Clustering

- Unsupervised learning, but specifically clustering consists of working with data without a set dependent variable or output column that is data.
- Furthermore, it works by grouping data, or reducing its size to move forward.
- Take consumer data, and aggregating certain aspects of consumption, and creating groups or categorizations
- In summary - clustering is the mechanism of grouping similar items together, and unsimular items separated from them.
- Clustering is one form, or technique of Unsupervised Learning Techniques
- Cluster := Collection of objects that are similar
- There are measures of similarity to determine which columns are indeed similar
- Through clsutering - data is simplified or reduced from a many data points into a few clusters

- As mentioned, similarity has a measure, that we can call distance. Common distance measures include (i) Manhatten Distance; (ii) Eucledian Distance; (iii) Chebyshev Distance
- Euclidean measure is the most common, which is the usual measure through Pythag's theorem: (x1-x2)^{2} + (y1-y2)^{2} + ...
- Manhatten distances is |x1-x2| + |y1-y2| + ...
- Chebyshev distance (chessboard distance): max{|x1-x2|, |y1_y2|, ...}
- Minkowski distance is a formula that provides all distances
-   Let there be M columns, and let X and Y be two rows. Then
-   D = ( |x1-y1|^{p} + |x2-y2|^{p} + ... + |xM-yM|^{p} ) ^(1/p)
-   If p = 2 then D is Euclidean
-   If p = 1 then D is Manhatten
-   If p = inf then D is Chebyshev
-   Though p is any real number, and for every p, there is a new measure of distance

# 1.2 Types of Clustering

- There are two types of clustering (i) Connectivity based clustering (ii) Centroid based clustering (K-means clustering)
- Connectivity based clustering looks at the distance between every row, before determining the clusters. This is computationally expensive. If there are N rows, then there are N*(N+1)/2 calculations

- Centroid based clustering fixed the number of clusters or centroids, and calculates the distances to the centroids. If there are M centroids then number of calculations is M*N

- Dendograms are trees showing how the centroid clusters are formed. y-axis is distance and x-axis is objects

- Algorithms can be agglomerative meaning starting with 1 object and aggregating them into clusteres, or divisive, where one stats with complete data and divides them into partitions

- K-means clustering involves assigning points to cluster centroids based on their distance from the centroids and the distance metric used is Euclidean distance.

- K-means clustering algorithm scales in the order of n, while the agglomerative clustering algorithm scales in the order of n2.

# 1.3 K-mean Clustering

- To recall - consider N points. Under Connectivity based clustering - there will be N*(N+1)/2 distances between the N points, and those with the smaller distances will be considered to be more similar.

- Under Centroid based clustering - there is a given number of centroids. Distances these points are made to the centroids. Thsoe points that have similar distances to the centroid will be considered similar.

- The key distinction here is that similarity under the centroid approach is determined by distances to the centroid and NOT between the points themselves.

- K-means clustering is the most used clustering technique.
  - It works by minimizing the "within-cluster sum of squares", which is the usual expression of variance on the points, where the mean is the centroid's location.

 - The minimization process happens through Lloyd's algorithm, whcih works as follows
   - A K is given
   - K clusters are guessed across the data
   - Distances are calculated from each point, to each cluster
   - Those points that are closest to a cluser, are assigned to the group for that cluster
   - Given a group, a new cluster is selected that, in aggregate, is even closer to the points in that group
   - However, in saying that, new distances are calcualted to the new clusters in each group
   - If a point ends up being closer to a cluser in another group - then the process iterates
   - If the points do not move from the group - then the algorithm is complete, the the process has converged
     
 - The next question is what is optimal number of K. One way to visualize the effect of different values of K is through a graph, where the vertical axis is the within group sum of squares, and the horizontal axis is the number of clusters. We can expect to observe

   - When K = 1, we expect the sum of squares to be at its highest, and compression is highest as all data is compressed toa  single point.
   - When K -> inf, we expect the sum of squres to be at its lowest, the compression the least, and the accuracy the highest.

   - As K increases, the sum of squares decreases, and the question is at what K is the rate of decreases decreasing, such that the marginal decrease more an additional cluster is a waste of resources.

   - Visually, the "Elbow Method" is used, as the elbow of the arm reflects that K to select, as additional Ks have a ineffective marginal decrease.
  
# 1.4 K-means Clustering Hands-on

Just coding

# 1.5 Importance of Scaling

- Given the formula for calculating distance, columns with larger magnitudes will dominate the calcualtion. Therefore, performing scaling, where all columns/variables are have the same scale or magnitudes is required.

- One method of scaling is by performing Z-score scaling, or, the number of standard deviations from the mean, all of which are calculated using the standard statistics

-  Using different distance measures will lead to different clusters. Therefore, one may play around with different distances, and observe the clusters and the results.

-  The Euclidean Measure is one of the most popular methods to use, although are highly scale dependaent. Furthermore, it ignores the relationship between measurements, and is sensitive to outliers. If there are outliers, the Manhattan distance is preferred.

-  We consider another distance measure that considers the relationship between variables - and this called the Mahalanobis Distance.

-    One way to understand this relationship factor, is to understand that while two points may indeed be closer to a cluster, there is no information about the points' closeness to the general data itself.

-   First - determine the natural axis of the data, or the eigenvalues of the covariance matrix of the data. Then, different ellipses of varying distances may be drawn about the axis. In saying that, every point on the ellipsis is considered to be equal distance from the center of the data. As such, a new distance system has been established.

-   Back to the example of two points - if point A is on an ellipisis further away from the one that point B is on, then point A is considered to be of further distance from the data.

-   The formula for this distance is (x-xb)T C-1 (x-xb), where xb is the center, T is transpose and C-1 is the inverse of the covariance matrix.

-   Another distance metric is te JACCARD DISTANCE, which is used to measure the distance between sets of data, and given by 1 - J(A,B), where J(A,B) is the Jaccard Index on sets A and B.

-   The calculation of J(A,B) works off a counting method through | A int B| / |A uni B|. Therefore, if A and B are disjoint then J(A,B) = 0, and the distance is 1.

# 1.6 Applications of Clustering

- Image Processing: Clustering pixels representing objects in each frame
- Medical - Clustering patient attributes such as age, height and weight...
- Customer Segmentation: Clusters based on frequency of purchase, value...

# 1.7 Advantages & Disadvantages of K-means Clustering

- Strengths:
  -   Simple principles without the need for any complex statistical terms
  -   Once clusters and their associated centroids are identified, it is easy to assign new objects (e.g. new customers) to a cluser based on the object's distance from the closest centroid.
  -   Because the method is unsupervised, using the k-means helps to elininate subjectiovity from the analysis
  -   
- Weakness:
  - Choosing the value of K. While the 'Elbow Test' was described, it is more complicated then that
  - The k-means algorithm is sensitive to the starting position of the initial cetroid. Thus it is important to rerun the k-means analysis several tgimes for a particular value of K to ensure the cluster results provide the overall minimum Within-Sum-of-Squares
  - Susceptive to curve of dimensionality, where an increase in clusters means an exponential increase in computational requirements
  - The algorithm involves computation of mean, and so, is sensitive to outliers.
 
# 1.8 Silhouette Coefficient for K-means

- To measure the performance of K-means clustering for a given K, one can calcualte the Silhouette Coefficient defined by
  S = (B-A)/max(A,B)
  where A is the average distance of the ith from all other points in its cluster A, excluding itself.
  where B is the average distance of the same ith point from all other points in the nearest cluster B

  If A < B as expected in the optimization process, then 0 < S <= 1 
  If A = B then from the numerator S = 0
  If B < A then -1 <= S < 0
  
# 1.9 Visual Analysis of Clustering

- Visualizing data is the best way to understand data well.
- Graphing marginal densities and their clusters, at different marginal dimensions may allow us to understand the number of clusters.

# 1.10 Dynamic Clustering

- New clustering is pereformed with new data.
- We can observe how one customer or data moves from cluster to cluster
- New data can change the cluster structure, also exits or redundant data may have a similar effect
- Catalysts (customer coupons) may also change behaviours and therefore the structure of clusters
- Clusters may also change with time
  
# 2.1 Hierarchical Clustering

- Clustering is used to better understand the data, instead of looking at variables seperately

- One can visualize clustering by plotting each row on an N-dimensional plane. Those rows that are similar will be closer together on the N-plane

- The Euclidean Distance applies in N-dimensions, where the formula is generalized across all pairwise variables between two rows

- A lower-triangular matrix providing the difference in Euclidean distances between each row may be calculated to view the proximity between rows.

- By using trees, called a Dendrfogram, visually, one may identify clusters as follows

-   1. Find the pairwise diferences in distances between points (call them here dis-diffs)
    2. Order the dis-diffs in ascending order
    3. Create the canvas of the tree, where the vertical axis is the space of dis-difs and the horizontal axis is the space of data
    4. Those points closest to eachother per the dis-difs form a cluster
    5. We may then generalize this procedure on the clusters themselves, to form a new cluster, should that be the requirement
    6. Determine the distance between clusters using one of the methodologies
      i) Single Linkage: The minimum distance between clusters, as determined by the points within
      ii) Complete Linkage: The maximum distance between clusters, as determined by the points within
      iii) Average Linkage: Average all pairwise distances between points in different clusters
      iv) Centroid Method: Average the points within each cluster (therefore determining the centroid) before calculating distance
      v) Ward's Method: A distance such that the combined cluster would minimize the within-variance between each centroid

- The final number of clusxters depends on the restrictions we place on the number, or maximum distances

- The lower the maximum distance, the more clusters there will be
   
- The most difficult part of clustering and unsupervised learning, is measuring the performance of the clusters, as there is no output or dependent variable to perform that testing.

# 2.2 Cophenetic Correlation

- Depending on the measure of distance selected as described above, different sets of clusters may be calculated.

- One problem wiht unsupervised learning is that we don't know if one dendrogram is better than another; we don't have a measure of success

- Different Dendrograms mayh be compared using the Cophenetic Correlation.

- This is the correlation between the base Euclean differences between two rows, and another set of distances according to the Dendrogram
  - Let the rows be X and Y, and construct clusters according to a selected distance methodology
  - See what distance would result in the clusters containing X and Y to form a new single cluster containing X and Y
  - Reiterate this process for all points in the data set
  - Calculate the correlation between the base set of Euclidean distances, and the Dendrogram distances described above
  - This correlation is the Cophenetic Correlation
 
- The higher the correlation, the more "faithful" the dendrogram is to the data (or something)

# 2.3 Hierarchical Clustering Hands-on

Coding exercise. Skip

# 2.4 Introduction to Dimensionality Reduction

- Dimensionality reduction is useful when there are a large number of columns or independent variables

- Calibrating on multiple columns may lead to overfitting, where irrelevant columns are used, just be chance in their signal

- Reducing dimensionality has a number of benefits including
    - Removes multi-collinearity to improve ML model performance
    - Helps reduce over fitting
    - Decreases computational times for fitting models
    - Makes visualization easier
    - Decreases storage requirements
    - Avoids curse of dimensionality, leading to exponential increase in computational times
 
  - There are two methods of dimensionality reduction
  -   (1) Feature Elimination: Remove variables that are not important, losing the any insight from those columns
  -   (2) Feature Extraction: Create a few new variables from the old variables. PCA is the most popular feature extraction technique. Another popular technique is the t-distributed stochastic neighbor embedding (t-SNE), which is a non-linear method

# 2.5 Principal Component Analysis (PCA) - Part 1



