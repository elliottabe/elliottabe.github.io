---
title: Neuromechanical Digital Twins for Closed-Loop Sensorimotor Control
summary: Building physics-accurate digital twins of animal bodies coupled to connectome-scale neural circuit models, enabling closed-loop simulation of the full sensorimotor loop from neural circuit to body mechanics to environmental interaction.
tags:
  - Deep Learning
  - Reinforcement Learning
date: '2024-02-18T00:00:00Z'

external_link: ''

image:
  caption: Closed-loop connectome–body model architecture
  focal_point: Smart

links:
  - name: MIMIC-MJX Preprint
    url: https://doi.org/10.48550/arXiv.2511.20532
  - name: Digital Sphinx Preprint
    url: https://doi.org/10.64898/2026.03.20.713233

url_code: ''
url_pdf: ''
url_slides: ''
url_video: ''

slides: ""
---

To understand how the brain controls behavior, we need more than recordings of neurons during movement — we need models that simulate the full sensorimotor loop: from neural circuit, through body mechanics, to environmental interaction, and back. My postdoctoral work builds this infrastructure as **neuromechanical digital twins**: physics-accurate simulations of animal bodies coupled to neural control policies, and ultimately to the fly's own connectome.

The project unfolded in three stages.

---

## Stage 1 — Deep RL for Behavioral Mimicking

The starting point was a simple question: *what does it take to move like a fly?* Using deep reinforcement learning (DRL) and the MIMIC-MJX platform[^1] (Zhang, Yang, Sirbu, Abe et al., 2025), we train motor policies to imitate naturalistic fly kinematics captured via markerless pose estimation. The policy uses a variational encoder-decoder architecture[^2] to reproduce joint trajectories, leg coordination, and timing in a MuJoCo/JAX physics simulator — purely from behavioral data, with no explicit neural model.

This behavioral mimicking stage serves two purposes. First, it produces a physically grounded virtual animal whose body can be probed and perturbed in ways that complement in vivo experiments. Second, it forced us to confront the limitations of existing physics models — leading to the custom components below.

**Custom physics models developed along the way:**

- **Muscle model**: We implemented a biologically-grounded muscle actuation model replacing simple torque actuators, enabling more realistic force generation and passive dynamics.
- **Quasi-steady aerodynamics**: For flapping flight, we rewrote the aerodynamics in MuJoCo to include lift, drag, and rotational forces based on the quasi-steady model of insect flight[^3] — capturing the physics that standard rigid-body simulators miss.

{{< video src="muscles01_active.mp4" controls="yes" >}}
{{< video src="flight01.mp4" controls="yes" >}}

---

## Stage 2 — The Digital Sphinx: A Cautionary Tale

Before building a biologically meaningful connectome-body model, we needed to understand what *not* to do. In the spirit of the dead fish fMRI experiment[^4], we built a deliberate parody: the **digital sphinx**[^5] (Brunton\*, Abe\* et al., 2026).

We coupled the *C. elegans* worm connectome[^6] (302 neurons) to a MuJoCo model of the fly body[^7], routing fly proprioceptive signals to worm sensory neurons via random projection, then using DRL to train the interface. The result: **highly realistic fly walking** — indistinguishable from the real thing.

{{< video src="DigitalSphinx.mp4" controls="yes" >}}

The punchline is the point. The worm brain is 500× smaller than the fly's; fly legs alone have more motor neurons than the worm's entire nervous system. The model produced realistic locomotion because **DRL is a capable optimizer that will fit expressive networks to complex data even when the imposed constraints are outright wrong**. The worm connectome functioned as a generic recurrent neural network — a fancy reservoir. Its neural activity was cyclic and uninterpretable.

The lesson: **behavioral fidelity is not biological fidelity.** Connectome-body models are easy to overinterpret unless their components *and interfaces* are grounded in biology at every level.

---

## Stage 3 — The Full Neuromechanical System

Armed with realistic physics models and a clear understanding of what can go wrong, we are now building the biologically meaningful version: a closed-loop connectome-body model of the fly grounded in biology at the level of components, interfaces, and predictions.

{{< figure src="Neuromech.png" caption="Architecture of the closed-loop connectome–body model. Proprioceptive sensors feed into the VNC connectome (from BANC), which drives motor neurons that activate leg muscle fibers in the MuJoCo-MJX physics simulation. Descending neurons (DNs) and ascending neurons (ANs) complete the sensorimotor loop." >}}

The key architectural principles:

