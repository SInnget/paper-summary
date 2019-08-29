# PointNet

# PointNet ++

PointNet++: Deep Hierarchical Feature Learning on Point Sets in a Metric Space
[paper link](https://arxiv.org/abs/1706.02413)

### Problem formulation
Do segmentation or classification *directly* on point cloud dataset.
Point cloud set $\Chi = (M, d) \subset \R^d$, where $d$ is inherented euclidean distance on $\R^d$.

### Improvement
In the pointnet, the localization(distance) was ignored, and computation cost is high. Here PointNet++ use `sampling`, `grouping`, and `extracting` to find an embedding of all points.

### Ingradients:
#### Sampling
1. given $\{x_1,..,x_N\}\subset \R^d$, reduce to $\{x_{i_1}, ..,x_{i_k}\}$.
2. Use farthest point sampling method to take care with locality.
#### Grouping
1. Input: Point set of size $N\times (d+C)$, and a set of centroids of size $N'\times d$, $N$ total number of points, $N'$ number of centroids/local regions.
2. Output: Grouped points of size $N'\times K \times (d+C)$, each group cooresponding to a local region, and $K$ the number of neighbors of centroid points ($K$ dependes on centroid points).
3. Ball query was applied to find local region points of each centroid, this method respect the distance locality, NOT K-NN.
#### Extracting
1. Apply PointNet to each local points
2. Input: $N'$ local regions of points of size $N' \times K \times (d+C)$.
3. Output: $N' \times (d+C')$.
4. Implementation: The coordinates in a fix local region was translated to local frame w.r.t. centroids, e.g. $\hat{x_i}^j = x_i^j - \bold{centroid}^j$, then apply to point net to find local feature.