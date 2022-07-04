## Manfred - 03 - Graph Data - Community Detection 
- What are communities
- Newman Girvan algorithm
- Modularity
- Node clustering with probabilistic mixture model
  
First of all what is a **community**?
A community in the graph context a part of the graph which is more **closely tied together internally** than they are with the rest of the graph. So communities are essentially a part of the network that **interacts more frequently** with each other.

In this context it is also important to know about **modularity**. **Modularity** is essentially a measure of how well the graph is connected, measuring the density of the connections withing a community. A high modularity score will have many connections within the community, but only a few connections outside the community.
Communities can have many different names and structure depending on the context. Sometimes called clusters, cohesive subgroups or modules. 
The different types of communities are:
- coherent subgroups, when we identify a single cluster.
- Graph clustering, when we split the graph into disjoint clusters.
- overlapping communities, when the communities overlap with each other.
- fuzzy clustering, when there are different degrees of membership in the communities.

The **Newman Girvan algorithm** is a method for detecting communities in a graph.
The idea behind the algorithm is in essence very simple and be described in simple steps. 
It is important to understand betweeness centrality, this is a measure of how often a node is connected to another node, and is central part of the algorithm.
1. For every node in the graph we calculate the betweeness centrality.
2. Then we remove the edge with the highest betweeness centrality.
3. Then we calculate the betweeness centrality for every remaining edge.
4. We then repeat until the graph is empty.
We now a hierarchy of the different communities in the graph.
To evaluate which of these communities are the most connected to each other we can use the modularity.

A **probabilistic mixture model** is a soft-clustering method that is used when we want a model to account for multiple different distributions. The probabilistic mixture model is constructed using mixture components that each represents a distribution in the mixture model. The gaussian mixture model is a mixture model that is constructed using gaussian distributions as mixture components.  
**Gaussian Mixture Models**. A gaussian mixture model is essentially used when we want a model to account for multiple different distributions. The mixture model is constructed using mixture components that each represents a distribution in the mixture model. A gaussian mixture model is a mixture model that is constructed using gaussian distributions as mixture components. When applying Gaussian Mixture Models, in can be done using the **Expectation Maximization algorithm**. Using this algorithm, we start with a random guess for what the clusters are going to be, and then proceed to improve iteratively by alternating two steps:
1. ***Expectation***: Assign each datapoint to a cluster probabilistically, meaning, the distance to the clusters.
2. ***Maximization***: Update the parameters for the clusters (weighted mean location and variance-covariance matrix) based on the points in the cluster (weighted by their probability assigned in the first set)

In the first task we use the Girvan-Newman algorthm to find the communities in a network.Here we see the modularity scores for the communites defineed by the Girvan-Newman algorithm:

k = 2: 0.0049
k = 3: 0.0049
k = 4: 0.071
k = 5: 0.073

They are all pretty bad. Which is shownn by computing the modularity score from the predined attributes, where we see that status and office have the highest score of 
Status          | k = 2: 0.255
Office          | k = 3: 0.197

We can also see that they suggest 2 and 3 communites, whereas the Girvan-Newman algorithm found 5. In task 2 we calculate the **log-likelihood** based on a **Gaussian mixture model**. 