# Claude Max Specifications & Workload Architecture

## FileVault: Enterprise Sizing, Claude AI Integration, and Capacity Specifications

**Document Status:** Production Technical Specification  
**Associated Blueprint:** `assets/diagrams/cloud-infrastructure-topology.svg`  
**Platform Target:** [https://filevault.cc](https://filevault.cc)  
**Lead Architect:** Sai Varshith M, National Institute of Technology Karnataka (NITK), Surathkal  

---

### 1. Overview & Claude Max Integration

<div align="center">
  <img src="assets/diagrams/cloud-infrastructure-topology.svg" alt="Claude Max Infrastructure Topology" width="100%"/>
</div>

This document details the **Claude Max Specifications** designed to scale FileVault ([filevault.cc](https://filevault.cc)) across 15,000+ engineering students at NITK Surathkal and sister technical institutions. It outlines the AI processing workload, multimodal vision pipelines, token throughput modeling, context window utilization, and infrastructure sizing.

---

### 2. Workload & Traffic Modeling

Academic traffic follows a highly distinct seasonal pattern compared to standard SaaS products:

```
Traffic Demand Profiles: Regular vs. Peak Exam Surges
┌──────────────────────────────────────┬───────────────────────┬──────────────────────────┐
│ Parameter                            │ Regular Semester Mode │ Peak Examination Mode    │
├──────────────────────────────────────┼───────────────────────┼──────────────────────────┤
│ Daily Active Users (DAU)             │ 1,500 – 2,500         │ 10,000 – 18,000          │
│ Peak Concurrent Requests             │ 300 req/sec           │ 4,500 req/sec            │
│ Daily Transferred Egress             │ 80 GB – 150 GB        │ 1.2 TB – 2.8 TB / day    │
│ Average Request Latency Target       │ &lt; 50ms               │ &lt; 80ms under 10× surge │
│ Claude AI Queries (Daily)            │ 2,000 queries         │ 35,000+ queries / day    │
│ File Stream Concurrency (PDF/Video)  │ 120 streams           │ 2,500+ streams           │
└──────────────────────────────────────┴───────────────────────┴──────────────────────────┘
```

#### Peak Exam Surge Dynamics:
During the two-week mid-term and three-week end-term examination windows, student queries surge by **600% to 1,000%**. The Claude Max architecture is engineered to absorb this surge with zero dropped connections and sub-second reasoning response times.

---

### 3. Claude Max AI Specifications

#### 3.1 Claude Vision Multimodal OCR Engine
- **Target Workload:** Scanned handwritten notes, chalkboard derivations, and circuit diagrams.
- **Model:** Claude 3.5 Sonnet / Claude Vision.
- **Throughput Capability:**
  - Processing Speed: **1.2 to 2.0 seconds per page**.
  - Batch Processing: ~1,800 scanned notebook pages per hour.
- **Mathematical Formula Extraction:**
  - Extracts complex handwritten multi-line equations directly into standardized **LaTeX syntax**.
  - Example target conversions: Maxwell's equations, Laplace/Fourier transforms, Navier-Stokes differentials, matrix eigenvalue proofs.
- **Visual Diagram Captioning:**
  - Logic gate networks, control systems block diagrams, and civil engineering shear force diagrams are translated into structured semantic tags.

#### 3.2 Claude 200,000-Token Context Window Utilization
- **Syllabus-Wide Synthesis:** Engineering courses typically consist of 5 intensive modules spanning 300+ lecture slides.
- **Full-Context Ingestion:** Claude’s 200k context window allows ingesting an entire semester's slide deck simultaneously, enabling:
  - Detection of prerequisite dependencies across lecture weeks.
  - Multi-document cross-referencing (e.g., verifying if a mid-term exam question aligns with Chapter 4 lecture slides).
  - Generation of comprehensive, syllabus-aligned chapter cheat sheets.

#### 3.3 Token Throughput & Rate Limit Sizing
- **Monthly Token Budget Target:** 50 Million to 100 Million tokens / month during active academic cycles.
- **Tokens per Request Profile:**
  - OCR Page Ingestion: ~1,500 input vision tokens + 400 output tokens.
  - Semantic Search Expansion: ~300 input tokens + 100 output tokens.
  - Grounded RAG Study Answer: ~3,500 context tokens + 600 output tokens.
- **Concurrency Rate Limits:** Sized for 100+ concurrent requests per minute during evening study hours (18:00 – 02:00 IST).

#### 3.4 Grounded Claude RAG Assistant
- **Strict Grounding:** Bounded strictly to retrieved context chunks from verified NITK course materials.
- **Zero-Hallucination Policy:** If a query falls outside the official slides, Claude replies:
  > *"This concept is not explicitly covered in the verified course slides for [Subject Name]. Please refer to the prescribed textbook or instructor office hours."*
- **Page Citations:** Generates exact page and slide citations (`[Lecture 7, Slide 14]`).

---

### 4. Supporting Cloud Infrastructure Sizing

To complement Claude Max AI capabilities, the underlying delivery stack is structured across high-availability tiers:

```
Full System Specification Stack
┌───────────────────────────────────┬────────────────────────────────────────────────────────┐
│ Component                         │ Claude Max Specification                               │
├───────────────────────────────────┼────────────────────────────────────────────────────────┤
│ Global Anycast CDN                │ 300+ Edge PoPs · Brotli compression · Sub-20ms latency │
│ Primary Object Storage            │ 10 TB – 50 TB Scalable S3/GCS-compatible hot storage   │
│ Cold Archival Storage             │ 30 TB immutable cold storage (10-yr question banks)    │
│ Serverless Edge Compute           │ 20M requests/mo (Deno / Go runtime) · 18ms avg exec    │
│ Managed PostgreSQL + pgvector     │ 4 vCPU, 16 GB RAM, Multi-AZ HA · 1536-dim vector index │
│ In-Memory Redis Cache             │ 6 GB High-Availability Cluster (&lt; 1ms manifest lookups)│
│ Security & Perimeter Defense      │ Anycast DDoS shield, WAF, Google reCAPTCHA v3          │
└───────────────────────────────────┴────────────────────────────────────────────────────────┘
```

#### 4.1 Storage & Edge Caching
- **Hot Tier:** Houses active semester notes, slides, and lab guides for sub-second retrieval.
- **Warm Tier:** Hugging Face Hub Dataset backend (`saivarshithm/file-vault-assets`) for bulk archival datasets with Git LFS tracking.
- **Cache Hit Ratio (CHR):** **98.4%** at the edge, ensuring rapid page loads and minimal origin strain.

#### 4.2 Vector Search (`pgvector`)
- **Index Type:** HNSW (Hierarchical Navigable Small World) with `m=16` and `ef_construction=64`.
- **Search Latency:** **< 15ms** cosine similarity resolution over 500,000+ indexed chunks.

---

### 5. Claude API Privacy & Zero Data Retention (ZDR)

```
Privacy & Academic Data Governance
├── Zero Data Retention (ZDR): Academic notes and student queries are never used to train models.
├── Zero Student Surveillance: No login required for reading; zero tracking cookies or analytics pixels.
├── Content Governance: Strictly educational fair-use materials (lecture slides, notes, past papers).
└── Security: TLS 1.3 in transit; AES-256-GCM encryption at rest with Cloud KMS keys.
```

---

### 6. Service Level Objectives (SLOs)

| Metric | Target Objective |
|:---|:---|
| **Platform Availability** | 99.99% Uptime |
| **Edge TTFB (Time to First Byte)** | < 50ms globally |
| **Claude AI Query Response** | < 1.5s for conversational answers; < 2.5s for vision OCR |
| **Search Resolution (Keyword)** | < 5ms in-memory client |
| **Search Resolution (Semantic Vector)**| < 25ms end-to-end |
| **Concurrency Ceiling** | 25,000 concurrent sessions |

---

<div align="center">
<sub>Claude Max Specifications · FileVault NITK · National Institute of Technology Karnataka, Surathkal · © 2026</sub>
</div>
