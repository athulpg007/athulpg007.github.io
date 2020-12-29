---
layout : default
title : Software and Tutorials
---

# Software and Tutorials

I provide here a brief summary of software I have developed and some programming tutorials. I know I will need to do these agaain at some point in the future, so I decided to document them here so it helps other who run into the same problems as well.

# Aerocapture Mission Analysis Tool (AMAT)

**AMAT** is an open source collection of Python subroutines for mission design and analysis
of aerocapture mission concepts.

<center><img src="/software/AMAT_logo_cropped.png" alt="Artist's illustration of an Orion-derived aeroshell performing aerocapture at Venus. Surface color is false color from Magellan data." width="500"/></center> 
Artist's illustration of an Orion-derived aeroshell performing aerocapture at Venus. Surface color is false color from Magellan data.

AMAT comes with a suite of tools to allow end-to-end conceptual design of aerocapture missions: launch vehicle performance calculator, extensive database of interplanetary trajectories, atmosphere models, guidance schemes, and aeroheating models. AMAT supports analysis for Venus, Earth, Mars, Titan, Uranus, and Neptune for both lift and drag modulation control techniques.

<center><img src="/software/planets.png" alt="AMAT supported planetary destinations across the Solar System" width="500"/></center> 
AMAT supported planetary destinations across the Solar System


AMAT has been extensively used in various aerocapture mission studies at the [Advanced Astrodynamics Concepts (AAC)](https://engineering.purdue.edu/AAC/) research group at Purdue University in active collaboration with the NASA Jet Propulsion Laboratory (JPL). 

To learn more about getting started with AMAT and installation instructions, please refer to the [AMAT documentation](https://amat.readthedocs.io). The stable version of the source code is available on [GitHub](https://github.com/athulpg007/AMAT).  

# Tutorials

## [Deploying Jupyter Notebooks on AWS EC2](jupyter-aws)

Jupyter Notebooks are very popular in the scientific programming community due to their ability to integrate code, equations, visualizations, and narrative text all into one interactive document. When running a Jupyter Notebook on a local machine, we are limited by the memory and computing power available on the laptop or desktop computer.  Amazon Web Services (AWS) Elastic Compute Cloud (EC2) provides on-demand, reliable, scalable, and inexpensive cloud computing services. This step-by-step tutorial will guide you to deploy Jupyter notebooks on an EC2 instance, providing you with the ability to combine the interactive functionality of Jupyter notebooks with the easily scalable computing capabilities offered by EC2. This is especially useful for high-perfomance computing and deep learning problems which can leverage parallel processing and GPU computing architectures provided by EC2 to run these codes much faster than on your local machine, while still being able to interactively change your code and visualize the results using Jupyter notebooks.







