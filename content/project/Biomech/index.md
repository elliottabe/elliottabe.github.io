---
title: Closed-loop connectome–body models of agile sensorimotor control
summary: This project develops closed-loop simulations of the Drosophila nervous system and body, using connectome-constrained neural models and deep reinforcement learning to study how circuit structure shapes motor control.
tags:
  - Deep Learning
  - Reinforcement Learning
date: '2024-02-18T00:00:00Z'

# Optional external URL for project (replaces project detail page).
external_link: ''

image:
  caption: MuJoCo model of fly
  focal_point: Smart

links:
url_code: ''
url_pdf: ''
url_slides: ''
url_video: ''

slides: ""
---

Understanding agile and robust motor control requires integrating knowledge of neural circuits, biomechanics, and the sensory feedback that closes the loop between perception and action. In insects like *Drosophila*, the recent availability of complete connectome datasets and detailed musculoskeletal models creates a unique opportunity to build closed-loop simulations grounded in biological reality.

This project develops physics-based models of the fly body in MuJoCo and trains neural control policies via deep reinforcement learning and imitation learning to reproduce naturalistic locomotion. By constraining these policies with connectome architecture, we can test how specific circuit motifs — such as central pattern generators and sensory feedback loops — contribute to the flexibility and robustness of walking behavior.

Key questions we address include:
- How do biomechanical constraints shape the solutions available to neural circuits?
- What is the role of sensory feedback in stabilizing and adapting locomotion?
- Can connectome-constrained models recapitulate the diversity of behavioral strategies observed in freely behaving animals?

This work connects to several collaborations including the MIMIC-MJX framework for neuromechanical emulation and the digital sphinx project, which asks whether a connectome from one organism can control the body of another — probing the limits of embodied intelligence across species boundaries.
