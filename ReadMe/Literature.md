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


# Literature Module

A module for searching and processing scientific literature from PubMed and arXiv, with functionality to download papers, extract content, and analyze metadata.

## Classes Overview

- `LitSearch`: Search for papers across scientific databases
- `Paper`: Download and process individual papers, extracting text, figures, and tables

## LitSearch

The `LitSearch` class provides methods to search PubMed and arXiv databases.

### Usage

```python
from ccm_demo.literature.literature import LitSearch

# Initialize searcher (optional PubMed API key)
searcher = LitSearch(pubmed_api_key="your_api_key")  # API key optional

# Search PubMed
pubmed_ids = searcher.search(
    query="BRCA1 breast cancer",
    database="pubmed",
    results="id",     # Return PMIDs
    max_results=1000  # Max number of results to return
)

# Search with DOIs
dois = searcher.search(
    query="BRCA1 breast cancer", 
    database="pubmed",
    results="doi"     # Return DOIs instead of PMIDs
)

# Search arXiv
arxiv_ids = searcher.search(
    query="machine learning genomics",
    database="arxiv"
)
```

## Paper

The `Paper` class handles downloading and processing individual papers.

### Usage

```python
from ccm_demo.literature.literature import Paper

# Initialize from PubMed ID
paper = Paper(
    paper_id="12345678",
    id_type="pubmed",
    citations=True,      # Get citation data
    references=True,     # Get reference data
    related_works=True   # Get related papers
)

# Initialize from arXiv ID 
paper = Paper(
    paper_id="2101.12345",
    id_type="arxiv"
)

# Initialize from local PDF file
paper = Paper(
    paper_id=None,
    filepath="/path/to/paper.pdf"
)

# Get paper abstract
abstract = paper.get_abstract()

# Download PDF
pdf_path = paper.download(destination="/downloads/")

# Process paper content
paper.process()  # Extracts text, figures, tables

# Access processed content
print(paper.text)              # Full text
print(paper.figures)           # Extracted figures
print(paper.tables)            # Extracted tables
print(paper.paper_info)        # Metadata from OpenAlex
```

## Key Features

### Paper Search
- Search PubMed and arXiv databases
- Return paper IDs or DOIs
- Configurable result limits

### Paper Processing
- Download PDFs from open access sources
- Extract paper abstract
- Extract full text content
- Extract figures and tables
- Get paper metadata (title, authors, etc.)
- Get citation data
- Get reference data
- Get related works
- Generate embeddings from chunked full text
- Generate embeddings from figures and tables
- Generate figure interpretation text using vision language models

## Notes

- Requires an active internet connection for searching and downloading
- Some features require paper IDs and won't work with local PDFs only
- PDF processing requires local storage for downloaded files
- Citations, references, and related works data comes from OpenAlex
- Not all papers may be available for download (depends on open access status and whether there is a direct pdf link)
