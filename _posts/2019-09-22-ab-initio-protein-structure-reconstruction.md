---
layout: post
title: "Ab Initio Protein Structure Reconstruction"
subtitle: "Automated Multi-Conformation Recovery from Cryo-EM Projections"
date: 2019-09-22 10:00:00 -0800
categories: [research, publications]
tags: [cryo-em, tomography, protein-structure, machine-learning, image-processing, iit-bombay]
excerpt: "A novel algorithm that automatically reconstructs multiple protein conformations from mixed 2D projections without knowing viewing angles or the number of structures present."
author: Arunabh Ghosh
toc: true
toc_sticky: true
feature_type: publication
featured: true
---

## The Problem: Unmixing Molecular Shapes

Biological molecules are dynamic machines that constantly change shape (or "conformation") to perform their functions. When scientists use [cryo-electron microscopy](https://en.wikipedia.org/wiki/Cryogenic_electron_microscopy){:target="_blank"} (cryo-EM), they capture thousands of 2D projection images of these molecules from different angles. The core challenge is that a single sample contains a mix of these different conformations, a problem known as **structural heterogeneity**.

Traditional reconstruction algorithms often assume all projections come from one identical structure. This forces them to average dissimilar shapes, resulting in blurry reconstructions that obscure crucial details. Existing methods to separate conformations often require known reference structures or tedious manual classification, which is slow, biased, and can fail to identify new, undiscovered shapes.

## Our Solution: A Fully Automated Pipeline

We developed an automated algorithm that solves the [ab initio reconstruction problem](https://en.wikipedia.org/wiki/Ab_initio){:target="_blank"} for heterogeneous samples without human intervention. Here's how it works:

1. **Robust Clustering**: We first use a variant of hierarchical clustering (**single-linkage clustering**) to group projections. Unlike standard k-means, this method creates "pure" clusters that contain projections from only one conformation, even in high-noise conditions.

2. **Projection Denoising**: The projections in each pure cluster are averaged and then cleaned using a patch-based [PCA denoising](https://en.wikipedia.org/wiki/Principal_component_analysis){:target="_blank"} algorithm. This produces a small set of clean, representative projections for each conformation.

3. **Classification & Angle Estimation**: We use a novel combination of techniques to sort the representative projections. A **graph Laplacian-based algorithm** reveals the underlying structure of the data, allowing us to automatically determine the number of conformations present. We then use the [Helgason-Ludwig consistency conditions](https://en.wikipedia.org/wiki/Radon_transform#Radon_transform_and_the_Fourier_transform){:target="_blank"} to find initial estimates for the viewing angle of each projection.

4. **Iterative Refinement**: Finally, we alternately refine the viewing angles and reconstruct the structure for each class using [filtered back-projection](https://en.wikipedia.org/wiki/Tomographic_reconstruction){:target="_blank"}. This iterative process minimizes the reconstruction error, converging on a high-fidelity model of each distinct conformation.

## Key Innovation

Our method's strength comes from uniquely combining three mathematical frameworks:

1. **Graph Laplacian techniques** to discover the number of distinct conformations automatically.
2. **Moment-based constraints** (HLCC) to connect 2D projections to 3D orientations without prior knowledge.
3. **A robust statistical framework** that withstands significant noise and correctly separates projections from different structures.

Crucially, the algorithm requires **no prior structural information, templates, or even knowledge of how many conformations exist**. In experiments on protein complexes like [Lipase](https://en.wikipedia.org/wiki/Lipase){:target="_blank"}, our method successfully separated and reconstructed up to eight different conformations from a single dataset, even with **high levels of noise** (noise standard deviation up to 30% of the average signal value, i.e., σ=0.3a).

This approach enables researchers to discover novel protein states and understand molecular dynamics, free from the bias of existing structural knowledge.

## Paper Details

- **Title**: Ab Initio Tomography With Object Heterogeneity and Unknown Viewing Parameters
- **Conference**: IEEE International Conference on Image Processing (ICIP) 2019
- **Presentation**: Oral
- **Authors**: Arunabh Ghosh¹, Ritwick Chaudhry², Ajit Rajwade³
- **Affiliations**: ¹Dept. of EE, IIT Bombay; ²Adobe Research; ³Dept. of CSE, IIT Bombay
- **Pages**: 1257-1261
- **DOI**: [10.1109/ICIP.2019.8803750](https://ieeexplore.ieee.org/document/8803750){:target="_blank"}
