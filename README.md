# CCM Benchmate

**CCM Benchmate** is an open-source toolkit for integrating and analyzing biological data from diverse public resources, literature, and your own research. Designed for bioinformaticians and computational biologists, it offers modular, interoperable components to build data pipelines and accelerate discovery.

To get started, please see the [installation instructions](https://github.com/ccmbioinfo/ccm_benchmate/blob/master/INSTALLATION.md). 
Each module is independently usable and well-documented—check out the README in each module's folder for details and code examples.

## Key Features
- **Unified APIs:**: Access major bioinformatics databases (UniProt, NCBI, Ensembl, STRINGdb, and more) through a simple Python interface.
- **Literature Search & Processing**: Find, download, and extract content from scientific articles (PubMed, arXiv, OpenAlex), with tools for processing PDFs and full-text mining.
- **Container Integration**: Seamlessly run and manage Singularity/Apptainer containers locally or on HPC, with tools to convert and deploy your own environments.
- **Genome, Sequence, and Variant Handling**: Intuitive classes for genomic intervals, sequences, variants, and annotations.
- **Structure Support**: Import, analyze, or predict molecular structures using state-of-the-art models.
- **Custom Knowledge Base**: Store and query your processed data and analysis results using PostgreSQL + pgvector for advanced semantic search (coming soon).

⭐️ Work in progress! Not yet intended for production. Feedback and [contributions](https://github.com/ccmbioinfo/ccm_benchmate/blob/master/CONTRIBUTING.md) are welcome.

## Documentation

Comprehensive documentation—including module guides and usage examples—is available at:  
**[ccmbio.github.io](https://ccmbio.github.io/)**

## Modules Overview

Explore the main components (click for details):
- [APIs](https://github.com/ccmbioinfo/ccm_benchmate/tree/master/ccm_benchmate/apis): Unified interfaces for biological databases
- [Literature](https://github.com/ccmbioinfo/ccm_benchmate/tree/master/ccm_benchmate/literature): Advanced literature search and processing
- [Container Runner](https://github.com/ccmbioinfo/ccm_benchmate/tree/master/ccm_benchmate/container_runner): Manage and run containers
- [Databases](https://github.com/ccmbioinfo/ccm_benchmate/tree/master/ccm_benchmate/databases): (In development) Local and community-curated resources
- [Genome](https://github.com/ccmbioinfo/ccm_benchmate/tree/master/ccm_benchmate/genome): Genomic data structures and queries
- [Sequence](https://github.com/ccmbioinfo/ccm_benchmate/tree/master/ccm_benchmate/sequence): Sequence handling and analysis
- [Structure](https://github.com/ccmbioinfo/ccm_benchmate/tree/master/ccm_benchmate/structure): Structure loading, prediction, and analysis
- [Variant](https://github.com/ccmbioinfo/ccm_benchmate/tree/master/ccm_benchmate/variant): Variant representation and processing
- [Ranges](https://github.com/ccmbioinfo/ccm_benchmate/tree/master/ccm_benchmate/ranges): Generic and genomic intervals
- [Knowledge Base](https://github.com/ccmbioinfo/ccm_benchmate/tree/master/ccm_benchmate/knowledge_base): Store and search for your results (coming soon)

## Roadmap

Robust, searchable knowledge base for all your project data and literature
Prebuilt, ready-to-use container library for bioinformatics workflows
Unified querying and scripting across APIs
Enhanced documentation, tests, and examples
Community-driven expansion—your feedback and contributions drive our direction!

## Contributing

We welcome contributions of all kinds—code, docs, containers, and ideas.
- Bug reports or feature requests: please create an issue on the GitHub repository.
- See [CONTRIBUTING.md](https://github.com/ccmbioinfo/ccm_benchmate/blob/master/CONTRIBUTING.md) for details.

## License

[license](https://github.com/qin-work/Benchmate_doc_ccm/blob/main/LICENSE)
