# Manfred - 04 - Graph Clustering
<font size="1">
This lecture started on a segment of the course that is dedicated to machine learning with graph and network data. In this lecture the focus was on a form of unsupervised learning for graphs; community detecting, a.k.a. graph clustering.

## Communities

Informally, a community in a network is a group of nodes with greater ties internally than to the rest of the network.

The actors in a network tend to form groups of closely-knit connections. The groups are also called communities, clusters, cohesive subgroups or modules in different context. Roughly speaking, individuals interacting more frequently within a group that between groups.

![](../attachments/Clipboard_2022-06-03-13-15-57.png)

## Graph Clustering

When performing network clustering, it is the task of extracting the natural community structure from networks of vertices and edges.

### Terminology and Notation

A cluster of $G=(V,E)$ is a partitioning of $C=\{ C_1, \dots, C_k \}$ of $V$

### Method selection

Pick a quality measure for clustering

Find an algorithm to (approximately) determine the clustering with optimal quality.

## Edge Betweenness

One such measure, is edge betweenness.

Shortest path betweenness: We find the shortest path between all pairs of vertices and count how many run along each ege. Calculated as:

$$\beta(e)=\sum_{u,v\in V} \frac{\text{Number of shortest path connection u, v going through e}}{\text{Number of shortest paths connection u,v}}$$

Defined as: Number of shortest path passing the edge.

In order to find the shortest path between a particular pair of vertices, breadth-first search can be used, but a more efficient way is by using methods proposed by Newman and Brades, where Newman is implemented in the work presented. But this are outside the scope of this topic.

The idea is to find the shortest path between all vertices in the graph, in order to locate edges used a lot, which can be concluded to be paths between clusters. 

The shortest path betweenness is however just one kind of betweenneess, and the one used in the slides. In the paper they discuss multiple ways. Another way is the random walk betweenness, where signals travel random about the network until they reach their destination. The expected net number of time a random walk between a particular of vertices will pass down a particular edge and sum over all vertex paris. 

Lastly where a unit resistance is placed on each edge of the network and unit current source and sink at a particular pair of vertices. The resulting current flow in the network will travel from source to sink along a multitude of paths, those with least resistance carrying the greatest fraction of the current. the current-flow betweenness for and edge is defined to be the absolute value of the current along the edge summed over all source/sink paris.

One thing to note is that the last two are probably outside the scope of this presentation, as only the first way was introduced in the lecture.

## Newman, Girvan Algorithm

Newman-Girvan Algorithm produces a hierarchy of $n$ clustering.

Attributes of the algorithm:
- Iterative removal of edges from the network to split it into communities. The edges removed are being identified using betweenneess measures.
- These are recalculated of the betweenness score after reach removal.

It differs from other work as it does not remove edges between vertex pairs with the lowest similarity, but on finding edges with the highest betweenness, where betweenness is some measure that favors edges that lie between communities and disfavors those that lie inside communities. Betweenness is based on the idea tha if two communities are joined by only a few intercommunitiy edges, then all paths through the network from vertices in one community to vertices in the other must pass along on of those few edges. Given a suitable set of paths, one can count ho many go along each ege in the graph and this number we then expect to be largest for the intercommunity edges, thus providing a method for identifying them.
Another way the method differs is in the inclusion of a recalculation step. If a standard divisive clustering was performed based on edge betweenness, the betweenness for all edges in the network and the n removed edges in decreasing order of betweenness. The issue here is that once the first edge is removed, the betweenness values for the remaining edges will no longer reflect the network as it is now. This can give rise to unwanted behaviors. If two communities are joined by two edges, but for whatever reason, most paths between the two flow along just one of those edged, then that edge will have a higher betweenness score and the other will not. AN algorithm that calculated betweennsses only once and then removed edges in the betweenness order would remove the first edge early in the course of its operations, but the second might not get removed until much later. Thus the obvious division of the network ino two parts might not be discovered by the algorithm. In the worst case, the two parts themselves might be individually broken up before the division between the two is made. The solution is to recalculate the betweenness score after the removal of each edge. This adds computational effort into the system, but it is deemed worth the cost.

The general form of the algorithm is as follows:
1. Calculate betweenness scores for all edges in the network
1. Find the edge with the highest score and remove it form the network. If two or more edges tie for the highest score, choose one of the mat random.
1. Recalculate betweenness for all remaining edges
1. Repeat from step 1

