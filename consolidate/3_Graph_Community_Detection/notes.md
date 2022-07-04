**TOPICS**
- What are communities
- Newman Girvan algorithm
- Modularity
- Node clustering with probabilistic mixture model

**THEORY**
A community in the graph context a part of the graph which is more closely tied together internally than they are with the rest of the graph. So **communities** are parts in the network that interact more frequently with each other. The closer a community is connected the more similar to each other node in the community is, this is called homophile.

To define a community, we need **Modularity** term which measures how well the graph is connected by calculating the density of the connetions within a community. Modularity score is between 0 and 1, high modularity score indicates a network with strong community structure.
There are two type of method:
    1. Hard clustering were each node is either in a community or not in the community.
    2. Soft clustering where there can be overlap between the communities.

**Newman Girvan algorithm** is a hard-clustering method which finds the communities in a network by:
- Calculating the edge betweeness score for each edge in the network. The edge betweenness is the amount of shortest paths passing through the edge. 
- Finds the one with the highest score and removes it. If there is a tie, one is choosen at random. 
- The edge betweenness is recalculated and the steps are repeated. This is repeated until the network is empty. This can then be used to select the best community's using the modularity score.


A **probabilistic mixture model** is a soft-clustering method that is used when we want a model to account for multiple different distributions. The probabilistic mixture model is constructed using mixture components that each represents a distribution in the mixture model. The gaussian mixture model is a mixture model that is constructed using gaussian distributions as mixture components.  
When applying Gaussian Mixture Model, in can be done using the **Expectation Maximization algorithm**. Using this algorithm, we start with a random guess for what the clusters are going to be, and then proceed to improve iteratively by alternating two steps:
    1. Expectation: Assign each datapoint to a cluster probabilistically, that is, the distance to the clusters.
    2. Maximization: Update the parameters for the clusters (weighted mean location and variance-covariance matrix) based on the points in the cluster (weighted by their probability assigned in the first set)

Notebook 4
In the first task we use the Girvan-Newman algorthm to find the communities in a network.Here we see the modularity scores for the communites defineed by the Girvan-Newman algorithm 
k = 2: 0.0049
k = 3: 0.0049
k = 4: 0.071
k = 5: 0.073

They are all pretty bad. Which is shownn by computing the modularity score from the predined attributes, where we see that status and office have the highest score of 
Status          | k = 2: 0.255
Office          | k = 3: 0.197


We can also see that they suggest 2 and 3 communites, whereas the Girvan-Newman algorithm found 5.

In task 2 we calculate the **log-likelihood** based on a **Gaussian mixture model**. 
