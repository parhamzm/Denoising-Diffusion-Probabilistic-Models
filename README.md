# Denoising-Diffusion-Probabilistic-Models
"This repository is dedicated to the development of superior image synthesis outcomes, utilizing Diffusion Probabilistic Models. These constitute a class of latent variable models, which draw inspiration from considerations rooted in non-equilibrium thermodynamics. Engaging with this repository will immerse you into the intricate, yet fascinating world of employing stochastic processes to achieve high-quality image synthesis."


# Denoising Diffusion Probabilistic Models (DDPMs)

Welcome to the repository for **Denoising Diffusion Probabilistic Models (DDPMs)**, a class of generative models that have gained prominence for their ability to synthesize high-quality data, particularly in image generation tasks. This repository provides an implementation, a theoretical overview, and hands-on examples to understand, experiment with, and advance DDPM research.

---

## Table of Contents

1. [Overview](#overview)
2. [Background and Theory](#background-and-theory)
   - [Denoising Diffusion](#denoising-diffusion)
   - [Probabilistic Formulation](#probabilistic-formulation)
3. [Features](#features)
4. [Installation](#installation)
5. [Usage](#usage)
   - [Training](#training)
   - [Sampling](#sampling)
6. [Examples](#examples)
7. [Results](#results)
8. [Contributing](#contributing)
9. [License](#license)

---

## Overview

Denoising Diffusion Probabilistic Models are a novel class of generative models inspired by the process of reverse diffusion. DDPMs model the underlying data distribution by sequentially corrupting data with Gaussian noise and then learning to denoise to recover the original data. This repository implements DDPMs based on the seminal paper:

> **Denoising Diffusion Probabilistic Models** by Jonathan Ho, Ajay Jain, and Pieter Abbeel (2020).

**Core Highlights:**
- State-of-the-art generative model for high-dimensional data.
- Robust against mode collapse issues seen in GANs.
- High flexibility in architecture design and parameterization.

---

## Background and Theory

### Denoising Diffusion

Diffusion models use a two-phase process:
1. **Forward Diffusion Process**: Gradually corrupt the data with Gaussian noise over a fixed number of timesteps \( T \), making it increasingly noisy.
2. **Reverse Diffusion Process**: Learn to progressively denoise and recover the original data distribution using a neural network \( \epsilon_\theta \).

### Probabilistic Formulation

1. **Forward Process**:
   Given data \( x_0 \sim q(x_0) \), the forward process produces noisy data:

![Forward Process Equation](https://latex.codecogs.com/png.latex?q(x_t%20|%20x_{t-1})%20=%20\mathcal{N}(x_t;%20\sqrt{\alpha_t}%20x_{t-1},%20(1%20-%20\alpha_t)%20\mathbf{I}))

where \( \alpha_t \) controls the noise schedule.

2. **Reverse Process**:
The reverse process approximates the denoising via:

![Reverse Process Equation](https://latex.codecogs.com/png.latex?p_\theta(x_{t-1}%20|%20x_t)%20=%20\mathcal{N}(x_{t-1};%20\mu_\theta(x_t,%20t),%20\Sigma_\theta(x_t,%20t))).

   The reverse process approximates the denoising via:
   \[
   p_\theta(x_{t-1} | x_t) = \mathcal{N}(x_{t-1}; \mu_\theta(x_t, t), \Sigma_\theta(x_t, t)).
   \]

3. **Objective**:
   The model is trained to minimize the variational lower bound (VLB) of the data likelihood, commonly simplified to:

![Objective Equation](https://latex.codecogs.com/png.latex?\mathbb{E}_q%20\left[%20\|%20\epsilon%20-%20\epsilon_\theta(x_t,%20t)%20\|^2%20\right])

where \( \epsilon \) is the noise added in the forward process.

---

## Features

- **Modular Implementation**: Clear separation of forward and reverse diffusion processes.
- **Configurable Noise Schedules**: Support for linear, cosine, and custom schedules.
- **Flexible Architectures**: Compatible with various backbone networks (e.g., U-Net).
- **High Performance**: Optimized for efficient training and sampling.

---

## Installation

Clone the repository and install dependencies:

```bash
git clone https://github.com/username/Denoising-Diffusion-Probabilistic-Models.git
cd Denoising-Diffusion-Probabilistic-Models
pip install -r requirements.txt
