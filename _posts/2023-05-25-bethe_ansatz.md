---
title: "What is the Bethe Ansatz?"
date: 2023-05-25
---

<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>

# Introduction

The Bethe Ansatz has found widespread use in questions from condensed
matter to stochastic processes to high energy physics. But what is it?
At the most elementary level, it as a guess for the form of the
eigenvectors of a matrix that in some cases allows us to diagonalize a
matrix with certain properties, thereby yielding its complete spectrum.
However the Bethe ansatz, after its initial invention by Hans Bethe in
1931, has taken on a life of its own and essentially underlies the field
of integrable systems: in some sense “integrable” is synonymous with
“Bethe ansatz solvable.” In these notes we will outline the coordinate
Bethe ansatz in the context that led to its creation, and deploy it in
considerable detail. We will also discuss the highly nontrivial fact
that the Bethe ansatz works at all, and what this means in terms of
simplifying the problem we wish to solve. The problem we discuss below
is that of finding the spectrum of the Heisenberg spin 1/2 XXX chain: a
model of a one dimensional quantum magnet with nearest-neighbor
isotropic spin interactions.

We do not assume any knowledge of the Bethe ansatz, but it will be
helpful to be familiar with the quantum mechanics of spin: in particular
the Pauli spin matrices, and the representation of quantum mechanical
Hilbert space as a tensor product of local spaces. We should state at
the outset that if one’s goal is to understand the Bethe ansatz in
general without an interest in quantum mechanics, there are similarly
illuminating use cases for diagonalizing the Markov matrix of particular
families of stochastic processes — we will discuss the latter in a
separate set of notes. For now we will proceed with the quantum
mechanical problem, which will soon be converted into a problem in
linear algebra.

# The Heisenberg spin chain

The model of interest here will be the Heisenberg spin 1/2 chain, which
is a quantum model of magnetism in one dimension. Its Hamiltonian can be
represented as a sum of local products of spin operators:

$$H  = J \\sum\_{i=1}^L \\mathbf S_i\\cdot \\mathbf S\_{i+1},\\label{eq:hamiltonian}$$
where the vector **S**<sub>*i*</sub> denotes the spin operator
(*S*<sub>*i*</sub><sup>*x*</sup>,*S*<sub>*i*</sub><sup>*y*</sup>,*S*<sub>*i*</sub><sup>*z*</sup>)
on site *i*, comprised of the spin operators in each of the spatial
directions. We will use periodic boundary conditions so that *L* + 1 is
identified with 1. Hilbert space grows exponentially with the number of
particles, and so *H* is fact a 2<sup>*L*</sup> × 2<sup>*L*</sup>
matrix, as we will see explicitly below. The spin operators on a
particular site of the chain are given by

*S*<sub>*i*</sub><sup>*α*</sup> = 𝟙<sub>1</sub> ⊗ ⋯ ⊗ 𝟙<sub>*i* − 1</sub> ⊗ *σ*<sub>*α*</sub> ⊗ 𝟙<sub>*i* + 1</sub> ⊗ ⋯ ⊗ 𝟙<sub>*L*</sub>,
for *α* = *x*, *y*, *z*, with
*σ*<sub>*x*</sub>, *σ*<sub>*y*</sub>, *σ*<sub>*z*</sub> representing the
Pauli spin 1/2 matrices, which are 2 × 2 matrices.
$$\\sigma_x = \\begin{pmatrix} 0&1\\\\1&0\\end{pmatrix},\\quad \\sigma_y = \\begin{pmatrix}0 & -i \\\\ i&0\\end{pmatrix},\\quad \\sigma_z = \\begin{pmatrix}1&0\\\\0&-1\\end{pmatrix}.$$
Here 𝟙 is a 2 × 2 identity matrix, irrespective of its index, which
simply labels the site on which it acts. The tensor product symbol ⊗ is
a way of combining the degrees of freedom from each of the individual
Hilbert spaces of the spins into one large Hilbert space for the whole
system. Explicitly in a matrix representation, we have
$$\\begin{pmatrix}a\_{11} & a\_{12}\\\\ a\_{21} & a\_{22}\\end{pmatrix}\\otimes \\begin{pmatrix}b\_{11} & b\_{12}\\\\ b\_{21} & b\_{22}\\end{pmatrix} = \\begin{pmatrix} a\_{11}b\_{11} & a\_{11}b\_{12} & a\_{12}b\_{11} & a\_{12}b\_{12}\\\\
a\_{11}b\_{21} & a\_{11}b\_{22} & a\_{12}b\_{21} & a\_{12}b\_{22}\\\\
a\_{21}b\_{11} & a\_{21}b\_{12} & a\_{22}b\_{11} & a\_{22}b\_{12}\\\\
a\_{21}b\_{21} & a\_{21}b\_{22} & a\_{22}b\_{21} & a\_{22}b\_{22}\\end{pmatrix}.$$

