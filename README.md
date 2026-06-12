# Multi-Document Audit Pipeline

**Graph + Temporal + Semantic + LLM + Scalable Contradiction Engine + PDF Ingestion**

This pipeline ingests a folder of PDFs, extracts factual or argumentative claims via GPT, clusters them semantically, and builds a directed graph of `supports` / `contradicts` relationships. It then scores each claim using PageRank, source authority, burst detection, and lifecycle classification. Every step is checkpointed – you can stop and resume at any time.

## 🚀 Key Features

- **Multi‑PDF ingestion** – Extract text from PDFs with per‑document page ranges.
- **Claim extraction** – LLM‑based (OpenAI) extraction of atomic claims from overlapping text chunks.
- **Semantic clustering** – DBSCAN on sentence‑transformer embeddings, with deduplication of near‑duplicate claims.
- **Scalable Contradiction Engine** – Avoids O(N²) LLM calls:
  - KNN pruning (top‑k neighbours per claim)
  - Sub‑clustering (agglomerative clustering inside each DBSCAN cluster)
  - Negation pre‑screen – high similarity + negation → auto `contradicts`; high similarity + no negation → auto `supports`
  - LLM only on the remaining mid‑band pairs (batched, parallel)
  - Transitive inference – closes the graph using a 4‑rule truth table
- **Temporal analysis** – Monthly time series per cluster, Kleinberg burst detection, lifecycle classification (emerging / stable / volatile / declining).
- **PageRank** – Weighted by edge confidence and source authority.
- **Composite scoring** – Weighted combination of PageRank, source weight, burst flag, and lifecycle stage.
- **Checkpointing** – Everything saves to disk; resume from any step.
- **Neo4j support** – Optionally write the graph to a Neo4j database.

## 📁 Outputs

All outputs go into a timestamped folder under `outputs/`:


## 🛠️ Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/multi-document-audit-pipeline.git
cd multi-document-audit-pipeline

# Install dependencies
pip install openai sentence-transformers scikit-learn neo4j pymupdf python-dotenv tqdm networkx pandas numpy

# ──────────────────────────────────────────────────────────────
# ❶  SET YOUR PDF FOLDER PATH
# ──────────────────────────────────────────────────────────────
PDF_FOLDER = "path/to/folder/with/pdfs"

# ──────────────────────────────────────────────────────────────
# ❷  RUN IDENTIFIER — unique folder per run
# ──────────────────────────────────────────────────────────────
CLIENT_NAME = "Test1"

# ──────────────────────────────────────────────────────────────
# ❸  PAGE RANGES (optional – per document)
# ──────────────────────────────────────────────────────────────
PAGE_RANGES = {
    "annual_report_2024.pdf": (1, 50),   # pages 1–50 only
    "executive_summary.pdf":  None,      # full document
}

PDF Folder
    │
    ▼
┌─────────────────────────────────────────────────────────────┐
│ 1. PDF Ingestion                                            │
│    • Extract text per page (fitz)                          │
│    • Respect PAGE_RANGES                                   │
│    • Chunk with overlap (CHUNK_SIZE=500, overlap=50)       │
│    • For each chunk: call LLM to extract claims            │
└─────────────────────────────────────────────────────────────┘
    │
    ▼
┌─────────────────────────────────────────────────────────────┐
│ 2. Deduplication & Clustering                               │
│    • Encode claims with sentence‑transformer               │
│    • Deduplicate near‑duplicates (cosine ≥ 0.97)           │
│    • DBSCAN clustering on embeddings                       │
└─────────────────────────────────────────────────────────────┘
    │
    ▼
┌─────────────────────────────────────────────────────────────┐
│ 3. Scalable Contradiction Engine                            │
│    • For each cluster:                                      │
│        - Build KNN candidate pairs                          │
│        - Sub‑cluster (agglomerative) to reduce pairs       │
│        - Negation pre‑screen → auto edges                   │
│        - Send remaining pairs to LLM (batched, parallel)   │
│        - Apply transitive inference                         │
│    • Build directed graph (supports / contradicts)         │
└─────────────────────────────────────────────────────────────┘
    │
    ▼
┌─────────────────────────────────────────────────────────────┐
│ 4. Temporal Analysis                                        │
│    • Monthly claim counts per cluster                       │
│    • Kleinberg burst detection (2σ above mean)             │
│    • Lifecycle: emerging / stable / volatile / declining   │
└─────────────────────────────────────────────────────────────┘
    │
    ▼
┌─────────────────────────────────────────────────────────────┐
│ 5. Scoring                                                  │
│    • PageRank on graph (weighted by confidence)            │
│    • Composite score = w1*PageRank + w2*source_weight      │
│                         + w3*burst + w4*lifecycle          │
│    • Export results to CSV                                  │
└─────────────────────────────────────────────────────────────┘

# After configuring PDF_FOLDER and API key
results_df, edges_df, bursts, lifecycle = run_pipeline(
    pdf_folder=PDF_FOLDER,
    skip_neo4j=True,    # set False if you have Neo4j running
    use_checkpoint=True
)

results_df.sort_values("score", ascending=False).head(10)

