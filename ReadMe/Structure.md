---
layout: default
title: Structure
---

## Structure Module

Similar to sequence module, the main goal is to store sequences and related information as well as some basic calculations related to biological structures. 

The base `Structure` class can take a pbd file and load its structure. It can extract the sequence of the structure, calculate embeddings using ESM3, calculate solvent accesible surface area, get its 3Di sequence (see above), align it to another `Structure` instance and write to results to a pdb file. Still under construction, you can also predict a structure using one of (OmegaFold, Alphafold2, AlphaFold3-you need to get your own weights due to licensing requirements, Boltz1 and Boltz2). These will be calls to the `ContainerRunner` module and results will be saved to disk. 

There is also a `StructureComplex` instance and as the name suggests this is there to represent complexes. These can be multiple proteins, or a protein+ligand, DNA/RNA/Protein complexes. Similar to the `Structure` instance we are working on creating `ContainerRunner` calls to predict arbitrary structure complexes using AlphaFold2/3 and Boltz1/2. 

Additionally we are working on creating a `Simulation` class to sample protein structure fluctiations either via [Openmm](https://openmm.org/) (very computationally intensive, but accurate and time resolved), [BioEmu](https://github.com/microsoft/bioemu) and [AlphaFlow](https://github.com/bjing2016/alphaflow). These again will be calls to `ContainerRunner` calls, which means if you have other calculations that will utilize these containers for arbitrary outputs. 


## Classes Overview

- `Structure`: Main class for handling individual protein structures
- `ProteinComplex`: Class for working with multi-chain protein structures (not yet fully implemented)

## Structure Class

### Basic Usage

```python
from ccm_benchmate.structure.structure import Structure

# Create from PDB file
structure = Structure(pdb="/path/to/structure.pdb")

# Create from sequence and predict structure
structure = Structure(
    sequence="MKLLPRGPAAAAAAVLLLLSLLLLPQVQA",
    predict=True,
    model="AF3"  # Currently only AlphaFold3 supported
)

# Download structure from PDB/AlphaFold DB
structure.download(
    id="1ABC",           # PDB or UniProt ID
    source="PDB",        # "PDB" or "AFDB" 
    destination="/path/", # Output directory
    load_after_download=True
)
```

### Structure Analysis

```python
# Calculate solvent accessible surface area (SASA)
structure.calculate_sasa()

# Get 3D structure embeddings
structure.calculate_embeddings(
    model="esm3",     # Currently only ESM3 supported
    normalize=False
)

# Get 3Di sequence encoding
structure.get_3di()

# Get amino acid sequence
sequence = structure.get_sequence()

# Align with another structure
other_structure = Structure(pdb="/path/to/other.pdb")
aligned_pdb, rotation_file, html_report = structure.align(
    other=other_structure,
    destination="/path/for/output/"
)
```

### Structure Prediction

```python
# Predict structure using AlphaFold3
predicted = structure.predict(
    output_path="/path/for/output/",
    container="af3_container",    # Container with AF3 
    inference=True,
    pipeline=False,
    model="AF3"                   # Currently only AF3 supported
)
```

### File Operations

```python
# Write structure to PDB file
structure.write("/path/to/output.pdb")
```

## Key Features

### Structure Operations
- Load structures from PDB files
- Download structures from PDB/AlphaFold DB
- Structure prediction with AlphaFold3
- Calculate SASA
- Generate structure embeddings
- Get 3Di sequence encoding
- Structure alignment
- Import/export PDB files

### Supported Sources
- PDB database
- AlphaFold DB
- Local PDB files

### Analysis Types
- SASA calculation
- ESM3 structure embeddings
- 3Di sequence encoding
- Structure alignment with MUSTANG

Currently, we are refactoring our code to run structure prediction via `ContainerRunner` class to increase the flexibility and
remove unecessary dependencies that might cause conflicts later in development. 