The sign of *J* in Equation
<a href="#eq:hamiltonian" data-reference-type="ref" data-reference="eq:hamiltonian">[eq:hamiltonian]</a>
determines whether the chain is ferromagnetic or antiferromagnetic. Note
the similarity between this model and the one dimensional classical
Ising model. The difference is that here each spin has three components
in the *x*, *y* and *z* directions respectively, and these are
represented by non-commuting operators.

# Constructing the Bethe ansatz

As discussed earlier, we want to find the eigenvalues and eigenvectors
of the Hamiltonian defined in Equation
<a href="#eq:hamiltonian" data-reference-type="ref" data-reference="eq:hamiltonian">[eq:hamiltonian]</a>.
This will give us the eigenstates and corresponding energies of the
magnet, and in principle will fully solve the system and its dynamics,
allowing us to calculate whatever we want. Things will not quite turn
out to be that nice, but we can still make significant progress with the
Bethe ansatz. The key will be to think about how the Hamiltonian
operator changes a state of the system when applied to it. We know that
a state of the system will be a 2<sup>*L*</sup>-dimensional vector. Let
us work in the *z* basis, in which case our basis vectors are states of
the system described by the *z* component of the spin at each site,
which can be 1 or  − 1, corresponding to
$\\begin{pmatrix}1\\\\0\\end{pmatrix}$ or
$\\begin{pmatrix}0\\\\1\\end{pmatrix}$ respectively. These states can be
represented as a tensor product of spins ↑ and ↓ at each site, in which
case we might use a shorthand like \| ↑  ↑  ↓ ⟩ for a chain of three
spins, which corresponds to state vector
$$\|\\uparrow\\uparrow\\downarrow\\rangle = \|\\uparrow\\rangle \\otimes \|\\uparrow\\rangle \\otimes\|\\downarrow\\rangle = \\begin{pmatrix}1\\\\0\\end{pmatrix}\\otimes \\begin{pmatrix}1\\\\0\\end{pmatrix}\\otimes \\begin{pmatrix}0\\\\1\\end{pmatrix}.$$

We will try to form eigenvectors of our Hamiltonians are linear
combinations of states of this form. To simplify notation, we will use
the notation \|*n*<sub>1</sub>, …, *n*<sub>*p*</sub>⟩ to denote a state
with down spins at sites on the chain except for the sites
*n*<sub>1</sub>, …*n*<sub>*p*</sub>. Explicitly, these means that for
*L* = 3, we have \|1⟩=\| ↓  ↑  ↑ ⟩, and \|1,3⟩=\| ↓  ↑  ↓ ⟩, etc.
Eventually we will want to take *L* to be very large. Then states with,
e.g. one spin flipped relative to all the others will correspond to the
high (or low) edge of the density of states for positive (or negative)
*J*. We will think of these states as “excitations” of *p* spins away
from our reference configuration of all spins up.

## Single spin excitations

First, we would like to study, for arbitrary *L*, how we might construct
an eigenfunction of *H* out of a linear combination of states with
*p* = 1, i.e. a single spin pointing down while all others point up.
Such a state can be notated as \|*n*⟩ where *n* is the index of the site
at which the down-spin is located. The crucial observation here is that
*H*\|*n*⟩=(*L*−2)\|*n*⟩ + 2\[\|*n*−1⟩+\|*n*+1⟩−\|*n*⟩\].
How can we see this? Thinking of the Hamiltonian *H* as a sum of many
local products of spin operators acting on sets of neighboring spins, as
in Equation
<a href="#eq:hamiltonian" data-reference-type="ref" data-reference="eq:hamiltonian">[eq:hamiltonian]</a>,
most of the bonds (*L* − 2 of them) will simply be acted on by the
identity operator. The nontrivial contribution will come from the bonds
(on either side of the *n*th site) that are not satisfied. By explicit
computation with the 4 dimensional subspace of Hilbert space
corresponding to two neighboring spins which are oppositely oriented, we
can come to the conclusion above.

