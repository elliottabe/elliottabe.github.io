---
title: "TiDHy: Timescale Demixing via Hypernetworks"
summary: A key feature of TiDHy is that it directly learns the intrinsic timescales of the data (rather than as a hyperparameter) and demixes independent systems, yielding interpretable dynamics. Using synthetic data, we show that TiDHy can demix multiple SLDSs from partially superimposed observations, even when they span orders-of-magnitude different timescales.
tags:
  - Deep Learning
date: "2024-02-18T00:00:00Z"

# Optional external URL for project (replaces project detail page).
external_link: ''

image:
  caption: Schematic of TiDHy
  focal_point: Smart

links:
  # - icon: github
  #   icon_pack: fab
  #   name: TiDHy
  #   url: 
url_code: ''
url_pdf: ''
url_slides: ''
url_video: ''
---
Natural behavior and neural dynamics are often characterized by multiple latent dynamical systems that are multiscale and nonstationary, yet they can only be partially observed, making these measurements challenging to model. To understand these datasets, a common approach is to define time points as discrete, mutually exclusive states (e.g., via switching linear dynamical systems (SLDS) or clustering). However, this set of assumptions does not represent real neural and behavioral data, so there is a critical need for a computational method that can demix simultaneously evolving systems. For instance, social behaviors involve interdependent, interacting animals with behaviors that span numerous timescales simultaneously. Motivated by this need, we develop timescale demixing via hypernetworks (TiDHy) to learn from partially observed data how linear combinations of latent dynamics may evolve. TiDHy can be considered a generalization of the SLDS framework and is computed with hypernetworks, a type of neural network architecture that generates the weights of another network.
A key feature of TiDHy is that it directly learns the intrinsic timescales of the data (rather than as a hyperparameter) and demixes independent systems, yielding interpretable dynamics. Using synthetic data, we show that TiDHy can demix multiple SLDSs from partially superimposed observations, even when they span orders-of-magnitude different timescales. Additionally, we demonstrate the application of TiDHy on a real-world multi-animal tracking dataset by creating an interpretable latent structure of each animal from key-point observations and recapitulating hand-annotated behavior labels.