- **Connectome Simulations**: The ventral nerve cord (VNC) connectome from BANC[^8] provides the synaptic connectivity of the interneurons.
- **Biologically grounded interfaces**: Sensory neurons and motor neurons are identified from the connectome and mapped to specific muscles and sensors. The only learned parameters are scalar gain values between motor neurons and muscles, and sensors and sensory neurons.
- **Closed-loop feedback**: Proprioceptive signals from the physics simulation feed back into the sensory neurons in real time through neural encoding models of *Drosophila* proprioceptors, completing the neural–body–environment loop.

This design enables **circuit perturbation studies** — silencing neurons, severing connections, swapping descending commands — and directly generates testable predictions for in vivo experiments.

{{< video src="Neuromech01.mp4" controls="yes" >}}

**Key questions:**
- How does the wiring architecture of the VNC give rise to the coordination patterns of walking?
- What is the role of sensory feedback in stabilizing and adapting locomotion?
- How do descending commands from the brain modulate ongoing motor rhythms?
- What does it mean for a nervous system to be *matched* to its body?

This work represents a paradigm shift: from correlational observation of neurons during behavior, to causal, circuit-level modeling of the neural–body–environment loop — the infrastructure for a new generation of experiments on embodied intelligence.

---

[^1]: Zhang CY, Yang Y, Sirbu A, Abe ETT, et al. (2025). MIMIC-MJX: Neuromechanical Emulation of Animal Behavior. *arXiv*. https://doi.org/10.48550/arXiv.2511.20532

[^2]: Aldarondo D, Merel J, Marshall JD, et al. (2024). A virtual rodent predicts the structure of neural activity across behaviours. *Nature*, 632, 594–602. https://doi.org/10.1038/s41586-024-07633-4

[^3]: Sane SP, Dickinson MH. (2001). The control of flight force by a flapping wing: lift and drag production. *Journal of Experimental Biology*, 204, 2607–2626. https://doi.org/10.1242/jeb.204.15.2607

[^4]: Bennett CM, Baird AA, Miller MB, Wolford GL. (2009). Neural correlates of interspecies perspective taking in the post-mortem Atlantic salmon: An argument for multiple comparisons correction. *NeuroImage*, 47(Suppl 1), S125.

[^5]: Brunton BW\*, Abe ETT\*, Hu LJ, Tuthill JC. (2026). The digital sphinx: Can a worm brain control a fly body? *bioRxiv*. https://doi.org/10.64898/2026.03.20.713233

[^6]: Zhao M, Wang N, Jiang X, et al. (2024). An integrative data-driven model simulating C. elegans brain, body and environment interactions. *Nature Computational Science*, 4, 978–990. https://doi.org/10.1038/s43588-024-00738-w

[^7]: Vaxenberg R, Siwanowicz I, Merel J, et al. (2025). Whole-body physics simulation of fruit fly locomotion. *Nature*. https://doi.org/10.1038/s41586-025-08677-6

[^8]: Bates AS, Phelps JS, Kim M, Yang HH, Matsliah A, Ajabi Z, Perlman E, Delgado KM, Osman MAM, Salmon CK, Gager J, Silverman B, Renauld S, Salman F, Patel J, Collie MF, Fan J, Pacheco DA, Zhao Y, Zhang W, Serratosa Capdevila L, Roberts RJV, Munnelly EJ, Griggs N, Langley H, Moya-Llamas B, Zhang Z, Maloney RT, Yu S, Sterling AR, Sorek M, Kruk K, Serafetinidis N, Dhawan S, Klemm F, Brooks P, Lesser E, Jones JM, Pierce-Lundgren SE, Lee S, Luo Y, Cook AP, McKim TH, Giakoumas DS, Gorko B, Kophs EC, Falt T, Negron-Morales AM, Burke A, Hebditch J, Willie KP, Willie R, Popovych S, Kemnitz N, Ih D, Lee K, Lu R, Halageri A, Bae JA, Jourdan B, Schwartzman G, Demarest DD, Behnke E, Bland D, Kristiansen A, Skelton J, Stocks T, Garner D, Hernandez A, Kumar S, The BANC-FlyWire Consortium, Daly KC, Dorkenwald S, Collman F, Suver MP, Fenk LM, Pankratz MJ, Yao Z, Huston SJ, Stürner T, Jefferis GSXE, Eichler K, Seeds AM, Hampel S, Agrawal S, Okubo TS, Zandawala M, Macrina T, Adjavon DY, Funke J, Tuthill JC, Azevedo A, Seung HS, de Bivort BL, Murthy M, Drugowitsch J, Wilson RI, Lee WCA. (2026). Distributed control circuits across a brain-and-cord connectome. *bioRxiv* 2025.07.31.667571. https://doi.org/10.1101/2025.07.31.667571
