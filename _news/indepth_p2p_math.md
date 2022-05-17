---
layout: page
title: Risk Sharing Principles
description: Some math results
img: /assets/img/math_colab_r.png
importance: 1
category: P2P
---

In our [paper](https://arxiv.org/abs/2107.02764), we first explore the stochastic oderings of linear risk sharing before moving on the some fun simulations. The idea of this post is to give a general overview that motivates our choices in the simulation steps. 


Here some of the most important results are summarised (this post being a summary of a summary skips a few steps - for details see our article). Further, the blog only contains the propositions and lemmas but skip the proofs.


The main results are below:

Given some random loss $$X$$ and an insurance scheme offering indemnity $$x \rightarrow I(x)$$ against a premium $$p$$, an agent will purchase the insurance if $$\xi \preceq_{CX}$$ for the convex order where $$\xi = X + \pi - I(X)$$, where $$\pi$$ is the associate premium to transfer that risk. 

#### Def.: Convex Order

Consider two variables $$X$$ and $$Y$$ such that $$\mathbb{E}[g(X)]\leq \mathbb{E}[g(Y)]$$ for all convex functions $$g:\mathbb{R}\rightarrow \mathbb{R},$$
(provided the expectations exist). Then $$X$$ is said to be smaller than $$Y$$ in the convex order, and is denoted as $$X\preceq_{CX}Y$$.

#### Proposition:  
If $$X\preceq_{CX}Y$$, then $$\mathbb{E}[X] =\mathbb{E}[Y]$$ and $$\text{Var}[X] \leq\text{Var}[Y]$$.

This motivates the use of the variance in the simulations later on. 


#### Def. Risk sharing scheme
Consider two random vectors $$\boldsymbol{\xi}=(\xi_1,\cdots,\xi_n)$$ and  $$\boldsymbol{X}=(X_1,\cdots,X_n)$$ on $$\mathbb{R}_+^n$$. Then $$\boldsymbol{\xi}$$ is a risk-sharing scheme of $$\boldsymbol{X}$$ if $$X_1+\cdots+X_n=\xi_1+\cdots+\xi_n$$ almost surely.

For example, the average is a risk sharing principle: $$\xi_i=\overline{X}=\displaystyle{\frac{1}{n}\sum_{j=1}^n}X_j$$, for any $$i$$. A weighted average, based on credibility principles, too: $$\xi_i=\alpha X_i+[1-\alpha]\overline{X}$$, where $$\alpha\in[0,1]$$ (we will get back on those averages in the next section). Observe also that the order statistics defines a risk sharing mechanism: $$\xi_i=X_{(i)}$$ where $$X_{(1)}\leq X_{(2)}\leq \cdots \leq X_{(n)}$$. Given a permutation $$\sigma$$ of $$\{1,2,\cdots,n\}$$, $$\xi_i=X_{\sigma(i)}$$ defines a risk sharing (that we we write, using vector notations, $$\boldsymbol{\xi}=P_{\sigma}\boldsymbol{X}$$, where $$P_{\sigma}$$ is the permutation matrix associated with $$\sigma$$). This example of permutations is actually very important in the economic literature. 

Which then leads to the proposition

#### Proposition:
Consider two linear risk sharing schemes $$\boldsymbol{\xi}_1$$ and $$\boldsymbol{\xi}_2$$ of $$\boldsymbol{X}$$, such that $$\boldsymbol{\xi}_2=D\boldsymbol{\xi}_1$$, for some doubly-stochastic matrix. Then
$$\operatorname{trace}\big[\operatorname{Var}[\boldsymbol{\xi}_2]\big]\leq\operatorname{trace}\big[\operatorname{Var}[\boldsymbol{\xi}_1]\big]$$.


Finally some extensions to work with cliques. This is important as it shows that for networks that are most often encountered in real life, we will need to settle for an approximation because the optimal solution will be NP-complete.

#### Def. Clique
A clique $$\mathcal{C}_i$$ within an undirected graph $$\mathcal{G} = (\mathcal{V}, \mathcal{E})$$ is a subset of vertices $$\mathcal{C}_i \subseteq \mathcal{V}$$ such that every two distinct vertices are adjacent. That is, the induced subgraph of $$\mathcal{G}$$ by $$\mathcal{C}_i$$ is complete. A _clique cover_ is a partition of the graph $$\mathcal{G}$$ into a set of cliques. 



Now we can start to work on the cliques:
In a network, a clique is a subset of nodes such that every two distinct vertices in the clique are adjacent. Assume that a network with $n$ nodes has two (distinct) cliques, with respectively $$k$$ and $$m$$ nodes. One can consider some ex-post contributions, to cover for losses claimed by connected policyholders. If risks are homogeneous, contributions are equal, within a clique. Assume that policyholders face random losses $$\boldsymbol{X}=(X_1,\cdots,X_k,X_{k+1},\cdots,X_{k+m})$$ and consider the following risk sharing
\begin{equation}
\xi_i = \begin{cases}
\displaystyle{\frac{1}{k}\sum_{j=1}^k X_j}\text{ if }i\in\{1,2,\cdots,k\}\quad\\
\displaystyle{\frac{1}{m}\sum_{j=k+1}^{k+m} X_j}\text{ if }i\in\{k+1,k+2,\cdots,k+m\}
\end{cases}
\end{equation}

In order to illustrate the proposition above, let $I$ denote a uniform variable over $$\{1,2,\cdots,n\}$$, and $$\xi'=\xi_I$$,
\begin{equation}
\mathbb{E}[\xi']=\mathbb{E}[\mathbb{E}[\xi_I|I]]=\frac{1}{n}\sum_{i=1}^n \mathbb{E}[\xi_i]=\frac{1}{n}\sum_{i=1}^n\mathbb{E}[X_i]=\mathbb{E}[X]
\end{equation}
as expected since it is a risk sharing, while
\begin{equation}
\text{Var}[\xi']=\mathbb{E}[\text{Var}[\xi_I|I]]=\frac{1}{n}\sum_{i=1}^n \text{Var}[\xi_i]=\frac{1}{n}\left(k\frac{\text{Var}[X]}{k^2}+m\frac{\text{Var}[X]}{m^2}\right)\\newline=\frac{\text{Var}[X]}{n}\left(\frac{1}{k}+\frac{1}{m}\right)=\frac{\text{Var}[X]}{k(n-k)}
\end{equation}
since $$n=k+m$$, so that $$\text{Var}[\xi']<\text{Var}[X]$$, meaning that if we randomly pick a policyholder, the variance of the loss while risk sharing is lower than the variance of the loss without risk sharing. Observe further that $$k\mapsto k(n-k)$$ is maximal when $$k=\lfloor n/2 \rfloor$$, which means that risk sharing benefit is maximal (socially maximal, for a randomly chosen representative policyholder) when the two cliques have the same size.

#### Cliques in practice

What does that imply for any practical solution though?

Cliques have attractive properties, in that they allow to use a linear risk sharing mechanism on the resulting subgraphs. Further, they can be used to represent a (more) homogeneous subgroup within a larger network, as for example Feng & Taylor propose (in their case, they partition the network based on a hierarchical structure). As we depart from the idea of a complete graph to begin with, partitioning the graph into cliques becomes a _clique problem_. Given a number of cliques $$j$$, the number of nodes $$n$$ and the number of members of clique $$i$$ $$n_i$$ (where $$n_j=n-\sum_{i=1}^{j-1}n_i$$), the variance is always minimized as:
\begin{equation}
\frac{\partial\text{Var}[\xi']}{\partial n_k}=\frac{1}{n_j^2} - \frac{1}{n_k^2} = 0
\end{equation}
implying $$n_i=\tilde{n} \forall i$$ and $$\tilde{n}=\frac{n}{j}$$. This in turn means that:
\begin{equation}
\text{Var}[\xi']=\text{Var}[X]\left(\frac{1}{n}\frac{j}{\frac{n}{j}}\right)=\text{Var}[X]\left(\frac{j}{n}\right)^2
\end{equation}
So the variance decrease is increasing in $$n$$ as in standard partitioning problems, but decreasing in $$j$$ up to the extreme case where $$j=n$$ (ie. every node is its own clique). Even when abstracting from the fact that the set of all cliques $$\mathcal{C}$$ in graph $$\mathcal{G}$$ might not contain ideally sized cliques, the problem of finding a clique cover that minimizes $$j$$ becomes a _minimal clique problem_ and this was shown to be NP-complete by Karp in 1972. Hence and optimal solution will be difficult if not practically impossible to find. One idea to circumvent this is to apply approximate clustering algorithms and reconnect cliques from there



