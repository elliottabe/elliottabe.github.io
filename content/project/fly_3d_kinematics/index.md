---
title: Whole-body 3D Kinematics of Freely Behaving Drosophila
summary: A markerless 3D pose estimation pipeline for the fruit fly — seven synchronized cameras at 800 fps, a hybrid 2D/3D deep learning model tracking 50 keypoints, and an inverse-kinematics retargeting step that produces anatomically feasible kinematic trajectories on a biomechanical body model.
tags:
  - Pose Estimation
  - Drosophila
  - Behavior
  - Deep Learning
date: '2026-05-04T00:00:00Z'

external_link: ''

image:
  caption: 3D pose tracking of freely behaving Drosophila
  focal_point: Smart

links:
  - name: Preprint
    url: https://doi.org/10.64898/2026.05.03.722293

url_code: ''
url_pdf: 'https://www.biorxiv.org/content/10.64898/2026.05.03.722293v1.full.pdf'
url_slides: ''
url_video: ''

slides: ""
---

Measuring how the brain controls movement requires watching the body move — accurately, in three dimensions, and at the timescales of real behavior. *Drosophila* is the model organism where genetic tools, connectomes, and neural-circuit knowledge converge, but its body is tiny, its limbs move fast, and self-occlusions are everywhere. To bring 3D kinematics to this system, we built a markerless pipeline (Ispizua\*, Abe\* et al., 2026[^1]) that captures whole-body fly behavior at high spatial and temporal resolution.

---

## The Pipeline

- **Seven synchronized high-speed cameras** record freely behaving flies at **800 fps**, providing the multi-view coverage needed to resolve a millimeter-scale body in motion.
- A **hybrid 2D/3D deep learning model** tracks **50 keypoints** distributed across the head, thorax, abdomen, legs, and wings.
- A **retargeting step** solves an inverse kinematics problem against a **biomechanical body model**, projecting the raw keypoints onto anatomically feasible joint trajectories. The output is not just point clouds, but kinematics consistent with the fly's actual skeleton.

This pipeline replaces brittle marker-based or 2D approaches with a 3D, biomechanically-grounded readout of fly motor behavior.

---

## What 3D Kinematics Reveal

Two findings stood out from the kinematic dataset:

- **Grounded running across the full speed range.** Flies do not switch between discrete gaits as they accelerate; instead, their leg coordination evolves continuously. The "tripod / tetrapod / wave" categorization that has dominated insect locomotion is, at best, a coarse description of an underlying continuum.
- **Multi-animal courtship coordination.** During courtship song, males coordinate **both wings** simultaneously, and modulate their **body pitch** to track the female's vertical position — a sensorimotor coupling between visual tracking and whole-body posture that is invisible to 2D approaches.

---

## A Foundation for Neuromechanical Modeling

The dataset and code are open-source. The 3D kinematics serve as the behavioral targets for our [Neuromechanical Digital Twin](../neuromechanical_digital_twin/) work — physics-based simulations of the fly trained via imitation learning to reproduce these exact trajectories. Without high-fidelity 3D kinematic ground truth, connectome-to-body models cannot be evaluated. This pipeline closes that gap.

---

[^1]: Ispizua JI\*, Abe ETT\*, Yan J, Othayoth R, Sawtelle S, Atkins F, Shiozaki HM, Meier NR, Wong J, Tran T, Mori C, Voigts J, Stern DL, Brunton BW, Tuthill JC, Johnson RE. (2026). Whole-body 3D kinematics of freely behaving *Drosophila*. *bioRxiv*. https://doi.org/10.64898/2026.05.03.722293