Now we see that the family of states indexed by *n* has the nice
property that we can explicitly write down the operation of *H* on a
single one of these states in terms of other states indexed by different
*n*. This will allow us to solve for eigenstates of *H* as a linear
combinations of the \|*n*⟩. We guess an eigenstate
\|*Ψ*⟩=∑<sub>*n*</sub>*z*<sup>*n*</sup>\|*n*⟩. Therefore the condition
on \|*Ψ*⟩ in order for it to be an eigenstate of *H* with eigenvalue *λ*
is
*λ*\|*Ψ*⟩=∑<sub>*n*</sub>\[*z*<sup>*n*</sup>(*L*−4)+2*z*<sup>*n* − 1</sup>+2*z*<sup>*n* + 1</sup>\]\|*n*⟩.

Another way to notate this (which we will use hereafter) is if we define
*ψ*(*n*) to be the coefficient in front of \|*n*⟩. Then we can write
*λ**ψ*(*n*) = (*L*−4)*ψ*(*n*) + 2*ψ*(*n*−1) + 2*ψ*(*n*+1).
We additionally have *ψ*(*n*+*L*) = *ψ*(*L*) from periodic boundary
conditions. Plugging in the ansatz *ψ*(*n*) = *z*<sup>*n*</sup> tells us
that *λ* = *L* − 4 + 2*z*<sup>−1</sup> + 2*z* from the eigenvalue
conditions, and *z*<sup>*L*</sup> = 1 from periodicity. Therefore we
find eigenvectors if *z* = *e*<sup>*i*2*π**k*/*L*</sup>, with
corresponding eigenvalues
*λ*<sub>*k*</sub> = *L* − 4 + 2*z*<sup>−1</sup> + 2*z* = *L* + 4\[cos(2*π**k*/*L*)−1\],
for *k* ∈ {1, …, *L*}.

We have therefore found *L* eigenvector-eigenvalue pairs for our
Hamiltonian in terms of linear combinations of the
\|*n*<sub>1</sub>, …*n*<sub>*p*</sub>⟩ states with *p* = 1. However this
is not the whole story — in particular there should be 2<sup>*L*</sup>
eigenvector-eigenvalue pairs in total. Below we will outline the
procedure for finding the rest of these, which leads us to the Bethe
ansatz.

## Two-spin excitations

Here we will outline the case of *p* = 2: that is, we will try to form
an eigenstate from a linear combination of states with two down-spins
somewhere in the chain of up-spins. These states can be notated as
\|*n*, *m*⟩ with 1 ≤ *n* \< *m* ≤ *L*. Following our approach for
*p* = 1, the crucial observation is that
$$\\begin{aligned}
H\|n,m\\rangle &= (L-8)\|n,m\\rangle + 2\[\|n+1,m\\rangle + \|n-1,m\\rangle + \|n,m+1\\rangle + \|n,m-1\\rangle\]\\\\
H\|n,n+1\\rangle &= (L-4)\|n,n+1\\rangle + 2\[\|n-1,n+1\\rangle + \|n,n+2\\rangle\].\\end{aligned}$$
This first of these observations is a natural generalization of Equation
<a href="#eq:eigp1" data-reference-type="ref" data-reference="eq:eigp1">[eq:eigp1]</a>
to the case *p* = 2, which assumes the two down-spins are spatially
separated and therefore act just like isolated single-spin excitations.
However we need to separately treat the case where these two spin
excitations are neighbors, and that is where the second equation comes
in. In this case we have two down-spins next to each other in the chain
of up-spins, and accordingly the number of unsatisfied bonds is two. By
considering the local action of the successive terms in the Hamiltonian
on our chain carefully, we can come up with the second equation above.
We will refer to this as a “collision condition,” since it treats the
case where our two spin excitations “collide” in space. Rewriting these
two conditions in our alternative notation gives

