<!-- TOPICS -->
- Node embeddings: shallow and functional
- Message passing updates
- Elements of GNN architectures (Skip connections, attention)
- GNNs for node classification, graph classification and link prediction


**Graph Neural Networks** is the application of neural networks to the graph data structure. The key ideas the GNN's revolve around is the idea of representing the nodes as vector embeddings for a concise and powerful representation. The edges, however, are used:
 - In GNNs where they denote the structure of the graph. They specify which 2 nodes have links between them and the weight of such edge if the edges are weighted.
-  In the message passing algorithm also known as the Graph Convolutional Networks (GCN)
<!-- TODO more clarify on edges usage - links of message passing and GCN -->

There are two method to represent the nodes as vector embeddings:
**Shallow embeddings** where you take all the nodes give them an id, an then assign them initially a vector embedding i specified dimensionality, and then you optimize exclusively this embedding, disregarding other structural information. 
<!-- A way to learn/optimize the first randomly intiazlied shallow embeddings is through the reconstruction loss. In the reconstruction loss we aim to reconstruct the adjacency matrix, with for example squared error loss.
A limitation of the shallow embedding is that they are inherently transductive, the embeddings depends on the specific training graph, and new nodes would not have id's/interpretation in that setting. -->

**Functional Embedding**: Here we learn a function that can map the nodes in a graph to the vector embeddings, and then we optimize this function.
<!-- 
- We can use for Link prediction or Node Classification.
- Given: one or several graphs
- Learn a function $f: (V,E,A_t,Y), i \in V \rightarrow \textbf{z}_i $ maps nodes in a graph to a vector embedding.
- Optimization in the space of parameters (weights) W defining the function.
- Minimize a task specific loss function (node/edge/graph classification error)
- Examples: graph kernels, GNNs
- works in inductive setting, hence also for transductive setting. -->

**Message passing** is the idea that each node has neighbours and then these neighbours pass their embedding to the node, and the node performs some aggregation of these embeddings, hence its own embedding will depend on its neighbours, that is the graph structure.

Some of the use cases of GNNs. We consider three overall categories of use cases:
1. **Node Classification**: 
    <!-- - The goal here is to classify nodes represented through their embedding vector in classes
    - Is a user in a social network going to vote democrat or republican?
    - Is a sensor in a sensor network going to fail within the next 30 days?
    - Has a computer in a computer network been hacked? -->
2. **Link Prediction**
    <!-- - The goal here is to predict the links between nodes represented through their embedding vector. It could be whether a certain edge exists between two nodes or not, or it could be classifying the type of edge between two nodes.
    - Are two proteins interacting?
    - Is there a ???capital of??? relation between Sacramento and California?
    - Is user A going to become a follower of user B? -->
3. **Network classification**
    <!-- - Here the goal is to classify the entire graph.
    - Is a molecule a mutagen?
    - Is molecule a drug for a disease? -->

<!-- In Node Classification we consider the distinction between between the transductive and inductive setting.

**Transductive Node Classification Setting**
- The graph here is fixed, that is cannot be changed/extended during inference. So we **know** already all existing vertices, so we can rely on havin a fixed set of nodes (this is a limitation of the transductive setting).
- ??? all nodes Vu that need to be classified already known when learning the classifier
- "Transfer" learning from one part of the graph to another part of the graph.

**Inductive Node Classification Setting**
- Here a Graph $G = ((V_l, V_u), E, A, Y)$ is used for training (possibly V_u = ???).
- Nodes that are classified can be new nodes, which are added to $G$, or even nodes in a different graph $G'$
- Hence it has much more flexibility -->


<!-- NOTEBOOKS -->

For the first task we observe the effects of changing the epochs, the results show that more is better and we are at 100% accuracy at 60 epochs consistently. A larger number of hidden dimensions also seems to improve the accuracy.

For the next task we create a new graph as can be seen below, we than mark each nodes that a two or less links away from the originals marked nodes.

We train the models on this new graph and see that the accuracy for the train set 1.0 and 0.99 for the test set.
Initialy this seems to be simple task, but To show that the model is inherently transductive we will generate new dataset, where we move the two  nodes.

This results in a much worse performance from the previose experiment, but we can see that the model is still transductive.