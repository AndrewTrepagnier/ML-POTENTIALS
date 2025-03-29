# Machine-learned Interatomic Potential with Pytorch🧠

***What is an interatomic potential?***

Interatomic potentials (or "potentials" for short) of a system of atoms/molecules are mathematical representations of the energy stored within that system of atoms. You can imagine a simple system of atoms would look something like this:

Imagine if each of these atoms where small masses and they each had springs attaching to the other atoms in the system. If you were to volumetrically strain the box, then energy would become stored in the springs. The potential describes these energies with a mathematical function. 

***Project Description***

Material Scientist need some type of way to produce an interatomic potential of the alloy or element they are studying. These potentials are used as inputs into molecular dynamics simulations like Large Scale Atomic/Molecularly Massive Parallel Simulator (LAMMPS) so they study the subtle behaviors of these systems when they are subjected to things like temperature changes, stresses, and strains. Using machine learning to make accurate potentials isn't something very new. Matter of fact, it has been done for decades and has been authored in nuemerous published research journals[1][2][3]. 

