---
title: "Neural Network Potentials: An introduction"
excerpt_separator: "<!--more-->"
categories:
  - Article
tags:
  - Machine Learning
  - Neural Network Potential
  - DFT
  - Symmetry 
  - Electronic Structure
---

## Introduction to interatomic potentials

Atomisitic computer simulations enable investigations of various complex physical systems ranging across physics, chemistry, biochemistry and materials sciece. Central to atomistic simulations is the notion of an interatomic potential, which calulates the potential energy as a function of atomic coordinates. Historically, there have been many ways to describe the interatomic potential in order to perform molecular dynamics simulations, including: emperical potentials (analytical approximations of the interatomic potential), semi-empirical potentials (some quantum mechanical features used to form the fit a potential), ab initio (first principles) quantum mechanical based potentials and hybrid quantum/classic molecular dynamics.

Ab initio molecular dynamics (AIMD) provides many significant advantages compared to other interatomic potential calculations:

- Many more quantaties other than the energy and forces are obtained from these calculations, for example:
    - Hirshfield Charges
    - Charge density 
    - Electronic States
- Significantly more accuracy than emperical/classically based interatomic potentials
- Able to describe reactive systems and perform bond breaking/making

However, relative to other interatomic potentials AIMD is incredibly expensive, requiring the electronic structure (potential energy surface) to be recalculated at each time step. In order to obtain 1ns of simulation time, one would have to have 3-4 months of computational time. These time scales are necessary to converge statistically parameters/properties that can be classed as 'rare events'. While there are many methods designed to alleviate this issue, such as metadynamics or other enhanced sampling methods, the fundamental bottleneck of explicitly recalculating the electronic structure remains. The recent advances in the field of Artificial Intelligence has enabled reasearchers to take aim at this bottleneck and try and improve efficiency of AIMD without loss in accuracy.

## Neural Network Potentials

New methodologies utilising artificial intelligence are able to take in the coordinate file and produce the energy of the system along with the forces on each atom, without explicitly perfomring a DFT calculation (electronic structure method used for AIMD). The neural network takes in this coordinate file and creates an environmental descriptor for each atomic environment. The output of the descriptor is used as the input for a neural network which in turn ouputs atomic energies which are summed to obtain system energies. Therefore the neural network provides a map from atomic coordinates to system energy. The forces are availalbe analytically through differentiation of the network parameters, with the chain rule applied for converting from cartesian to descritor coordinates. Of course, in order for the network to perfom an accurate mapping from coordinates to energy, it must be trained and teseted first. This in turn requires a comprehensive dataset of releavant atomic configurations for the system of interst along with the DFT energy and forces. 

Many different methodologies exist to generate Neural Network Potentials. Crucial to all of these are the dataset of electronic structure caclulations and the descriptors that describe the local atomic environment. Later articles will explore these topics in more detail along with the subject at the heart of these two key components, symmetry. For the time being, it is sufficient to view the neural network as interpolating between points sampled on the potential energy surface. Therefore, sampling relevant atomic configurations is crucial to ensure reasonable interpolation occurs. Futhermore, the accuracy of the electronic structure calculation will limit the accuracy of the neural network prediction. Therefore, the higher accuracy the electronic structure method, the higher accuracy obtained for the potenial energy surface neural network predictions, meaning it is beneficial to use very expensive electronic structure methods as long as the size of the dataset required is minimal. This enables molecular dynamics at electronic structure accuracy levels not achieved before.




