---
title: "How to determine the upper critical dimension of a field theory"
date: 2023-06-17
---

<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>

### Introduction
Field theory can be a powerful tool in statistical physics, which allows us to model the behavior of a space-varying field (such as local magnetization, superfluid density, particle orientation) as a function of control parameters like temperature and external magnetic field. Theories whose Hamiltonians can be formulated in terms of spatial fields, often denoted $$\phi({\bf x})$$, are also amenable to momentum-space renormalization group methods.

Coming up with a field theory to describe a system whose Hamiltonian is given in terms of microscopic variables is often a phenomenological affair consisting of writing down all symmetry-permitted terms in the order parameter field. It is then possible to analyze this field theory around criticality (when the order parameter is small and the expansion valid). For example, the Ising model has a Hamiltonian in terms of spin variables given by

$$ H = -J\sum_{\langle ij\rangle} \sigma_i\sigma_j,$$

with the $$\{\sigma_i\}$$ Ising variables, that is $$\sigma_i=\pm 1\forall i$$, and with the sum over all pairs of neighboring sites $$i$$ and $$j$$ on the lattice. However, its field theoretic Hamiltonian in terms of local magnetization $$\phi({\bf x})$$ looks rather different, as we will see below. Since field theory is based on continuous space rather than a lattice model, it can also give us insights into the dependence of the relevant phase transition on the spatial dimension in which it takes place. This dependence on spatial dimension will be the focus of these notes. We will be particularly interested in understanding the notion of _upper critical dimension_ and how it arises from a field theoretic description of a phase transition.

The upper critical dimension $$d_{uc}$$ of a transition is the spatial dimension above which the transition is quantitatively identical to the mean field transition. By quantitatively identical, we mean that the critical exponents (to be discussed below) take on the same values as they do in the mean field, which is a simplified variant of the theory which ignores spatial fluctuations. The fact that such a dimension exists --- above which one can safely ignore spatial fluctuations and still get the right answer --- is nonobvious: our goal in this post is to understand why this is the case, and explain how to calculate the upper critical dimension of a field theory given its Hamiltonian.

### Mean Field Theory
In order to understand the presence of an upper critical spatial dimension $$d_{uc}$$ above which mean field theory becomes exact, we must first understand what mean field theory is. In mean field theory we dispense altogether with spatial nonuniformities in our order parameter field, and take the order parameter to be a single quantity, often denoted by $$\phi$$. Our Hamiltonian is a function of $$\phi$$, whose form depends on the transition of interest. Landau theory motivates the form of the Hamiltonian by essential symmetry constraints arising from the underlying microscopic Hamiltonian. For the Ising model, the order parameter is the average magnetization. Since the Hamiltonian is invariant to an overall change in sign of $$\phi$$, the Landau-Ginzburg Hamiltonian is given (to leading order) by

$$ H = \frac12 r\phi^2 + \frac14 u\phi^4,$$

where $$r$$ and $$u$$ are phenomenological parameters. The magnetization of the system at equilibrium in this mean field theory is given by the value of $$\phi$$ which minimizes $$H$$. Therefore the transition occurs when $$r$$ goes through $$0$$. For $$r$$ positive the equilibrium value of $$\phi$$ is $$0$$, while for $$r$$ negative the equilibrium values are $$\pm\sqrt{|r|/u}$$.
Note that this form of $$H$$ does not give us an idea of the _correlation length_ of the system --- the length scale over which fluctuations in $$\phi$$ are correlated. Indeed this Hamiltonian has no length scale in it, because we are taking $$\phi$$ to be spatially uniform.


### Spatial Fluctuations
The natural extension to the mean field theory outlined above is to make $$\phi$$ a field that depends on space. In this case our Hamiltonian can have gradients of $$\phi$$ which are allowed by the symmetries of the problem (spatial parity), and are physically motivated by the tendency of nearby spins to align. In this case the Landau-Ginzburg Hamiltonian is given by

$$ H = \int d^d {\bf x}\left[(\nabla\phi)^2 + \frac12r\phi^2({\bf x}) + \frac14u\phi^4({\bf x})\right].$$

