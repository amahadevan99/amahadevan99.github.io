---
title: "How to determine the upper critical dimension of a field theory"
date: 2023-05-25
---

<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>

### Introduction
Field theory can be a powerful tool in statistical physics, which allows us to model the behavior of a field (such as local magnetization, superfluid density, particle orientation) in space and time. In particular, the framework of the momentum space renormalization group allows us to deal with Hamiltonians formulated in terms of fields, and to integrate out high-wavevector components of these field to understand their low energy physics.

Coming up with the correct field theory to describe a system whole Hamiltonian is given in terms of microscopic variables is often a phenomenological affair consisting of writing down all symmetry-permitted terms in the order parameter field. It is then possible to analyze this field theory around criticality (when the order parameter is small and the expansion valid).

The upper critical dimension of a theory is the spatial dimension above which the phase transition of the theory behaves identically to as if the theory were taking place in the mean field, or in the infinite dimensional limit, wherein the field at a specific location is coupled to all other locations. The fact that such a dimension exists in the first place is highly nonobvious: our goal in this post is to understand why this is the case, and explain how to calculate the upper critical dimension of a field theory given its Hamiltonian.

### References

