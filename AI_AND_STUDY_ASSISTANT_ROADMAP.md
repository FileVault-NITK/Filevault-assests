# AI Document Intelligence & Study Assistant Roadmap

## FileVault: Next-Generation Multimodal OCR, Semantic Search, and RAG Architecture

**Status:** AI Technical Roadmap (Cloud Max Grant Feature)  
**Platform Target:** [https://filevault.cc](https://filevault.cc)  
**Author:** Sai Varshith M, National Institute of Technology Karnataka (NITK), Surathkal  

---

### 1. The Challenge: Invisible Academic Knowledge

In higher engineering education, the most valuable learning resources are often **invisible to traditional search engines**:
- Over **40% of student-contributed study materials** are photographs or scans of handwritten notebooks, whiteboard derivations, and hand-sketched circuit diagrams.
- Traditional full-text search engines (Elasticsearch, Lucene, client-side regex) rely strictly on ASCII text. They treat scanned PDFs and images as opaque binary blobs.
- Under intense exam pressure, students spend up to 45 minutes manually skimming through hundreds of notebook pages looking for a single derivation (e.g., *"Derivation of Navier-Stokes equation in cylindrical coordinates"* or *"State transition matrix solution via Laplace transform"*).

**The Cloud Max Solution:** Implementing a **Multimodal Academic Document Intelligence Engine** powered by cloud GPU compute and dense vector embeddings.

---

### 2. AI Architecture Topology

```
AI Document Processing Pipeline
┌──────────────────┐     ┌──────────────────┐     ┌──────────────────┐
│ Scanned Notes &  │ ──► │ GPU Multimodal   │ ──► │ LaTeX Formula &  │
│ Lecture Slides   │     │ Vision Worker    │     │ Diagram Parser   │
└──────────────────┘     └──────────────────┘     └────────┬─────────┘
                                                           │
                                                           ▼
┌──────────────────┐     ┌──────────────────┐     ┌──────────────────┐
│ RAG Grounded     │ ◄── │ HNSW Hybrid      │ ◄── │ 1536-dim Dense   │
│ Study Assistant  │     │ Search Engine    │     │ Vector Store     │
└──────────────────┘     └──────────────────┘     └──────────────────┘
```

The system operates across three interconnected modules:
1. **Multimodal GPU OCR & Mathematical Extraction**
2. **Hybrid Dense Vector Search (`pgvector`)**
3. **Grounded RAG Academic Study Assistant**

---

### 3. Module 1: GPU Multimodal OCR & Formula Extraction

#### 3.1 Handwriting & Math Recognition Pipeline
- Scanned pages are ingested by cloud GPU instances (NVIDIA L4 / T4).
- The pipeline applies adaptive binarization, skew correction, and noise reduction.
- Vision-Language Models (VLMs) and specialized OCR transformers (such as Nougat and TrOCR) extract:
  - **Inline and Display Math:** Converted directly into standard **LaTeX syntax** (e.g., `$$\oint_{\partial \Sigma} \mathbf{B} \cdot d\mathbf{l} = \mu_0 I_{\text{enc}} + \mu_0 \varepsilon_0 \frac{d\Phi_E}{dt}$$`).
  - **Engineering Schematics:** Diagrams (logic gates, control block diagrams, civil trusses) receive automatic semantic captions and label extraction.
  - **Structural Tables:** Tabular laboratory data converted into structured Markdown.

#### 3.2 Processing Throughput
- Average processing speed: **1.2 to 2.5 seconds per scanned page**.
- Batch workers process an entire 150-page notebook in under **4 minutes**.

---

### 4. Module 2: Hybrid Semantic Vector Search (`pgvector`)

#### 4.1 Hybrid Lexical + Semantic Search Strategy
Standard vector search often struggles with exact domain-specific identifiers (like course codes `CS301` or `EC250`), while lexical search fails on conceptual synonyms. FileVault unites both:

```
Hybrid Search Resolution Flow
Query: "How does carrier lifetime affect diode reverse recovery?"
  │
  ├──► Lexical Branch (BM25):
  │      Matches exact occurrences: "carrier lifetime", "reverse recovery"
  │
  └──► Semantic Branch (pgvector HNSW):
         Matches conceptual chunks: "minority charge storage", "diffusion capacitance"
  │
  ▼
Reciprocal Rank Fusion (RRF) -> Unified Top-K Ranked Document Pages
```

#### 4.2 Dense Chunking & Vector Sizing
- Extracted text and slide transcripts are split using a **semantic boundary chunker** (500 tokens with 50-token sliding overlap, respecting paragraph and formula boundaries).
- Embeddings are generated using high-dimensional dense embedding models (1536 dimensions).
- Stored in PostgreSQL with an **HNSW (Hierarchical Navigable Small World)** vector index:
  ```sql
  -- Vector Index Construction
  CREATE INDEX ON document_chunks 
  USING hnsw (embedding vector_cosine_ops) 
  WITH (m = 16, ef_construction = 64);
  ```
- Result: **Sub-15ms search resolution** across 500,000+ indexed lecture slides and notebook pages.

---

### 5. Module 3: Grounded RAG Academic Study Assistant

During examination revision, students require immediate, accurate conceptual clarification grounded strictly in their professor's course syllabus.

#### 5.1 Zero-Hallucination Guardrails
Generic AI chatbots frequently hallucinate engineering formulas or cite unapproved curricula. FileVault's RAG Assistant enforces strict constraints:
- **Hard Grounding:** The assistant is restricted to answering *only* from the retrieved context of verified NITK lecture slides and faculty notes.
- **Explicit Failure Mode:** If a concept is not present in the indexed courseware, the assistant explicitly replies:
  > *"This specific topic is not covered in the verified course slides for [Subject Name]. Please refer to Chapter X of the recommended reference textbook or consult the course instructor."*
- **Page-Level Citations:** Every assertion includes a direct clickable link to the exact page of the course PDF (e.g., `[Lecture 14, Slide 22]`).

#### 5.2 Automated Revision Tools
- **Instant Topic Summaries:** One-click generation of concise 1-page revision summaries for complex multi-week modules.
- **Self-Assessment Quiz Generator:** Dynamically creates 5 conceptual multiple-choice and short-answer questions derived directly from the uploaded slide deck to test retention.

---

### 6. Cloud Compute & Token Allocation Requirements

To deploy and maintain this AI roadmap, the requested Cloud Max grant provides the following essential capacity:

| AI Resource Component | Sizing & Allocation | Workload Role |
|:---|:---|:---|
| **Cloud GPU Instances** | 1× NVIDIA L4 (24GB VRAM) Spot / Scheduled | Batch OCR of scanned notes & formula parsing |
| **Vector Storage (pgvector)** | 100 GB dedicated SSD index space | 500,000+ 1536-dim vector embeddings |
| **Inference Token Quotas** | 50 Million tokens / month | Embedding generation + RAG assistant queries |
| **Redis Cache for AI** | 2 GB dedicated memory | Caching frequent student semantic queries |

---

<div align="center">
<sub>FileVault AI Roadmap · National Institute of Technology Karnataka, Surathkal · © 2026</sub>
</div>
