## Literature module:

This module provides a way to search for scientific literature. It is designed to work with the NCBI PubMed and ARXIV databases.
You can search for articles and using free text queries as well as retriving specific articles by their identifiers. The latter is 
useful for retrieving articles that you already know about or more importantly are mentioned in the data you have retrieved using the 
apis modules. 

Articles titles and abstracts are returned as from pubmed and arxiv searches (pubmed already archives medarxiv and bioarxiv articles).
Additionally you can search for open acceess articles using openalex.org and retrieve their full text pdf files for download. 

These downloaded pdf (as well as any other local pdf that you already have) can be processed to extract the text, figures, tables from the 
downloaded documents. Using semantich chunking methods (sepearing the text into sections that convey similar topics) the text can further be
processed. Figures and tables can be automaticall interpreted using a vision language model (default is QWEN-7.5B-VL). These interpretations 
are similarly processed to the full text data. All of this can be permanantly stored in a database for later retrieval and analysis 
(more on that later, see knowledge_base module). 
