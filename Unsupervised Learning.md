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
