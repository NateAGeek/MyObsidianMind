## Overview
The paper discusses the way some neurons in models pack unrelated concepts into a single neuron, kinda like a compression of multiple data sets into one node. They call this "polysemanticity" of neurons.

### Introduction
The paper discusses how models, toy models in their case, encode relatively overlapping data as more features are introduced. They use the concepts of superposition and the interference principles to encode more sparsely data into one neuron. Allowing for the neuron to contribute to compressing more relations than are linearly learned. 
![[../../../../NotebookAssets/Pasted image 20240527223408.png]]

They then also lead to how this interference can lead to an almost "eureka" moment and explain how models that jump in learning and grokking, where the model generalized after overfitting,

**Key Results**
* They do demonstrate superposition is real
* Both monosemantic and polysemantic neurons can form
* computation on performance of superposition is possible
* Phase changes govern superposition of features
* Superposition can organize features into geometric structures

## Definitions and Motivations: Features, Directions, and Superposition

The sections defines some areas of introspection of how data is composed in these neurons. They define goals of defining what makes the neurons encode data. 

* **Decomposability**: The way features are independently understood within the neurons structures.
* **Linearity**: how the features are representing directionally in dimensional spaces. 
* **Privileged Basis**: The dimensionality of the features take higher priority in the encoded neuron, aka the neuron has more priority of the feature compared to other neurons. Like how some layers in covnets detect edges to identify faces (feature).
* **Superposition**: Are neurons that have multiple encoding of the features that compress relational encodings.

## Empirical Phenomena
They go over the current way "features" have been empirically discussed and discovered to encode information. Such as the following:
* **Word Embeddings**: How word embeddings become vector relations over large trainings. The vector relations contain a degree of relation, such as V("king") - V("man") + V("woman") = V("queen")
* **Latent Spaces**: 