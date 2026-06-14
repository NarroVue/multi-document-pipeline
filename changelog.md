# Changelog

All notable changes to this project will be documented in this file.

The project follows the principles of [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) and documents major methodological, analytical, and architectural milestones.

---

## [0.7.0] - Research Audit Pipeline

### Added

* End-to-end reproducible narrative audit workflow.
* Structured JSON export pipeline.
* Structured CSV export pipeline.
* Dataset validation framework.
* Claim traceability system.
* Evidence mapping workflow.
* Analysis integrity checks.
* Export-ready reporting datasets.
* Methodology appendix support.

### Changed

* Standardized phase-based pipeline architecture.
* Refactored analysis workflow into discrete processing stages.
* Improved interoperability between ingestion, classification, and export components.

### Improved

* Reproducibility of analytical outputs.
* Dataset consistency validation.
* Cross-phase traceability.
* Reporting and audit readiness.

### Technical Stack

* Python
* Pandas
* Jupyter Notebook
* JSON
* CSV
* Git
* GitHub

---

## [0.6.0] - Narrative Intelligence Framework

### Added

* Narrative signal scoring framework.
* Lexical signal analysis.
* Semantic signal analysis.
* High-signal chunk detection.
* Section-level scoring.
* Narrative intensity metrics.
* Entity co-occurrence analysis.
* Narrative relationship mapping.

### Added (Experimental)

* Zero-shot Natural Language Inference (NLI).
* Contradiction detection workflows.
* Entailment scoring workflows.

### Improved

* Quantification of narrative structures.
* Detection of high-salience textual patterns.
* Cross-document semantic comparison capabilities.

### Technical Stack

* sentence-transformers
* Transformer-based NLI models
* Custom scoring framework

---

## [0.5.0] - Semantic Analysis Layer

### Added

* Named Entity Recognition (NER).
* Semantic similarity analysis.
* Embedding-based text representation.
* Topic modeling workflows.
* Entity frequency analysis.
* Entity relationship extraction.

### Changed

* Transitioned from keyword-driven analysis to semantic analysis.
* Expanded support for concept-level pattern detection.

### Improved

* Corpus-wide thematic discovery.
* Entity extraction accuracy.
* Semantic clustering capabilities.

### Technical Stack

* spaCy
* sentence-transformers
* BERTopic

---

## [0.4.0] - Document-Aware Ingestion

### Added

* Section-aware document parsing.
* Table of contents recognition.
* Page-range targeting.
* Header removal workflows.
* Footer removal workflows.
* Structural document preservation.

### Changed

* Replaced basic extraction workflow with document-aware processing.
* Expanded support for complex PDF layouts.

### Improved

* Extraction fidelity.
* Structural preservation.
* Downstream sentence segmentation quality.

### Technical Stack

* pdfplumber
* PyMuPDF (fitz)
* Custom document parsing utilities

---

## [0.3.0] - Claim Extraction Framework

### Added

* Sentence-level claim extraction.
* Claim normalization framework.
* Claim classification system.
* Claim validation workflows.
* Analytical taxonomy for policy and narrative analysis.

### Added Claim Categories

* Descriptive
* Predictive
* Causal
* Policy-Predictive
* Weakly Falsifiable
* Unfalsifiable Predictive
* Normative
* Unspecified

### Improved

* Analytical consistency.
* Claim traceability.
* Structured claim representation.

### Technical Stack

* Python
* Regular Expressions (Regex)
* Custom classification engine

---

## [0.2.0] - Structured Text Processing

### Added

* Sentence tokenization workflows.
* Corpus cleaning routines.
* Metadata preservation.
* Dataset-oriented text processing.
* Structured sentence records.

### Changed

* Transitioned from raw document processing to structured datasets.
* Introduced sentence-level analytical units.

### Improved

* Data organization.
* Corpus consistency.
* Downstream analytical flexibility.

### Technical Stack

* NLTK
* Pandas
* Python Standard Library

---

## [0.1.0] - Initial PDF Extraction

### Added

* PDF ingestion capability.
* Multi-page document processing.
* Raw text extraction.
* Initial text normalization routines.
* Basic preprocessing workflows.

### Technical Stack

* PyPDF2
* Python Standard Library

---

# Technology Stack Summary

## Core Language

* Python

## Data Processing

* Pandas
* NumPy

## Document Processing

* PyPDF2
* pdfplumber
* PyMuPDF (fitz)

## Natural Language Processing

* NLTK
* spaCy

## Semantic Analysis

* sentence-transformers
* BERTopic
* Transformer-based NLI Models

## Research Environment

* Jupyter Notebook
* Anaconda

## Version Control

* Git
* GitHub

---

# Current Capabilities

* PDF ingestion and parsing
* Document structure preservation
* Sentence extraction
* Metadata generation
* Claim extraction
* Claim classification
* Semantic similarity analysis
* Topic modeling
* Named entity recognition
* Narrative signal scoring
* Evidence mapping
* Traceability auditing
* Structured dataset exports
* Reproducible analytical workflows

---

# Planned

### Added (Planned)

* Multi-document corpus analysis
* Temporal narrative evolution tracking
* Narrative drift monitoring
* Neo4j graph integration
* Contradiction tracking across corpora
* Citation verification workflows
* Streamlit dashboard interface
* Public Comment Intelligence workflows
* Comparative Narrative Intelligence workflows
