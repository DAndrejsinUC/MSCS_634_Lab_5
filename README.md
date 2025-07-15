# MSCS_634_Lab_5

## Step 4: Analysis and Insights

### Comparison: Hierarchical vs. DBSCAN Clustering

In this lab, I applied agglomerative hierarchical clustering and DBSCAN to the standardized Wine dataset. Both algorithms produced useful results, but they approached the problem in different ways.

Using hierarchical clustering, I tested different values for `n_clusters` and analyzed the dendrogram. The largest vertical jump in the dendrogram occurred when going from three to two clusters, suggesting that three clusters best captured the natural groupings in the data. This outcome aligns with the fact that the dataset contains three known wine cultivars. The PCA scatter plot confirmed that the three clusters were relatively well separated.

DBSCAN worked differently. Instead of requiring a specific number of clusters, it formed clusters based on data density using two parameters: `eps` (radius of neighborhood) and `min_samples` (minimum number of points in a neighborhood). I ran 84 combinations of these parameters. The best configuration was `eps = 2.4` and `min_samples = 3`, which resulted in two clusters and several noise points. This means DBSCAN identified two dense groupings but considered the third wine class too sparse to be a proper cluster under those settings.

A key takeaway here is that hierarchical clustering gave me a solution that captured all three wine types, while DBSCAN focused on density and excluded less compact groups. This highlights how different clustering algorithms can lead to different interpretations of the same data.

### Influence of Parameters

In hierarchical clustering, the outcome depended entirely on the `n_clusters` value I chose. The dendrogram helped me decide where to cut the hierarchy for the most meaningful result.

In DBSCAN, the clustering results were very sensitive to the `eps` and `min_samples` values:
- A smaller `eps` created many noise points and sometimes no clusters at all.
- A larger `eps` merged clusters that should have remained separate.
- A high `min_samples` value made it harder to form clusters, especially for sparser regions.

Carefully tuning these parameters was necessary to get useful results.

### Strengths and Weaknesses

| Algorithm        | Strengths                                                   | Weaknesses                                                  |
|------------------|--------------------------------------------------------------|-------------------------------------------------------------|
| Hierarchical     | Easy to visualize; allows control over cluster count         | Requires `n_clusters` input; sensitive to linkage strategy  |
| DBSCAN           | Finds arbitrary shapes; detects noise; no need to set `k`    | Sensitive to `eps`; may miss valid but sparse clusters      |

### Final Thoughts

This lab made it clear that clustering doesn’t have a single correct answer. Hierarchical clustering worked well when the number of clusters was guided by the dendrogram. DBSCAN, meanwhile, found dense regions and excluded scattered points, showing that its strength lies in identifying compact clusters and flagging outliers.