$$\\begin{aligned}
\\lambda \\psi(n,m) &= (L-8)\\psi(n,m) + 2\\psi(n-1,m) + 2\\psi(n+1,m) + 2\\psi(n,m-1) +2\\psi(n,m+1)\\\\
\\lambda \\psi(n,n+1) &= (L-4)\\psi(n,n+1) + 2\\psi(n-1,n+1) +2\\psi(n,n+2).\\end{aligned}$$
In addition, periodic boundary conditions give us
*z*<sub>1</sub><sup>*L*</sup>*z*<sub>2</sub><sup>*L*</sup> = 1 and
*ψ*(*n*,*L*+1) = *ψ*(1,*n*). \[Think about why this second statement is
the correct boundary condition!\]

Now we make the ansatz
\|*Ψ*⟩=∑<sub>1 ≤ *n* \< *m* ≤ *L*</sub>(*A**z*<sub>1</sub><sup>*n*</sup>*z*<sub>2</sub><sup>*m*</sup>+*B**z*<sub>2</sub><sup>*n*</sup>*z*<sub>1</sub><sup>*m*</sup>)\|*n*, *m*⟩ ⟹ *ψ*(*n*,*m*) = *A**z*<sub>1</sub><sup>*n*</sup>*z*<sub>2</sub><sup>*m*</sup> + *B**z*<sub>2</sub><sup>*n*</sup>*z*<sub>1</sub><sup>*m*</sup>.
In addition to determining *z*<sub>1</sub> and *z*<sub>2</sub>, we need
to determine the ratio *A*/*B* (the overall amplitude of the eigenvector
is a free parameter).

Plugging in this ansatz, we conclude that
$$\\lambda = L-8 + 2\\left(z_1+z_2+\\frac{1}{z_1}+\\frac{1}{z_2}\\right).$$
Then from the cancellation condition we get
$$\\frac AB = -\\frac{2z_1-1-z_1z_2}{2z_2-1-z_1z_2}.$$
The boundary conditions then give
*z*<sub>1</sub><sup>*L*</sup>*z*<sub>2</sub><sup>*L*</sup> = 1 and
$$\\frac{A}{B} = \\frac{z_2z_1^n - z_2^n z_1^{L+1}}{z_1^n z_2^{L+1}-z_1z_2^n} = z_1^L,$$
where the second equality comes from using the fact that
*z*<sub>1</sub><sup>*L*</sup>*z*<sub>2</sub><sup>*L*</sup> = 1. This
allows us to eliminate the ratio *A*/*B*, and we obtain two equations
that constrain *z*<sub>1</sub> and *z*<sub>2</sub>:
$$z_1^Lz_2^L=1\\quad\\text{and}\\quad z_1^L = -\\frac{z_1z_2-2z_1+1}{z_1z_2-2z_2+1}.$$
Note that if we want we can write these symmetrically for
*z*<sub>1</sub> and *z*<sub>2</sub>, namely
$$z_i^L = -\\prod\_{k=1}^2\\frac{z_iz_k-2z_i+1}{z_iz_k-2z_k+1}.$$
Solutions to these equations will allow us to determine the eigenvalues
and eigenvectors which can be built out of two-spin excitations!

## Three-spin excitations

So far we have systematically found the eigenvectors that can be built
from states with one and two spins excited from the reference
configuration. This has hinged on the appropriate ansatz for the form of
these eigenvectors, which in essence constituted a proto-Bethe ansatz in
each of their respective cases. However the nature of the Bethe ansatz
is more apparent when we consider three-spin excitations. Doing out the
three-spin case is a bit of a slog, but it is somewhat illustrative
about the general case. Having noticed some patterns in the one and
two-spin excitation cases above, we can write down the following
conditions for our would-be coefficients for the three-spin excitations
that must be satisfied to construct and eigenvector:
$$\\begin{aligned}
\\lambda \\psi(n,m,l) &= (L-12) \\psi(n,m,l) + 2\[\\psi(n-1,m,l) + \\psi(n+1,m,l) +\\\\
&\\psi(n,m-1,l) + \\psi(n,m+1,l) = \\psi(n,m,l-1) + \\psi(n,m,l+1)\]\\nonumber\\\\
\\lambda \\psi(n, n + 1, l) &= (L - 8) \\psi(n, n + 1, l) +  \\\\&2\[\\psi(n - 1, n + 1, l) + \\psi(n, n + 2, l) + \\psi(n, n + 1, l - 1) + \\psi(n, n + 1, l + 1)\]\\nonumber\\\\
\\lambda\\psi(n, m,  m + 1) &= (L - 8) \\psi(n, m, m + 1) + \\\\&2 \[\\psi(n - 1, m, m + 1)+ \\psi(n + 1, m, m + 1) + \\psi(n, m - 1, m + 1) + \\psi(n, m, m + 2)\]\\nonumber\\\\
 \\psi(n + L, m + L, l + L) &= \\psi(n, m, l) \\\\
 \\psi(n, m, L + 1) &= \\psi(1, n, m).\\end{aligned}$$
