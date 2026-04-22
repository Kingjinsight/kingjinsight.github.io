---
date:  "2026-04-02"
draft: false
title: "The Limitations of Current AI: Architecture, Embodiment, and Education"
author: 'King Jin'
tags: ["AI", "brain-science", "education"]
showtoc: true
---

This post summarises a podcast discussing the limitations of current AI from multiple perspectives. [Watch the podcast](https://www.youtube.com/watch?v=-Et3GJRSI_0&t=5788s)

## I. Three Fundamental Dilemmas Facing AI (Architecture Level)

Professor Liu Jia argues that current transformer-based large models have three fundamental structural flaws compared to the human brain:

**1. Insufficient neuron complexity.** During evolution, the brain took two paths: increasing the number of neurons *and* increasing their complexity. Today's AI neurons are extremely simple — sum the inputs, pass through an activation function, done. Biological neurons, by contrast, are four-dimensional structures (three spatial dimensions + time), with their own dynamics. A single refined biological neuron has computing power equivalent to 5–8 layers of a deep neural network. Transformers have no time dimension, no partial differential equations — they are fundamentally a "2D" system.

**2. No long-range feedback connections.** Roughly 40% of the brain's connections are long-range feedback links (e.g., the frontal lobe connecting directly back to the visual cortex), used for resolving uncertainty, forming hypotheses, and enabling creativity. Transformers are purely feedforward networks — once trained, there is no feedback at all. This is precisely why their reasoning ability has a ceiling.

**3. No parallel processing capability.** The essence of a transformer is "predict the next token," which is inherently sequential. But when a human faces danger, they instantly process massive amounts of visual information in parallel — you don't analyse a flying object token by token, you just dodge. This kind of parallel perception is architecturally impossible for transformers.

---

## II. Two Core Challenges of Embodied Intelligence

**1. Perception: parallel real-time sensing (corresponding to point 3 above).** True embodied intelligence requires the ability to instantly catch a "fleeting" danger and react, as our ancestors did in the wild. This is an open-ended problem, unlike autonomous driving which operates on a closed dataset. Existing robots (including Optimus) have no real "eyes" — they are essentially pre-programmed industrial robot arms in a different shape.

**2. Motor control: the cerebellum's world model (System 1).** Of the brain's 86 billion neurons, roughly 70 billion are in the cerebellum — 6–7 times the number in the cerebral cortex. The cerebellum builds an intuitive physical world model: automatically adjusting grip force when picking up a full versus empty cup, tossing a book onto a table. These are effortless for humans but computationally extreme for robots.

Current AI addresses "System 2" (cerebral cortex — reasoning, language, mathematics) and has not touched "System 1" (cerebellum/basal ganglia — intuition, movement, perception) at all. True embodied intelligence requires **a second enlightenment grounded in neuroscience**.

---

## III. Education in the Age of AI

Liu Jia argues that today's education system — from primary school through university — was built on the first Industrial Revolution and has entirely become "false demand" in the AI era. He proposes three core directions:

**1. Emphasise the concept of "self".** The industrial age buried the self inside collective division of labour — people just had to tighten their bolts. In the AI era, one person plus ten thousand GPUs can form a one-person company. The greatest source of motivation is **one's own interests**. The core of education should be helping children discover "who am I and what do I want."

**2. Cultivate AI-native thinking.** Knowing how to use AI tools is not the same as AI-native thinking. Being AI-native is a **fundamental shift in cognitive paradigm** — treating AI as part of your body, not as a tool. Adults struggle to make this shift because of entrenched thinking patterns; children can build this mindset from scratch far more easily.

**3. Master deductive reasoning / first-principles thinking.** AI can answer any surface-level question, but finding the "logical origin" is something AI cannot do. Children must be trained to ask, before any decision: **What is my logical starting point?** This is both an anchor against getting lost in an information explosion and the root of 0-to-1 creativity.

> His closing point: **education focused on memorising knowledge has become completely worthless** (because large models make knowledge instantly accessible). The most important education going forward is teaching people **how to become themselves**.