Note the similarity between this Hamiltonian and the mean field Hamiltonian: indeed if $$\phi$$ is taken to be spatially uniform, this Hamiltonian reproduces the mean field picture. However, here we have crucially added a spatial dimensionality $$d$$ to our formulation of the Hamiltonian.
The question we would like to answer is: when (if ever) does this _field theory_ produce the same results as _mean field theory_ at criticality? The results in question will be critical exponents characterizing the transition, which measure the rate at which quantities like the susceptibility, average magnetization and correlation length change at the transition.

Note that from this form of the Hamiltonian we can already see the emergence of a length scale: the correlation length $$\xi$$ whose value can be determined by dimensional analysis to be of order $$|r|^{-1/2}$$. This will be the length scale over which fluctuations in $$\phi({\bf x})$$ are correlated.

In order to determine $$d_{uc}$$, the strategy we take is the following: we introduce spatial variations in the order parameter field, as done above. We then ask whether these spatial variations are important or not close to criticality of the model. The answer to this question depends on the dimensionality $$d$$ of the field theory, and we will be able to address this question by considering the relative importance of the $$(\nabla \phi)^2$$ term compared to the other terms in $$H$$, as criticality is approached. If this gradient term is large compared to the other terms, then the energy cost of fluctuations is dominant and the order parameter field will look uniform close to the transition, implying the validity of mean field theory. By contrast, if the $$(\nabla \phi)^2$$ term is not the largest term in $$H$$ at criticality, then there will be spatial fluctuations in $$\phi$$ that cannot be ignored, and this invalidates quantitative predictions of mean field theory. We will find that in general, there is a value of $$d$$ above which the $$(\nabla\phi)^2$$ term is dominant: this is the upper critical dimension.

### The $$\phi^n$$ model
Here we will calculate the upper critical dimension of a particular field theory, of which a specific case is the famous $$\phi^4$$ field theory, which describes the Ising model. We also note that for $$d<d_{uc}$$, the condition for spatial fluctuations in $$\phi({\bf x})$$ to have a large energetic cost results in a quantitative condition (the Ginzburg criterion) on the validity of mean field theory. Since the energy cost of fluctuations shrinks relative to other terms as we approach criticality in $$d<d_{uc}$$, mean field theory becomes invalid roughly when the cost of fluctuations becomes comparable to other terms in $$H$$. 

The Hamiltonian we are interested in is
$$ H = \int d^d {\bf x}\left[(\nabla\phi)^2 + \frac12r\phi^2({\bf x}) + \frac 1n u\phi^n({\bf x})\right],$$
where $n$ has to be even to have a convergent partition function. For $$n=4$$ we recover the Hamiltonian of the Ising model.
Mean field theory for this model gives us a free energy of 

$$ H = \frac12 r\phi^2 + \frac 1n u\phi^n,$$

from which one can see that as $$r$$ changes sign from positive to negative, the value of $$\phi$$ that minimizes $$H$$ goes from $$0$$ to $$\pm(|r|/u)^{1/(n-2)}$$. The transition as $$r$$ goes from positive to negative is precisely the disorder-order transition of the model. Our goal is now to see how important the spatial term $$[\nabla\phi]^2$$ is as $$r\to 0$$. To do this, we would like to heuristically estimate the contribution of the this term to the Hamiltonian. Let us start in the ordered phase $$r<0$$ inrease $$r$$ towards criticality. Recall that the correlation length of the field theory scales as $$\xi\sim |r|^{-1/2}$$.

