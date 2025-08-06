## Apis module:

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
