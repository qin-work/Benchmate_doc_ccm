## Apis module:

## Quick Links
- [Goal](#Goal)
- [Usage](#usage):
| Database   | Class                | Status   | Data Type              |
|------------|----------------------|----------|-------------------------|
| Ensembl    | ensembl.Ensembl      | ✅ Stable | Genomic data           |
| UniProt    | uniprot.Uniprot      | ✅ Stable | Protein data           |
| STRING     | stringdb.Stringdb    | ✅ Stable | PPI networks           |
| GTEx       | others.GTEX          | 🚧 Beta  | Expression data        |
| BioGRID    | others.BioGrid       | ✅ Stable | Interactions           |
| IntAct     | others.Intact        | ✅ Stable | Molecular interactions |
| Reactome   | reactome.Reactome    | ✅ Stable | Pathways               |
| RNAcentral | rna.RNACentral       | ✅ Stable | Non-coding RNA         |

| Database   | Class                | Status   | Data Type              |
|------------|----------------------|----------|-------------------------|
| [ensembl.Ensembl](#ensembl.Ensembl)    | ensembl.Ensembl      | ✅ Stable | Genomic data           |
| [uniprot.Uniprot](#uniprot.Uniprot)   | uniprot.Uniprot      | ✅ Stable | Protein data           |
| [stringdb.Stringdb](#stringdb.Stringdb)     | stringdb.Stringdb    | ✅ Stable | PPI networks           |
| [others.GTEX](#others.GTEX)      | others.GTEX          | 🚧 Beta  | Expression data        |
| [others.BioGrid](#others.BioGrid)    | others.BioGrid       | ✅ Stable | Interactions           |
| [others.Intact](#others.Intact)   | others.Intact        | ✅ Stable | Molecular interactions |
| [reactome.Reactome](#reactome.Reactome)   | reactome.Reactome    | ✅ Stable | Pathways               |
| [rna.RNACentral](#rna.RNACentral) | rna.RNACentral       | ✅ Stable | Non-coding RNA         |


## Goal
The goal of the module is to provide a unified(-ish) interface to different biological databases. The module has interfaces
the following databases:

+ uniprot.org: This is a database of protein sequences and annotations. The module provides a way to search for proteins
and their respective annotations. The entirety of the uniprot database can be searched using the module, including variation
isoforms and mutagenesis endpoints. These are then integrated into a single dictionary that can be used to access the data.
+ ncbi.nlm.nih.gov: This is a database of nucleotide sequences and annotations. The module provides a way to search for all 
of the ncbi databases, including nucleotide sequences, protein sequences, gene annotations, and more. While you can search pubmed
using this module, the literature module is better suited for that purpose (see below). 
+ ensembl.org: This is a database of genomic sequences and annotations. The module provides a way to search for gene variants
mapping between different coordinates systems, and more. The module also provides a way to search for genes and their annotations,
annotate variants, query cross references from different databases and more. 
+ stringdb.org: This is a database of protein-protein interactions. The module provides a way to search for protein-protein interactions. 
Additionally you can use the biogrid and IntAct endpoints under others to perform similar queries.
+ For information on RNA the RNACentral module provides a way to search for RNA sequences and annotations. 

You can see a detailed overview of how these can be used in the readme file under ccm_benchmate/apis/README.md.

We are currently working on adding more databases to this module, if you have suggestions for databases that you would like to see
please open an issue on the GitHub repository and we will try to add them.

We are also working on a databses module that will provide a way to retrieve data from smaller platforms such as GTEx where the whole 
database is downloaded ahead of time in a read-only folder. 

from PIL.features import featuresfrom PIL.features import featuresfrom sympy.physics.units.definitions.dimension_definitions import information

# Usage

This module includes the API classes for the ccm_demo application. Each API class is responsible for 
handling a specific type of request and returning the appropriate response. The classes assume that you know what you are
looking for and gives you the power to link different public databases to each other programmatically. Each of the apis
return a dictionary with varying degrees and the parsing also is different. The API classes are as follows:

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


Here is a `README.md` for the classes under `ccm_benchmate/apis`. Each section describes the class and provides usage examples for each public method.

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