In order to estimate the term $$\int d^d{\bf x}(\nabla\phi)^2$$, we use that fact that the only length scale in the problem is $$\xi$$, and therefore we must have $$\int d^d{\bf x}(\nabla\phi)^2\sim \xi^{d-2}|\phi|^2\sim |r|^{-(d-2)/2}|r|^{2/(n-2)}$$. More physically, one could consider splitting the volume of the system into boxes of linear dimension $$\xi$$, and imagine that $$\phi$$ varies between boxes but not much from box to box --- this would give the same answer. Simplifying our answer, we find that $$\int d^d{\bf x}(\nabla\phi)^2\sim |r|^{\frac{n}{n-2} - d/2}$$. Therefore this quantity diverges at criticality provided that $$d>\frac{2n}{n-2}$$, and furthermore, it is a good exercise to check that it diverges _faster_ than the competing term $$\int d^d{\bf x}\phi^2$$. Therefore we have found the upper critical dimension of the $$\phi^n$$ field theory: it is $$d_{uc} =\frac{2n}{n-2}$$. Note that for $$n=4$$ this gives us the famous $$d_{uc}=4$$ for the Ising model.

### The random field Ising model
We can use similar ideas to calculate the upper critical dimension of the random field Ising model, we we have discussed in a previous post. Here there is a spatially varying (but constant in time) magnetic field with mean $$0$$ that is uncorrelated from one spatial location to another. The field theoretic Hamiltonian is that of the regular Ising model, plus this contribution from this spatially inhomogeneous field.

$$H = \int d^d {\bf x}\left[(\nabla\phi)^2 + \frac12r\phi^2({\bf x}) + \frac 14 u\phi^4({\bf x}) + h({\bf x})\phi({\bf x})\right]$$

where $$h({\bf x})$$ is the random field. As before, it is going to be beneficial to think about averaging our system over blocks of linear dimension $$\xi$$, the correlation length. In this case, the _average_ magnetic field in such a box is approximately gaussian with standard deviation scaling as $$\xi^{-d/2}$$ from the central limit theorem. Meanwhile, we know how the magnetization of the Ising model in zero field scales with uniform magnetic field from the mean field description: this comes from analyzing the Landau-Ginzburg energy $$\frac12 r\phi^2 + \frac14 u\phi^4 + h\phi$$ at criticality when $$r=0$$: from this we conclude that the magnetization goes as $$h^{1/\delta}$$ with $$\delta=3$$, where $$h$$ is the uniform magnetic field.

Therefore the term $$\int d^d{\bf x}(\nabla\phi)^2 $$ can be estimated as $$\xi^{d-2} |\phi|^2\sim \xi^{d-2}\left[\xi^{-d/2}\right]^{2/\delta}\sim \xi^{d-2-d/\delta}$$. Meanwhile, the term $$\int d^d{\bf x}h({\bf x})\phi({\bf x})$$ will scale as $$|\phi|\xi^{d/2}\sim \xi^{d/2-d/(2\delta)}$$ by similar central limit arguments. Therefore in order for the $$(\nabla\phi)^2$$ to dominate at criticality and ensure the mean field is valid, we must have 

$$ \frac{\xi^{d-d/\delta-2}}{\xi^{d/2-d/(2\delta)}}\to\infty\text{ as }\xi\to\infty.$$

Using the Ising value of $$\delta=3$$, justified by the fact that as the correlation length diverges, the system looks more and more like a pure Ising model in a uniform field, one finds that this condition is met when $$d>6$$. This gives us the upper critical dimension of the random field Ising model as $$d_{uc}=6$$.

The types of arguments here form the basis for the renormalization group for second order phase transitions, as they give us a starting point around which we can expand our theory below the upper critical dimension, where we know quantitative properties at criticality. 

### What about the lower critical dimension?
Although, as we have seen, there is a somewhat systematic way to calculate the upper critical dimension of a field theory, calculating the lower critical dimension is in general much harder. This can require arguments of the type of Hohenberg-Wagner-Mermin, Peierls or Imry-Ma as we have discussed in previous posts. In addition, calculating $$d_{uc}$$ is not always easy: there are models for which there is no consensus on the upper critical dimension and we do not have a field theoretic description of the phase transition: for example the Edwards-Anderson model, also known as the random bond Ising model.

### References
Chaikin and Lubensky: Principles of Condensed Matter Physics, Chapter 5
Goldenfeld: Lectures on Phase Transitions and the Renormalization Group, Chapter 7
