## Structure Module

Similar to sequence module, the main goal is to store sequences and related information as well as some basic calculations related to biological structures. 

The base `Structure` class can take a pbd file and load its structure. It can extract the sequence of the structure, calculate embeddings using ESM3, calculate solvent accesible surface area, get its 3Di sequence (see above), align it to another `Structure` instance and write to results to a pdb file. Still under construction, you can also predict a structure using one of (OmegaFold, Alphafold2, AlphaFold3-you need to get your own weights due to licensing requirements, Boltz1 and Boltz2). These will be calls to the `ContainerRunner` module and results will be saved to disk. 

There is also a `StructureComplex` instance and as the name suggests this is there to represent complexes. These can be multiple proteins, or a protein+ligand, DNA/RNA/Protein complexes. Similar to the `Structure` instance we are working on creating `ContainerRunner` calls to predict arbitrary structure complexes using AlphaFold2/3 and Boltz1/2. 

Additionally we are working on creating a `Simulation` class to sample protein structure fluctiations either via [Openmm](https://openmm.org/) (very computationally intensive, but accurate and time resolved), [BioEmu](https://github.com/microsoft/bioemu) and [AlphaFlow](https://github.com/bjing2016/alphaflow). These again will be calls to `ContainerRunner` calls, which means if you have other calculations that will utilize these containers for arbitrary outputs. 