The first of these treats the cases where the three excitations are
separated along the length of the chain. The second and third handle the
two body collisions, and the last two specify periodic boundary
conditions. The goal is to make an ansatz for *ψ*(*n*,*m*,*l*) which
allows us to satisfy these conditions. However, first we will point out
a very important fact.

### Three body collision is redundant

In the above, we have two collision conditions instead of just one as we
had in the two-spin excitation case: this is because there are two
possible two-body collisions when we have three spin excitations along
our chain. However there is a third collision, a three-body collision,
that can also occur for states where all three spins are neighboring
each other, which corresponds to coefficients of form
*ψ*(*n*,*n*+1,*n*+2). The additional condition for these coefficients is
*λ**ψ*(*n*,*n*+1,*n*+2) = (*L*−4)*ψ*(*n*,*n*+1,*n*+2) + 2*ψ*(*n*−1,*n*+1,*n*+2) + 2*ψ*(*n*,*n*+1,*n*+3).
This would seem to complicate our problem, as we now have an addition
condition to satisfy. However, here something very nice happens. One can
see by explicit calculation that the three-body collision condition is
automatically satisfied if we have the first three conditions from above
satisfied, which are just the generic case and the two body collisions.
The way to see this (which the reader should try!) is to plug in the
appropriate *n*, *m* and *l* so that one gets an equation for
*ψ*(*n*,*n*+1,*n*+2). For example, in the first equation, one should set
*m* = *n* + 1, *l* = *n* + 2. The fact that the three body collision
condition is automatically satisfied by the two body conditions is the
key to the solvability (the *integrability*) of this model.

### Finding the Bethe equations

Having determined that we do not need the three-body collision condition
in order to fully diagonalize our matrix, we will proceed to do without
it. For the three-spin excitation case, we make the ansatz
*ψ*(*n*,*m*,*l*) = *A**z*<sub>1</sub><sup>*n*</sup>*z*<sub>2</sub><sup>*m*</sup>*z*<sub>3</sub><sup>*l*</sup> + *B**z*<sub>1</sub><sup>*n*</sup>*z*<sub>3</sub><sup>*m*</sup>*z*<sub>2</sub><sup>*l*</sup> + *C**z*<sub>2</sub><sup>*n*</sup>*z*<sub>1</sub><sup>*m*</sup>*z*<sub>3</sub><sup>*l*</sup> + *D**z*<sub>2</sub><sup>*n*</sup>*z*<sub>3</sub><sup>*m*</sup>*z*<sub>1</sub><sup>*l*</sup> + *E**z*<sub>3</sub><sup>*n*</sup>*z*<sub>1</sub><sup>*m*</sup>*z*<sub>2</sub><sup>*l*</sup> + *F**z*<sub>3</sub><sup>*n*</sup>*z*<sub>2</sub><sup>*m*</sup>*z*<sub>1</sub><sup>*l*</sup>.
This shows the structure of the Bethe ansatz: it is a sum of *p*! terms
of varying amplitudes, and our job is to find the ratios of the *p*!
amplitudes as well as the complex numbers
*z*<sub>1</sub>, …, *z*<sub>*p*</sub>.

