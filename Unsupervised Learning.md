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

- There are two types of clustering (i) Connectivity based clustering (ii) Centroid based clustering
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

   
