# Machine-learned Interatomic Potential with Pytorch🧠

***What is an interatomic potential?***

The interatomic potential (or "potentials" for short) of a system of atoms/molecules is a mathematical representations of the energy stored within that system of atoms. You can imagine a simple system of atoms would look something like this:

![Untitled video - Made with Clipchamp (1)](https://github.com/user-attachments/assets/42e418b7-51c1-460e-a945-0e9c1a37c531)

Imagine if each of these atoms where small masses and they each had springs attaching to the other atoms in the system. If you were to volumetrically strain the box, then energy would become stored in the springs. The potential describes these energies with a mathematical function. 

## Project Description

Material Scientist need some type of way to produce an interatomic potential of the alloy or element they are studying. Potentials can act as inputs for molecular dynamics such as Large Scale Atomic/Molecularly Massive Parallel Simulator (LAMMPS) or VASP. In doing so, we are able to study the behaviors of these systems of atoms under various conditions such as temperature changes and volumetric stresses and strains. However, the quailty of these simulations have are dependent on the quality of the interatomic potential used. Over the past two decades, machine learning has become a useful technique in producing highly accurate potentials. Some recent approaches have become increasingly popular for their accuracy and effienciency such as the Behler–Parrinello approach[1] and Specral Neighbor Analysis Method(SNAP)[2]. In this project, a pytorch neural network model is trained over a Density Functional Theory(DFT) database with two structural fingerprints embedded in the input layer for computational efficiency. 



## Codebase Breakdown
**Basic overview of code** 

Fingerprint_radial.py is a pythonic version of the fingerprint_radial.cpp file. The purpose of this transcription is to make a Pytorch implementation to reach larger audiences whole are more comfortable with machine learning in python than cpp.  
 

Each class has a single, well defined responsibility within this file. Parameters are group logically, such that all metaparameters of the network(re, rc, dr, ect.) are within RadialParameters, and all atomic system configuration characteristics (number of atoms, atom positions, etc.) are within the AtomicSystem class.   
 

**RadialParameters**

Designed for user readability. It describes the parameter types that will be saved and validated. These values will be found through the input_parser function in section XXX. 

For a given system of atoms, there exisit an equilibrium distance, re, in which a pair of atoms will stabilize at. You can think of this like two masses connected by a spring. If the spring is stretched or compressed from equilibrium point, then there will be energy stored within the spring. The radial cutoff distance, rc, is the radial distance from an atom in which neighbors outside of this region have negligible effect on the atom, and vise versa within the cutoff radius. This parameter is dictated by the specific characteristics of the atom/molecule being studied. A special cutoff radius function is implemented within the Fingerprint_radial class to account for a smooth, continuous cutoff radius description. 

  

**AtomicSystem** 

 

**Fingerprint_radial** 

 - Initiaialization 

 - Input_parser 

 - Dump_parser
   A typical dump file will have hundreds of recursive items that look something like this:

           Typical LAMMPS dump item should look like this, if not the parsing algorithms will be incorrect:

        ITEM: TIMESTEP energy, energy_weight, force_weight, nsims
        1        -199944.4130284513230436    1    1   88
        ITEM: NUMBER OF ATOMS
        52        
        ITEM: BOX BOUNDS xy xz yz pp pp pp
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

    
        """

   - The dump_parser opens all of the dump files within the folder and parses through the files to save the following data:
   - number of atoms in the simulation(in the example above, 52)
   - a vector of the coordinate positions of all atoms within that simulation snapshot(item)
   - energy for each snapshot(what the network will be predicting)
   - positions = [x0, y0, z0;
                   x1, y1, z1;
                     ...;
                     x51, y51, z51]
   - Then a distance matrix is generated that describes the radial displacement between atom i and atom j = 1 through 51. Since the displacement between i = j will always be zero(since it is the same atom), this instance is skipped. This matrix can be visualized as such, where element[i][j] indicates the euclidean distance between atom i and atom j:
  
   - 
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
