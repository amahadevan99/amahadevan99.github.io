---
title: "Random matrices and response functions"
date: 2024-06-28
---

<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>

Here we will exploit the correspondence between the response function of a dynamical system and the resolvent of a matrix in order to calculate the spectral densities of two famous random matrix ensembles. The results of these calculations are the same as in [these notes](https://amahadevan99.github.io/files/marchenko_pastur.pdf) (which also contain a summary of why we care about the resolvent at all) but the means are different (and perhaps more intuitive, at least from a physics perspective). The central correspondence is that _the resolvent of a matrix_ $$M$$ _is the same as a Laplace transform of the response function of a dynamical system_ $$\dot x_i = \sum_j M_{ij} x_j$$. This explains why resolvents are referred to as Greens functions sometimes: the Greens function of a differential equation is exactly its response function. Here we will use the dynamic cavity method to calculate the response function of dynamical matrices from a desired random matrix ensemble, and therefore find the corresponding spectral density.

### Resolvents
Referring [here](https://amahadevan99.github.io/files/marchenko_pastur.pdf) for more details, we recall that for and $$N\times N$$ matrix $$A$$, if we know its resolvent, defined as

$$ g(z) = \frac{1}{N}{\rm E}\left[{\rm Tr} \frac{1}{z-A}\right],$$

then (if $$A$$ is from an ensemble with real eigenvalues) the spectral density (the probability distribution of eigenvalues) of the ensemble from which $$A$$ is drawn is given by

$$ \rho(x) = \lim_{\epsilon\to 0^+} \frac{1}{\pi}\operatorname{Im} g(x-i\epsilon).$$

### Response functions
We also recall that _response functions_ capture how a function of interest changes when an external field is applied at a prior time. For stationary processes the response function depends only on a _time difference_ and if we have a process $$x(t) = f(x,t) + h(t)$$ for external field $$h(t)$$, then the response function $$\chi(\tau)$$ for time difference $$\tau$$ comes in as

$$ \delta x(t) = \int_0^\infty \chi(\tau)h(t-\tau) d\tau,$$

where $$\delta x(t)$$ is the change in $$x(t)$$ caused by external field $$h(t)$$. Note that the convolution above makes it convenient to work in Laplace (or Fourier) transforms, since convolutions become multiplications.

So how is the response function of $$x_i = \sum_j M_{ij} x_j$$ related to resolvent of $$M$$? If one takes a Laplace transform of the dynamical equation with an external field $$h_i(t)$$ and then solves for the response function, one can immediately see how the resolvent emerges. Recall that the response function can be computed by taking the functional derivative $$\delta x_i(t)/\delta h_i(t-\tau)$$, which in Laplace variables amounts to dividing $$\tilde x_i(z)$$ by $$\tilde h_i(z)$$.


## Gaussian orthogonal ensemble

We will now bring in the random matrices. Imagine that we have a linear dynamical system

$$ \dot{\vec x} = A \vec x  \implies \dot x_i = A_{ij}x_j,$$

where $$A$$ is drawn from the ensemble whose spectral density we wish to compute, and we use Einstein summation convention. Let's take $$A$$ to be from the Gaussian orthogonal ensemble (GOE) which is comprised of symmetric matrix with gaussian entries of variance $$1/N$$ for off-diagonal and $$2/N$$ for diagonal entries. The cavity method consists of asking the question: What happens if we add a new dimension into our vector $$x$$, and concomitantly into our matrix $$A$$? The dynamics of $$x_0$$ will be given by

$$ \dot x_0 = A_{0j}(x_j(t)+\delta x_j(t)) + A_{00}x_0(t),$$

where $$\delta x_j(t)$$ measures the change in the the components of the $$x$$ vector due to the addition of $$x_0$. These in turn are dynamical variables given (according to the definition of the response function) by

$$ \delta x_j(t)  = A_{j0}\int^\infty \chi_j(\tau)x_0(t-\tau)d\tau$$

where the $$j$$ is not summed over in the equation above.
Plugging this into our equation for $$\dot x_0$$, we have

$$ \dot x_0  = A_{0j} x_j + A_{0j}A_{j0}\int^\infty \chi_j(\tau)x_0(t-\tau)d\tau + A_{00}x_0. $$

Using the self-averaging property along with the symmetry of the matrix $$A$$ such that $${\rm E}[A_{j0}A_{0j}]=\frac1N$$, we have

$$ \dot x_0 = A_{0j}x_j + \int^\infty \chi(\tau)x_0(t-\tau)d\tau,$$

where $$\chi(\tau) = \frac1N\sum_j \chi_j(\tau)$$ is the "global" average response, given by the average of "local" response functions.

Defining $$h_0(t) = A_{0j}x_j(t),$$ we now have

$$ \dot x =  h(t) + \int^\infty \chi(\tau)x(t-\tau)d\tau.$$

We have dropped the $$0$$ subscripts, because each component of the vector is statistically identical --- this is a key assumption of the cavity method. We have therefore reduced our many-body problem to a single-body problem, where we need to enforce self consistency, in the sense that the response function of the solution to this equation must be equal to the response function in the equation itself.

More specifically, we move to frequency space via Laplace transform and have

$$ z \tilde x(z) = \tilde h(z) + \tilde \chi(z)\tilde y(z)\implies \tilde x(z) = \frac{\tilde h(z)}{z-\tilde \chi(z)}.$$

Now we impose self consistency: the fact that $$\chi(\tau) = \frac{\delta x(t)}{\delta h(t-\tau)}$$, which in frequency space reads

$$ \tilde\chi(z) = \frac{1}{z-\tilde\chi(z)}.$$

This equation allows us to directly solve for the response function, and we get

$$ \tilde\chi(z) = \frac12\left(z \pm i\sqrt{4-z^2}\right).$$

Note that the imaginary part of this is exactly the resolvent of a GOE matrix, up to a factor of $$\pi$$ as expected. Namely,

$$ \rho(x) = \frac{1}{2\pi}\sqrt{4-x^2}.$$

In other words, as we stated, _the Laplace transform of the response function of the dynamics generated by the matrix is the same as the resolvent of the matrix._


## Wishart-Laguerre ensemble
The same method that we used to find the density of states for the GOE can be used to find the density of states for the ensemble consisting of a gaussian $$N\times T$$ asymmetric matrix multiplied by its transpose. Define the matrix 

$$ W_{ij} = \frac{1}{T}\sum_\mu M_{i\mu}M_{j\mu}$$

where the entries of $$M$$ are i.i.d gaussian with $${\rm E}[M_{i\mu}^2] = 1$$. We will use the convention that Roman indices go from $$1$$ to $$N$$ and Greek indices go from $$1$$ to $$T$$.
Then, as before, consider the dynamical system

$$ \dot x_i = W_{ij}x_j = \frac{1}{T}M_{i\mu}M_{j\mu}x_j.$$

As before, we use Einstein summation convention. Here it will be helpful to define the auxiliary variables $$a_\mu = \sum_j M_{j\mu}x_j$$. Then we can write our dynamical equations as 

$$ \dot x_i = \frac{1}{T} M_{i\mu}a_\mu,\quad \text{and}\quad  a_\mu = M_{j\mu}x_j.$$

Now the cavity method consists of adding a new $$x_0$$ and $$a_0$$ together, which means increasing both $$N$$ and $$T$$ by $$1$$. We then need to introduce two distinct classes of response functions: one for the $$x_i$$, which we will call $$\chi_i(\tau)$$ and one for the $$a_\mu$$ which we will call $$\eta_\mu(\tau)$$.
We then have

$$ \dot x_0 = \frac{1}{T} M_{0\mu}(a_\mu+\delta a_\mu) + \frac 1T M_{00}a_0,\quad  a_0 = M_{j0}(x_j+\delta x_j) + M_{00}x_0.$$

Meanwhile, the perturbations induced in the $$x$$ and $$a$$ variables are

$$ \delta x_j = \frac 1TM_{j0}\int^\infty a_0(t-\tau) \chi_j(\tau)d\tau,\quad \delta a_\mu = M_{0\mu}\int^\infty x_0(t-\tau) \eta_\mu(\tau)d\tau.$$

Here $$j$$ and $$\mu$$ are not summed over.

A similar procedure of going to Laplace space and then enforcing self consistency in both response functions gives coupled equations for the Laplace transforms of the global response functions $$\chi(\tau) = \frac1N\sum_j \chi_j(\tau)$$ and $$\eta(\tau) = \frac1T\sum_\mu \eta_\mu(\tau)$$, namely

$$ \tilde \chi = \frac{1}{z-\tilde \eta},\quad \tilde\eta = \frac{1}{1-q\tilde\chi},$$

where $$q = N/T$$.
This system has solutions

$$ \tilde \chi =\frac{q+z-1\pm i\sqrt{-q^2-(z-1)^2+2q(z+1)}}{2qz},\quad\tilde\eta = \frac{1-q+z\pm i\sqrt{-q^2-(z-1)^2+2q(z+1)}}{2}. $$

The imaginary part of $$\tilde\chi$$ tells us the density of states. Noting that one can rewrite

$$ -q^2-(z-1)^2+2q(z+1) = [(1+\sqrt q)^2 - x][x-(1-\sqrt q)^2],$$

we have that the density of states of the Wishart matrix is

$$ p(x) = \frac{1}{2\pi}\frac{\sqrt{(\lambda_+-x)(x-\lambda_-)}}{qx},\quad \text{with } \lambda_\pm = (1\pm\sqrt q)^2.$$

This formula is valid for $$0\leq q\leq 1$$; for $$q>1$$ one additionally gets a $$(1-1/q)\delta(x)$$ contribution from the zero-eigenvalues.