Plugging in our ansatz to the three-spin equations, *λ* can be found to
be
$\\lambda = L-12 + 2\\left(z_1+z_2+z_3 + \\frac{1}{z_1} + \\frac{1}{z_2} + \\frac{1}{z_3}\\right)$
and therefore can be eliminated, and one of the boundary conditions
gives
*z*<sub>1</sub><sup>*L*</sup>*z*<sub>2</sub><sup>*L*</sup>*z*<sub>3</sub><sup>*L*</sup> = 1.
Then there are three remaining conditions. These conditions must be
satisfied no matter the values of the {*z*<sub>*i*</sub>} and
*n*, *m*, *l*. Therefore we can isolate terms of like powers in
*z*<sub>1</sub>, *z*<sub>2</sub>, *z*<sub>3</sub> and set their
coefficients to 0. This gives us a number of conditions on the
amplitudes *A*, …, *F*. In particular we find that
$$\\begin{aligned}
\\frac AC &= -\\frac{z_1z_2-2z_1-1}{z_1z_2-2z_2-1},\\quad \\frac{D}{F} = -\\frac{z_2z_3-2z_2+1}{z_2z_3-2z_3+1},\\quad \\frac BE = -\\frac{z_1z_3-2z_1+1}{z_1z_3-2z_3+1},\\\\
\\frac AB &= -\\frac{z_2z_3-2z_2+1}{z_2z_3-2z_3+1},\\quad \\frac CD = -\\frac{z_1z_3-2z_1+1}{z_1z_3-2z_3+1},\\quad \\frac EF = -\\frac{z_1z_2-2z_1+1}{z_1z_2-2z_2+1}.\\end{aligned}$$
Note that we have found 6 conditions even though just 5 would have been
enough to uniquely specify all the amplitudes. This hints at some kind
of algebraic structure between the amplitudes. If we start at one
amplitude, say *A*, and find its relationship to, say *E*, there is more
than one way to do this, and these must yield the same answer.

Thus far we have used all the conditions (eigenvalue condition, two
collision conditions, and
*ψ*(*n*+*L*,*m*+*L*,*l*+*L*) = *ψ*(*n*,*m*,*l*)) except the second
periodic boundary condition, which is
*ψ*(*n*,*m*,*L*+1) = *ψ*(1,*n*,*m*). Enforcing this last condition will
allow us to obtain a closed set of equations for the
{*z*<sub>*i*</sub>}. This last condition reads
$$\\begin{aligned}
 0 =
A(z_1^n z_2^m z_3^{L+1} - z_1 z_2^n z_3^m) +
B(z_1^{n} z_2^{L+1} z_3^m - z_1 z_2^m z_3^n)+
C(z_1^m z_2^n z_3^{L+1} - z_1^n z_2 z_3^m)+\\\\
D(z_1^{L+1} z_2^n z_3^m - z_1^m z_2 z_3^n)+
E(z_1^m z_2^{L+1} z_3^n - z_1^n z_2^m z_3)+
F(z_1^{L+1} z_2^m z_3^n - z_1^m z_2^n z_3).\\end{aligned}$$
Performing a similar exercise to enforce consistency by setting the
coefficients of each monomial to 0, we obtain
$$z_1^L = \\frac BF = \\frac AD,\\quad z_2^L = \\frac CB = \\frac DE,\\quad z_3^L = \\frac FC = \\frac EA.$$
Given our expressions for the amplitudes above, one can check that these
equations are equivalent to the *Bethe equations*
$$z_i^L = \\prod\_{k=1}^3\\frac{z_iz_k-2z_i+1}{z_iz_k-2z_k+1}.$$
As before, we have reduced the task at hand to solving these coupled
algebraic equations!

## Multi-spin excitations and the Bethe equations

For general *p*, the Bethe ansatz is
$$\\psi(n_1,\\dots n_p) = \\sum\_{\\sigma\\in S_p}A\_{\\sigma} \\prod\_{k=1}^p z\_{\\sigma(k)}^{n_k}.$$

We have already seen that the three body collision factors into two body
collisions and thus provides no new information. This property is what
makes our system tractable. In fact collisions of any degree will factor
totally into two-body collisions, and so these are the only conditions
that we need to enforce.

