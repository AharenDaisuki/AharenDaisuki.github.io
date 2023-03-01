---
title: 'Metropolis Hastings Algorithm - Motivation and Implementation'
date: 2023-03-01
permalink: /posts/2023/03/MetropolisHastings/
tags:
- Markov Chain Monte Carlo
- Metropolis Hastings Sampler
- Stochastic Process
- Machine Learning
---

Motivation
------
Basically why Metropolis-Hastings? It's not always trivial to compute the integral of a specific function h(x) when h(x) is rather complex.

$ \int h(x) dx $

However, it is plain to see that we can always let h(x) = p(x) * f(x).

$ E_{p_x}(f(x)) = \int p_x(x) f(x) dx $

This is essentially equivalent to derive the expectation of f(x) on pdf p(x). In traditional way, sampling methods are adopted in order to approximate the expectation of f(x).

\[ E_{p_x}(f(x)) =  \lim_{n \to \infty} (\sum_{i = 1}^{n} f(x_i)) / n \]

Another issue is that we need to guarantee that samples are selected from a steady distribution with pdf p(x). And this is when Metropolis Hastings algorithm comes into play.

Proofs of Correctness
------

$ \textbf{Definition} $

DTMC ${X_n}$ with transition matrix $P$ is siad to satisfy the $ \textbf{detailed balance condition} $ with respect to the probability distribution $\pi$ satisfying $\pi_{i}>0, \forall i,$ if
\[ \pi_{i}p_{ij} = \pi_{j}p_{ji}, \forall i \in S, j \in S \]

$ \textbf{Theorem} $

If the $ \textbf{detailed balance condition} $ holds for $P$ and $\pi$, then $\pi$ is a stationary distribution for $P$,
i.e., the balancing equation $\pi = \pi P$ holds. (easy to prove by taking sum over j  for the detail balance condition)

Intuitively, it's critical to guarantee a DTMC satisfying the detailed balance condition (reversibility) in MCMC-based method, but the detailed balance condition may not hold for most of the cases.

In order to make sure the detailed balance condition hold, accept rate matrix $\alpha$ is introduced, such that
\[ \pi_{i} p_{ij} \alpha(i | j) = \pi_{j}p_{ji} \alpha(j | i) \]

And this is the key idea of Metropolis Algorithm. A plain-to-see improvement is to normalize the accept ratio to 1 on one side of the equation.
if $ \alpha(i | j) < \alpha(j | i) $:
\[ \pi_{i} p_{ij} \frac{\alpha(i | j)}{\alpha(j | i)} = \pi_{j}p_{ji} \]
else if $ \alpha(i | j) \geq \alpha(j | i) $:
\[ \pi_{i} p_{ij} = \pi_{j}p_{ji} \frac{\alpha(j | i)}{\alpha(i | j)} \]

To simplify this, we define $ \alpha(i | j) = \min(1, \frac{\pi_{j}p_{ji}}{\pi_{i} p_{ij}})$.
By now, we should somehow understand the guts of Metropolis Hastings Algorithm.

Pseudo-code
------

Given current state $X_{n} = i$
  * 1 rollout state j from the proposal distribution with probability $p_{ij}$
  * 2 accept $X_{n+1} = j$ with probability $ \alpha(i | j) = 1 ^ \frac{\pi_{j}p_{ji}}{\pi_{i} p_{ij}} $
  * 3 otherwise, X_{n+1} = i















