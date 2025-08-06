## Genome Module

While it is possible to use the ensembl api class to query genomic ranges and intervals for instances where you are interested in only one genome (and its annotatoins) for the whole project and you will need to make repeated queries it would be more performant (and nicer to ther people using the ensembl api) to generate a data structure that can represent genomic/proteomic information. 

This is were the genom module comes into play. The genome.genome.Genome class takes a genome fasta file and a gtf fjile and creates a database of genomic regions. These regions can then be queried by genes, transcripts, exons, cdss, introns and utrs depending on the avalibility of these annotation types in the gtf file. You can also extract sequences from the genome fasta file for any arbitrary genome interval (see Ranges and GenomicRanges below) as well as providing (or generating) transcritome and proteome fasta files. 

The genome module also suspports saving these results to an arbitrary database, whether this is your knowledge base or any other kind of SQL databse (could even be in-memory sqlite). Each genome instance can be created and stored independently so if your analysis/project requires multiple genomes (or multiple annotations of the same fasta file, these are treated as different genomes). There is also support for that. 

Finally for your own work you can add arbitrary annotations to each of the tables in `JSON` format and then query them later. 
