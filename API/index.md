---
layout: default
title: API
---

# API

## Apis module:

## Goal:
The goal of the module is to provide a unified(-ish) interface to different biological databases.

## Quick Links
- [Databases](#Databases)
- [Usage](#usage):

| Class                | Status   | Data Type              |
|----------------------|----------|-------------------------|
| [ensembl.Ensembl](#ensembl.Ensembl)    | ✅ Stable | Genomic data           |
| [uniprot.Uniprot](#uniprot.Uniprot)   | ✅ Stable | Protein data           |
| [stringdb.Stringdb](#stringdb.Stringdb)      | ✅ Stable | PPI networks           |
| [others.GTEX](#others.GTEX)      | 🚧 Beta  | Expression data        |
| [others.BioGrid](#others.BioGrid)    | ✅ Stable | Interactions           |
| [others.Intact](#others.Intact)   | ✅ Stable | Molecular interactions |
| [reactome.Reactome](#reactome.Reactome)   | ✅ Stable | Pathways               |
| [rna.RNACentral](#rna.RNACentral) | ✅ Stable | Non-coding RNA         |

## Databases
The module interfaces with the following public databases:

[UniProt](https://www.uniprot.org/): A comprehensive resource for protein sequences and annotations. This module allows users to search the full UniProt database, including variation isoforms and mutagenesis endpoints. Retrieved information is integrated into a unified dictionary format for easy programmatic access.

[NCBI](https://www.ncbi.nlm.nih.gov/): A suite of databases covering nucleotide sequences, protein sequences, gene annotations, and more. This module enables queries across all NCBI databases. While PubMed can be accessed through this module, we recommend using the dedicated literature module for more effective literature queries (see below).

[Ensembl](https://www.ensembl.org/): A resource for genomic sequences and annotations. This module supports searching gene variants, mapping coordinates across assemblies, annotating variants, retrieving gene details, and accessing cross-references across databases.

[STRINGdb](https://string-db.org/): A database of known and predicted protein-protein interactions. This module allows querying interaction data between proteins. Similar functionality is available through the BioGRID and IntAct endpoints in the others module.

[RNAcentral](https://rnacentral.org/): For RNA-related data, the RNACentral module provides access to RNA sequences and their associated annotations.

# Usage

This module defines the API classes used in the ccm_demo application. Each class is designed to handle a specific type of request and return the corresponding response. These APIs are intended for users who have a clear understanding of their data needs and wish to programmatically link various public databases. Each API returns a dictionary, though the structure and parsing logic may vary across classes. The available API classes are:

The apis marked with (WIP) are still under development and may not be fully functional yet.

+ Ensembl
+ Uniprot
+ NCBI E utils
+ Reactome
+ stringdb
+ Intact
+ RNAcentral
+ Rfam (WIP)
+ GTEx (WIP)
+ EBI tools (requires testing)
+ BioGrid
---

## ensembl.Ensembl

**Description:**  
Client for the Ensembl REST API. Supports gene, variant, phenotype, sequence, mapping, and overlap queries.

**Usage Examples:**
```python
from ccm_benchmate.apis.ensembl import Ensembl
from ccm_benchmate.ranges.genomicranges import GenomicRange

ensembl = Ensembl()

# Variation info
info = ensembl.variation("rs56116432")
info_translated = ensembl.variation("rs56116432", method="translate")
info_pub = ensembl.variation("26318936", method="publication", pubtype="pubmed")

# VEP (requires Variant class)
# myvar = Variant(1, 6524705, 6524705, "C", "T")
# vep_info = ensembl.vep(myvar, check_exists=True)

# Phenotype
grange = GenomicRange(9, 22125503, 22125502, "+")
phenotypes = ensembl.phenotype(grange)

# Sequence
seq = ensembl.sequence("ENSG00000139618")

# Overlap
features = ["gene", "transcript", "cds", "exon", "repeat"]
overlap = ensembl.overlap(grange, features)

# Xrefs
xrefs = ensembl.xrefs("ENSG00000139618")

# Mapping
mapping = ensembl.mapping("ENSP00000288602", 100, 300)

# Info
info = ensembl.info()
```

---

## uniprot.Uniprot

**Description:**  
Client for the UniProt API. Retrieves protein information, mutagenesis data, isoforms, and protein-protein interactions.

**Usage Examples:**
```python
from ccm_benchmate.apis.uniprot import Uniprot

uniprot = Uniprot()

# Get protein info
protein_info = uniprot.get_protein("P38398")

# Mutagenesis
mutagenesis = uniprot.get_mutagenesis("P38398")

# Isoforms
isoforms = uniprot.get_isoforms("P38398")

# Interactions
interactions = uniprot.get_interactions("P38398")
```

---

## others.GTEX

**Description:**  
Client for the GTEx Portal API. Supports querying eQTL, sQTL, and iQTL associations for genes and tissues.

**Usage Examples:**
```python
from ccm_benchmate.apis.others import GTEX

gtex = GTEX()

# Individual-level eQTLs
ieqtl_results = gtex.ieqtl(gene="ENSG00000139618", tissue="Liver", dataset="GTEx_Analysis_v8_eQTL")

# Individual-level sQTLs
isqtl_results = gtex.isqtl(gene="ENSG00000139618", tissue="Liver", dataset="GTEx_Analysis_v8_sQTL")
```

---

## others.BioGrid

**Description:**  
Client for the BioGRID API. Retrieves molecular interaction data, evidence types, organisms, and supported identifiers.

**Usage Examples:**
```python
from ccm_benchmate.apis.others import BioGrid

biogrid = BioGrid(access_key="YOUR_BIOGRID_KEY")

# Interactions
interactions_df = biogrid.interactions(
    gene_list=["TP53", "BRCA1"],
    id_types=["entrez"],
    evidence_types=["physical"]
)

# Evidence types
evidence_types = biogrid._get_evidence_types()

# Organisms
organisms = biogrid._get_organisms()

# Supported identifiers
id_types = biogrid._get_supported_identifiers()
```

---

## others.Intact

**Description:**  
Client for the IntAct molecular interaction database. Fetches protein-protein interactions using EBI IDs.

**Usage Examples:**
```python
from ccm_benchmate.apis.others import Intact

intact = Intact()

# Search for interactions by EBI ID
interactions, last_page = intact._search("EBI-123456")

# Retrieve all interactions for a given interactor (requires intact.interactions to be set)
# all_interactions_df = intact.intact_search(page=0, page_size=1000)
```

---

## reactome.Reactome

**Description:**  
Client for the Reactome API. Accesses pathway and reaction data for genes and proteins.

**Usage Examples:**
```python
from ccm_benchmate.apis.reactome import Reactome

reactome = Reactome()

# Get pathways for a gene
pathways = reactome.get_pathways("TP53")
```

---

## rna.RNACentral

**Description:**  
Client for the RNAcentral API. Retrieves non-coding RNA information and cross-references.

**Usage Examples:**

```python
from ccm_benchmate.apis.rnacentral import RNACentral

rna_central = RNACentral()

# Get RNA info
rna_info = rna_central.get_rna("URS000075C6A6")
```

---

## stringdb.Stringdb

**Description:**  
Client for the STRING database API. Fetches protein-protein interaction networks and functional enrichment data.

**Usage Examples:**
```python
from ccm_benchmate.apis.stringdb import Stringdb

stringdb = Stringdb()

# Get interaction network
network = stringdb.get_network("9606.ENSP00000354587")
```

---

**Note:**  
Replace example IDs and access keys with valid values. Refer to each class's docstrings for more details on available methods and parameters.