Therefore the number of conditions we can enforce in order to solve for
our eigenfunctions and eigenvectors is one eigenvalue condition, *p* − 1
two-body collisions, and two boundary conditions, namely from
translating all excitations by *L* and from the case where the last
excitation is at the lattice site *L*. This is a total of *p* + 1
conditions. The number of unknowns in our ansatz is *p*! − 1 + *p*, for
the amplitudes of the various terms (modulo an overall factor) and and
the values of the *z*<sub>*k*</sub> themselves. However, since the
amplitudes are related to one another by functions of the
*z*<sub>*k*</sub>, we need only to solve for one of the ratios, and the
others will follow. Note that the reduction in complexity due to the
factorization of the collisions is commensurate with the reduction in
complexity from the algebraic relationship between amplitude ratios.
Therefore the total number of unknowns is also *p* + 1. This will allow
us to solve for the *z*<sub>*i*</sub> for *i* ∈ {1, …, *p*}. In general
one finds that these satisfy
$$z_i^L = (-1)^{p+1}\\prod\_{k=1}^p\\frac{z_iz_k-2z_i+1}{z_iz_k-2z_k+1},$$
for excitations of *p* spins. These are the general Bethe equations.

The fact that the number of conditions and the number of unknowns are
both *p* + 1 is highly nontrivial and is what makes this model solvable
by the Bethe ansatz. In general this will not be true: but for a class
of so-called *integrable* models this property holds, and allows for
solution by the Bethe ansatz.

# Solving the Bethe equations

In principle, as we have said, the full spectrum of our Hamiltonian can
be found by solving the Bethe equations for *p* from 1 to *L*. Although
we have seriously simplified the problem from the original
diagonalization of a 2<sup>*L*</sup> × 2<sup>*L*</sup> matrix to the
solution of *p* coupled algebraic equations, finding the solutions of
these equations is still quite nontrivial.

To see how this works, consider the case of *p* = 2. Then the Bethe
equations become the same for *z*<sub>1</sub> and *z*<sub>2</sub>,
namely
(1<sup>1/*L*</sup>+1)(*z*<sup>*L*</sup>+1) − 2(*z*+1<sup>1/*L*</sup>*z*<sup>*L* − 1</sup>) = 0,
where we have used the fact that
*z*<sub>1</sub>*z*<sub>2</sub> = 1<sup>1/*L*</sup> where
1<sup>1/*L*</sup> is an *L*th root of unity. This equation has *L*
solutions which can be found numerically. Furthermore, solutions where
*z*<sub>1</sub> = *z*<sub>2</sub> are invalid, as can be checked given
the form of the Bethe ansatz for *p* = 2 above. Therefore we have
$\\binom L 2$ solutions for the pair *z*<sub>1</sub> and
*z*<sub>2</sub>. The same idea continues for larger values of *p*,
though it is much more difficult (even numerically) and I do not know of
a systematic way of solving these equations. I believe that for each
*p*, we get $\\binom Lp$ valid solutions of the
{*z*<sub>1</sub>, …*z*<sub>*p*</sub>}, which therefore account for all
2<sup>*L*</sup> eigenvalues since $\\sum\_{p=1}^L \\binom Lp = 2^L$.
There are related cases (which we will discuss in other notes) where the
Bethe equations are easier to solve, but the XXX chain requires quite a
lot of work to solve.

We will end our discussion here for now: having discussed the derivation
of the Bethe equations and the nontrivial facts that allow us to solve
the XXX model by the appropriate Bethe ansatz. There is lots more to be
said about solving the Bethe equations, as well as different
incarnations of the Bethe ansatz (algebraic, functional, etc.) which we
may address in further notes.

# References

[Levkovich-Maslyuk
2016](https://iopscience.iop.org/article/10.1088/1751-8113/49/32/323004/pdf)  
[maybe useful for solving Bethe
equations](https://yauc.seu.edu.cn/_upload/article/files/0b/e0/206fa9724645829f4e9b4c29aed9/1de7484d-3293-4426-86d8-7b97b54a2784.pdf)  
[Bethe’s original paper in
translation](https://homepages.dias.ie/dorlas/Papers/Bethe.pdf)  
[Introduction to Bethe Ansatz
I](https://arxiv.org/pdf/cond-mat/9809162.pdf)  
[useful resources listed here (Math
stackexchange)](https://mathematica.stackexchange.com/questions/165262/solving-bethe-ansatz-equations)  
[Nepomechie Ravanini 2003](https://arxiv.org/pdf/hep-th/0307095.pdf)  
[Vieira Lima-Santos 2015](https://arxiv.org/pdf/1502.05316.pdf)  
[Fadeev 1996, algebraic Bethe
ansatz](https://arxiv.org/pdf/hep-th/9605187.pdf)  
[Kirone Mallick lecture](https://www.youtube.com/watch?v=2AuFxEWa48E)
