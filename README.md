# Machine-learned Interatomic Potential with Pytorch🧠

***What is an interatomic potential?***

Interatomic potentials (or "potentials" for short) of a system of atoms/molecules are mathematical representations of the energy stored within that system of atoms. You can imagine a simple system of atoms would look something like this:

![Untitled video - Made with Clipchamp (1)](https://github.com/user-attachments/assets/42e418b7-51c1-460e-a945-0e9c1a37c531)

Imagine if each of these atoms where small masses and they each had springs attaching to the other atoms in the system. If you were to volumetrically strain the box, then energy would become stored in the springs. The potential describes these energies with a mathematical function. 

***Project Description***

Material Scientist need some type of way to produce an interatomic potential of the alloy or element they are studying. These potentials are used as inputs into molecular dynamics simulations like Large Scale Atomic/Molecularly Massive Parallel Simulator (LAMMPS) so they study the subtle behaviors of these systems when they are subjected to things like temperature changes, stresses, and strains. Using machine learning to make accurate potentials isn't something very new. Matter of fact, it has been becoming increasingly popular over the past decade with many researchers authoring their own models and preprocessing techniques like the Behler–Parrinello approach[1] and Specral Neighbor Analysis Method(SNAP)[2]. 












References

[1]Nongnuch Artrith, Alexander Urban, An implementation of artificial neural-network potentials for atomistic materials simulations: Performance for TiO2, Computational Materials Science, Volume 114,
2016, Pages 135-150, ISSN 0927-0256, https://doi.org/10.1016/j.commatsci.2015.11.047.
(https://www.sciencedirect.com/science/article/pii/S0927025615007806)


[2] A.P. Thompson, L.P. Swiler, C.R. Trott, S.M. Foiles, G.J. Tucker, Spectral neighbor analysis method for automated generation of quantum-accurate interatomic potentials, Journal of Computational Physics,
Volume 285, 2015, Pages 316-330, ISSN 0021-9991, https://doi.org/10.1016/j.jcp.2014.12.018.
(https://www.sciencedirect.com/science/article/pii/S0021999114008353)
