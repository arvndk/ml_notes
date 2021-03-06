## Thomas - 06 - Probabilistic Graphical Models (PGMs)
<font size="1">

#### PGM syntax
Let $X_1, \cdots X_n$ b a collection of random variables, A PGM over $X_1, \cdots X_n$ consists of:
- a directed acyclic graph $G = {V,E}$ whose nodes $V$ are the variables $X_1, \cdots X_n$ 
- a set of local conditional distributions $P = {p(X_i|pa(X_i)), X_i \in V}$, where $pa(X_i)$ are the parents of $X_i$ in $G$ as defined by the edges $E$

#### PGM semantics
A PGM $N$ with nodes $X_1, \cdots, X_n$ defines a joint distribution
$$pn(X_1, \cdot , X_n) = \prod_{i=1}^{n} p(X_i | pa(X_i))$$

**Bayes' rule** Bayes' rule illustrates some of the inference we face:
![]("..\attachments/cool.png)

#### Approximate inference: Variational inference

**What is Variational inference?**
The main idea of variational methods is to cast inference as an optimization problem. 

Variational Bayesian methods are a family of techniques for approximating uncontrollable integrals arising in Bayesian inference and machine learning. They are typically used in complex statistical models consisting of observed variables (usually termed "data") as well as unknown parameters and latent variables, with various sorts of relationships among the three types of random variables, as might be described by a graphical model. As typical in Bayesian inference, the parameters and latent variables are grouped together as "unobserved variables". Variational Bayesian methods are primarily used for two purposes:

1. To provide an analytical approximation to the posterior probability of the unobserved variables, in order to do statistical inference over these variables.
2. To derive a lower bound for the marginal likelihood (sometimes called the evidence) of the observed data (i.e. the marginal probability of the data given the model, with marginalization performed over unobserved variables). This is typically used for performing model selection, the general idea being that a higher marginal likelihood for a given model indicates a better fit of the data by that model and hence a greater probability that the model in question was the one that generated the data.

In the former purpose (that of approximating a posterior probability), variational Bayes is an alternative to Monte Carlo sampling methods ??? particularly, Markov chain Monte Carlo methods such as Gibbs sampling ??? for taking a fully Bayesian approach to statistical inference over complex distributions that are difficult to evaluate directly or sample. In particular, whereas Monte Carlo techniques provide a numerical approximation to the exact posterior using a set of samples, variational Bayes provides a locally-optimal, exact analytical solution to an approximation of the posterior. 

VI is deterministic, ie, there is no randomness. VI has easy to gauge convergence. 

The main differences between sampling and variational techniques are that:
- Unlike sampling-based methods, variational approaches will almost never find the globally optimal solution.
- However, we will always know if they have converged. In some cases, we will even have bounds on their accuracy.
- In practice, variational inference methods often scale better and are more amenable to techniques like stochastic gradient optimization, parallelization over multiple processors, and acceleration using GPUs.

Approximate the true posterior distribution $p(z|x)$ with a variational distribution belonging to a tractable family of disruptions.

**The KL-divergence (Kullback-Leibler divergence)**

To formulate inference as an optimization problem, we need to choose an approximating family $Q$ and an optimization objective $J(q)$. This objective needs to capture the similarity between $q$ and $p$; the field of information theory provides us with a tool for this called the Kullback-Leibler (KL) divergence.

 $$KL(f \| g) = \int_Z f(Z) log(\frac{f(Z)}{g(Z)}) dz = \mathbb{E}_f 0[ log (\frac{f(Z)}{g(z)})]$$

 **Assumptions about variational distribution**
 We will often use the mean field, which states that $Q$ consists of all distributions that factorizes according to the equation:
 $$q(z)=\prod_i q_i(z_i)$$

**ELBO**
Maximizing the ELBO is equivalent to minimizing the
KL divergence.
The ELBO is the evidence lower bound.
ELBO consist of two terms the reconstruction term and the penalty term.

 **Bayesian learning using variational inference**
 - We posit a model $p(y|\theta)$, and want to learn $\theta$ from a data set $D={y_1,\cdots, y_N}$
 - We cast the problem in a Baysian setting by including a prior $p(\theta)$
 - We seek the posterior $p(\theta | D)$, which is approximated by
$$\hat{q}(\theta)=arg \underset{q \in Q}{\operatorname{min}} KL (q(\theta)\| p(\theta|D))$$
- This is identical to maximizing $L(q)$- a lower bound of $p(D)$

#### Black Box Variational Inference
Variational inference transforms the problem of approximating a conditional distribution into an optimization
problem.

Maximizing the ELBO is equivalent to minimizing the
KL divergence.

In black box variation they instead use stochastic optimization to maximize
the ELBO. In stochastic optimization, we maximize a
function using noisy estimates of its gradient

- The goal is to obtain efficient inference in
unconstrained Bayesian network models ??? any structure, any
combination of distributional families

- Black-Box Variational Inference promises VB inference in any
model, but at the cost that inference relies on sampling ??? and it
sometimes shows poor converge properties in practice.
</font>