Another issue is that the algorithm will be used on networks which are not know ahead of time, but how do we then know the found communities are good ones? This is a relevant problem, as this algorithm will always removed edges, even when there are no meaningfully communities in the network. In addition to this, the output is in the form of a dendrogram representing an entire nested hierarchy of possible community divisions for the network. So it is relevant to know which is the best one and where we should cut the dendrogram to get a sensible division of the network.

In order to address this question, a measure of quality is defined, called modularity. This measure is based on previous measure of assortative mixing proposed by Newman. Consider a particular division of a network into $k$ communities. Then define a $k \times k$ symmetric matrix __e__ whose element $e_{ij}$ is the fraction of all edges in the network that link vertices in community $i$ to vertices in community $j$. The trace in this matrix Tr $e = \Sigma_i e_{ii}$ gives the fraction of edges in the network that connect vertices in the same community, and clearly a good division into communities should have a high value of this trace. The trace on its own is however not a good indicator of the quality of the divisions since, for example, placing all vertices in a single community would give the maximal value of Tr $e = 1$ while given no information about community structure at all. So we further define the row (or column) sums $a_i=\Sigma_j e_{ij}$, which represents the fraction of edges tha connect to vertices in community $i$. In a network in which edges fall between vertices without regard for the communities they belong to, we would have $e_{ij}=a_ia_j$. Thus we can define a modularity measure by:

$$Q=\sum_i (e_{ii}-a^2_i) = \text{Tr e}-\| e^2\|$$

Where $\| x \|$ indicates the sum of the elements of the matrix $x$. This quantity measures the fraction of the edges in the network that connects the vertices of the same type (i.e. within community edges) minus the expected value of the same quantity in a network with the same community divisions by random connection between the vertices. If the number of within-community edges i no better than random, we well get $Q=0$. Values approaching $Q=1$, which is the maximum, indicate networks with strong community structure. In practice, values for such networks typically fall in the range from $0.3$ to $0.7$. Higher values are rare. Typically  we will calculate $Q$ for each split of a network into communities as we move down the dendogram, and look for local peaks in its value, which indicate particularly satisfactory splits. Usually there are one or two of such peaks.

__NOTE__: Modularity cannot be optimized directly, as exact solution is NP hard

## Mixture Model for Clustering

## Gaussian Mixture Models

Clustering is an unsupervised learning problem where we intend to find clusters of points in our dataset with similar characteristics. When considering clustering methods, they can be hard (like K-Means) where each point is only assigned to one cluster. There is not uncertainty measure or probability for other clusters the point could belong to. This is something Gaussian Mixture addresses, by representing clusters as Gaussian distributions. Another advantage is that it does not have a bias towards circular clusters, so it works well even with non-linear data distributions.

A Gaussian Mixture is a function comprised of several gaussian's, each identified by $k \in \{1, \dots, K\}$, where $K$ is the number of clusters.Each Gaussian $k$ in the mixture is comprised of the following parameters:

- A mean $\mu$ defining the center
- A covariance $\Sigma$ defining the width

When applying Gaussian Mixture Models, in can be done using Expectation Maximization. Using this algorithm, we start with a random guess for what the clusters are going to be, and then proceed to improve iteratively by alternating two steps:

1. Expectation: Assign each datapoint to a cluster probabilistically, meaning, the distance to the clusters.
1. Maximization: Update the parameters for the clusters (weighted mean location and variance-covariance matrix) based on the points in the cluster (weighted by their probability assigned in the first set)

## Latent Mixture Random Graph Model

A mixture model is a probabilistic model for representing the presence of subpopulations within an overall population.

For Random Graph Models; two-stage sampling procedure for graphs: given number of nodes $n$

__step 1__ for each node $v_i$, sample latent coordinates $z_i \in \mathbb{R}^d$ according to a Gaussian Mixture Model

__step 2__ For each pair of nodes $v_1, v_j$, sample the value of a boolean edge valuable $E_{i,j}$ according to logistic regression model dependent on Euclidean distance between latent coordinates.

The input is a graph with unlabeled nodes and target number of clusters $k$. The task is to determine model parameters and latent coordinates. Nodes are then clustered by applying the Gaussian Mixture Model to the points.

# Modularity
The Modularity Optimization algorithms tries to detect communities in the graph based on their modularity. Modularity is a measure of the structure of a graph, measuring the density of connections within a module or community. Graphs with a high modularity score will have many connections within a community but only few pointing outwards to other communities.

</font>