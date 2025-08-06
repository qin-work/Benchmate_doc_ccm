## Sequence Module

This module is there to represent biological sequences. There are a few methods (more to come, please create an issue if you'd like to see specific things). 

The base `Sequence` class can take 4 different kinds of sequences (DNA, RNA, protein and [3di](https://github.com/steineggerlab/foldseek)) and store arbitary properties and annoations in the features property. You can read/write these to fasta files, run blast searches using NCBI's blast api calculate msas using mmseqs (this will be moved to containers module and will call that container by default in the future) and calculate embeddings using several different AI models likek ESM2/3 or nucleotide transformer (more will come, please create an issue if you would like to see more models). 

For collections of sequences there are 2 other class types, `SequenceList` and `SequenceDict`, as the name suggests there are `list` and `dict`  like instances and contain many other methods that list and dictionaries have. Please see the sequence module readme for more information and usage instructions. 
