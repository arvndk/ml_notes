- Inductive and transductive classification
- Homophily
- Independent classification
- Label propagation
- Node classification with Markov networks

To explain node classification in graph data, we need to differentiate **inductive and transductive classification**.  
 - **Inductive** is commonly known as traditional supervised learning where we train a machine learning model on a labelled training dataset, then the model is used to predict the labels of a testing dataset, which have not been seen before. The graphs used for training can be different.
 - **Transductive** differs because here all the data, both the train and test data is observed beforehand. Even when the labels of the test is not known, it can still be used to find patterns during training. The graph is fixed, if changes occur the algorithm has to be rerun.
 --> So in the inductive classification, we try to create a more generic model. While with the transductive classification, it is more specific and will only work for the specific data used in the training.

Another term is **Homophily**, which is when a link between individuals (such as friendship or other social connection) is correlated with those individuals being similar in nature. For example, friends often tend to be similar in characteristics like age, social background and education level. This is very often seen in real data, when closely linked individuals are similar in nature. This also the case when looking at communities in graphs the more densely connected a community the more similar they are. For example, friends often tend to be similar in characteristics like age, social background and education level

<!--TODO Independent classification -->

One example of transductive classification is **Label Propagation** Algorithm (LPA) which is a semi-supervised iterative algorithm to predict labels to unlabelled points by propagating labels through the dataset. It has some characteristics:
    - No node features
    - Transduction classification exploiting homophily
    - For unlabeled nodes compute probability distribution over class labels

Within community networks, the label propagation algorithm aims the change the label of each node based on the communities label. The biggest advantage for label propagation is it excellent runtime.

Label propagation works on the relatively simple assumption that closely connected nodes also have the same label so it is possible to propagate the label to unlabeled nodes in the network.

The algorithm works by performing a random walk foreach of the unlabeled nodes. This is done to determine the probability distribution of reaching a node with a label.
This is then done multiple times until the probabilities stop changing in the unlabeled nodes. Unlabeled nodes are then assigned a label based on the probability distribution.

**Markov Networks** works on undirected models. It is good for mutal non-casual dependencies.<!--TODO add more detail -->


<!-- Notebooks -->
For the task we were asked to write the gibbs sampling function.

## Gibbs Sampling
But first ill quickly explain what gibbs sampling is
Problem: compute a marginal probability $P_N(X=x)$.

(approximate) solution: generate a sequence of samples: $X_1,X_2, \cdots X_N$
So that the frequencies in the sample (approximate) match the marginal probability.

The idea behind Gibbs sampling is to obtain new samples from previous sample by randomly changing the value of the only one selected variable.

From the results in the self study 
- We can see that the standard divination. is low over 5 runs of gibbs sampling so seems decently stable,
- we see that the accuracy as a function of the number of steps swings quite a bit in [.65,.80], and that more steps doesn't really add much

Next, In self study 5 we used Markov Networks on a dataset of lawyers. We use the friendship attribute as edges.

We also use Gibbs sampling, which approximate a solution by generating a sequence of samples so that the frequencies in the sample approximately correspond to the distribtuion