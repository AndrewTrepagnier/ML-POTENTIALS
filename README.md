# Machine-learned Interatomic Potential with Pytorch - paused development

**What *is* an interatomic potential?**

An interatomic potential is a mathematical function that describes the energy stored within a system of atoms or molecules based on their positions. You can think of it like this:

Imagine a box filled with atoms, where each atom is connected to others by springs. If you stretch or compress the box, the springs stretch or compress too, storing energy. That stored energy is described by the interatomic potential.

Here's a helpful visualization:

![Untitled video - Made with Clipchamp (1)](https://github.com/user-attachments/assets/42e418b7-51c1-460e-a945-0e9c1a37c531)

## Project Description

Materials scientists rely on interatomic potentials to simulate the physical behavior of materials under various conditions—such as changes in temperature, pressure, or mechanical stress. These simulations are typically run using tools like LAMMPS or VASP, but the accuracy of the results is entirely dependent on the quality of the potential being used.

Traditional hand-tuned potentials often struggle to match the complexity of real-world materials. That’s where machine learning comes in.

This project uses PyTorch to build a machine-learned interatomic potential (MLIP), trained on Density Functional Theory (DFT) data. The model leverages two structural fingerprints in its input layer to maintain both efficiency and accuracy.

Notable inspirations include:

- The Behler–Parrinello Neural Network [1]
- The Spectral Neighbor Analysis Method (SNAP) [2]

## Why does it matter?

Machine-learned potentials like this one are transforming how we simulate and understand materials. By combining physics-based insight with deep learning, we can:

- Dramatically improve simulation accuracy
- Customize models for specific materials
- Enable discovery of new alloys or molecular behaviors
  
This project aims to make these advanced tools more accessible to researchers and engineers—especially those already comfortable in the Python and PyTorch ecosystems.


## Codebase Breakdown

The Tutorials folder offers the best step-by-step example of fingerprints:

```ML-POTENTIALS/Tutorials/Fingerprint_Tutorial1.ipynb```


The main goal of this codebase is to provide a clean, Pythonic implementation of the MLIP framework using PyTorch—built to be approachable by Python-based ML researchers and materials scientists.

### Fingerprint_radial.py
**RadialParameters**
This file is a full transcription of fingerprint_radial.cpp, reimagined in Python. Each class serves a single, clear purpose.

RadialParameters

This class contains all the meta-parameters needed to compute structural fingerprints:

- re: Equilibrium bond distance where atomic forces balance.
- rc: Cutoff radius—atoms beyond this distance don’t meaningfully affect a given atom.
- dr: A smoothing parameter for the cutoff function.
- These values are initialized through the input_parser() and grouped for clarity and usability.

**AtomicSystem**

Holds information about the specific atomic configuration:

Number of atoms
Atomic positions
Simulation metadata
This system’s configuration is later used to compute distance matrices and other properties needed to evaluate the potential.
  
### Dump_parser

The dump_parser() method reads LAMMPS-style dump files and extracts the data required to train the MLIP. Here's what a typical dump item looks like:

ITEM: TIMESTEP energy, energy_weight, force_weight, nsims
-        1        -199944.4130284513230436    1    1   88
-        ITEM: NUMBER OF ATOMS
-       52        
-        ITEM: BOX BOUNDS xy xz yz pp pp pp
       -6.6599068561068142     10.6426540787132993     -5.7964044747763319
       -1.5903743695984427      8.9256853388485613     -0.8635023813304824
        0.0000000000000000     16.3996700907443120     -1.5903743695984427
        ITEM: ATOMS id type x y z
        1      1          1.5004620351452496     0.5243795304393224     3.8834927664029966
        2      1         -0.4657385064656120     1.2308782860044023     7.0568980742855700
        3      1          1.2745152962579427     0.0833213387822464     9.3340024694978840
        .       .           .
        .       .           .
        .       .           .
        52     1          4.0887810494581123     5.4317594751390095    15.0272327985735377


The dump_parser opens all of the dump files within the folder and parses through the files to save the following data:
   - number of atoms in the simulation(in the example above, 52)
   - a vector of the coordinate positions of all atoms within that simulation snapshot(item)
   - energy for each snapshot(what the network will be predicting)
   - Then a distance matrix is generated that describes the radial displacement between atom i and atom j = 1 through 51. Since the displacement between i = j will always be zero(since it is the same atom), this instance is skipped. This matrix can be visualized as such, where element[i][j] indicates the euclidean distance between atom i and atom j:
  
                    atom0   atom1   atom2   ....

            atom0   i=j=None  [0][1]  [0][2] 

            atom1   [1][0]   i=j=None   [1][2]

            atom2   .           .           .
     









References

[1]Nongnuch Artrith, Alexander Urban, An implementation of artificial neural-network potentials for atomistic materials simulations: Performance for TiO2, Computational Materials Science, Volume 114,
2016, Pages 135-150, ISSN 0927-0256, https://doi.org/10.1016/j.commatsci.2015.11.047.
(https://www.sciencedirect.com/science/article/pii/S0927025615007806)


[2] A.P. Thompson, L.P. Swiler, C.R. Trott, S.M. Foiles, G.J. Tucker, Spectral neighbor analysis method for automated generation of quantum-accurate interatomic potentials, Journal of Computational Physics,
Volume 285, 2015, Pages 316-330, ISSN 0021-9991, https://doi.org/10.1016/j.jcp.2014.12.018.
(https://www.sciencedirect.com/science/article/pii/S0021999114008353)
