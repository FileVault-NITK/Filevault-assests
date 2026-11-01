# Cloud Infrastructure Sponsorship & Grant Proposal

## Project FileVault: High-Throughput, AI-Augmented Academic Resource Infrastructure for Higher Education

**Institution:** National Institute of Technology Karnataka (NITK), Surathkal  
**Project Platform:** [https://filevault.cc](https://filevault.cc)  
**Principal Lead & Architect:** Sai Varshith M, B.Tech Scholar, NITK Surathkal  
**Proposal Target:** Cloud Grant Program / Cloud Max Infrastructure Subscription / Academic Research Credits  
**Date:** Academic Year 2026–2027  

---

### Executive Summary

Access to high-quality academic materials—lecture slides, curated laboratory manuals, handwritten professor notes, past examination archives, and reference code—is the single most vital determinant of student success in technical engineering education. Yet across premier technical institutions like the **National Institute of Technology Karnataka (NITK), Surathkal**, academic knowledge remains severely fragmented across disparate Google Drive folders, fleeting WhatsApp groups, and fragile ephemeral links.

**FileVault** ([filevault.cc](https://filevault.cc)) was engineered to solve this challenge. It provides a lightning-fast, zero-friction, searchable academic repository that currently serves thousands of engineering students across all semesters and departments. Built with a user-centric, zero-login philosophy, FileVault delivers sub-100ms in-browser previews of complex multi-format courseware, client-side ZIP compilation, and community-driven verification.

As FileVault enters its next phase of maturity, the platform faces significant infrastructure demands:
1. **Exponential Data Growth:** Moving from gigabytes to tens of terabytes of high-resolution engineering courseware, video tutorials, and interactive datasets.
2. **Massive Exam-Time Concurrency:** Unpredictable traffic surges during mid-term and end-semester examination cycles where 10,000+ students generate concurrent requests, demanding high-throughput edge CDN egress and auto-scaling compute.
3. **AI-Driven Document Intelligence:** Transitioning from basic filename keyword search to deep multimodal OCR (extracting handwritten equations and diagrams) and semantic vector search with an intelligent RAG (Retrieval-Augmented Generation) study assistant.

To accomplish this vision without compromising our zero-cost, open-access commitment to students, we are formally requesting a **Cloud Grant / Cloud Max Tier Subscription**. This proposal outlines the project architecture, resource sizing, implementation roadmap, and societal impact that this partnership will unlock.

---

### 1. Institutional Background: NITK Surathkal

The **National Institute of Technology Karnataka, Surathkal (NITK)**, established in 1960 and declared an **Institute of National Importance** by the Parliament of India, is one of India's premier public engineering institutions (consistently ranked in the top 10 engineering institutions nationwide by NIRF).

- **Student Body:** Over 7,500 full-time undergraduate, postgraduate, and doctoral scholars.
- **Academic Ecosystem:** 13 specialized engineering and science departments, encompassing Computer Science, Artificial Intelligence, Electronics & Communication, Electrical & Electronics, Mechanical, Chemical, Civil, Metallurgy, and Information Technology.
- **Academic Rigor:** Heavy reliance on continuous evaluations, laboratory projects, and semester exams requiring rapid access to exhaustive reference materials.

FileVault was conceived on the NITK campus to empower this student body, bridging the gap between classroom instruction and independent student research.

---

### 2. The Problem: Academic Knowledge Fragmentation

In modern technical education, student learning is impeded by severe systemic knowledge distribution bottlenecks:

```
┌────────────────────────────────────────────────────────────────────────┐
│ Current Academic Sharing Landscape                                     │
├───────────────────────┬────────────────────────────────────────────────┤
│ Ephemeral Messengers  │ WhatsApp/Telegram links expire, media degrades │
│ Personal Cloud Drives │ Storage limits (15 GB cap), dead sharing links │
│ Institutional LMS     │ Heavy login friction, sluggish UI, rigid silos │
│ Scanned Materials     │ Handwritten notes are unsearchable images      │
│ Exam Period Surges    │ Bandwidth choking, rate-limits, and downtime   │
└───────────────────────┴────────────────────────────────────────────────┘
```

#### Core Challenges Addressed by FileVault:
- **Zero Friction:** Students should never be barred from study materials by clunky login portals, expired links, or intrusive paywalls.
- **Format Inclusivity:** Engineering requires viewing PDF lab manuals, LaTeX slides, high-resolution circuit schematics, source code repositories, and recorded demonstrations in a unified interface.
- **Searchable Intelligence:** Students need to search for conceptual terms (e.g., *"Nyquist stability criterion"* or *"Deadlock avoidance Dijkstra"*) and instantly find the exact slide or handwritten note where that concept is discussed.

---

### 3. FileVault Architecture & Current Traction

FileVault was developed with relentless focus on performance and architectural minimalism.

```
Current Live Platform Status:
├── Domain: https://filevault.cc
├── Availability: 99.8% over past 12 months
├── Daily Average Users: 1,500 – 2,500 active engineering students
├── Peak Concurrent Users: 4,000+ (during mid-semester examination weeks)
├── Supported Departments: 8 engineering disciplines, 1st through 4th Year
└── Community Contributions: 150+ student contributors via verified webhooks
```

#### Innovative Features Already Shipped:
1. **Lightweight PWA Client:** Zero-framework, zero-build vanilla JavaScript core delivering sub-100ms First Contentful Paint (FCP) and near-zero memory footprint.
2. **In-Browser Multi-Format Previewer:** Native streaming previews for PDFs, audio, video, images, and syntax-highlighted code with line numbers.
3. **One-Screen Resource Comparison:** Dual-pane comparison viewer enabling students to contrast lecture notes with textbook solutions side-by-side.
4. **Client-Side ZIP Generation:** Leverages `JSZip` in a Web Worker to package hundreds of megabytes of course files into a single download directly in the client's browser, offloading server compute entirely.
5. **Hybrid Storage Strategy:** Initial migration of bulk assets to Hugging Face Hub datasets and Supabase Edge Functions for tokenized streaming.

---

### 4. Why We Need a Cloud Max / Cloud Grant Subscription

While FileVault's initial architecture proved the viability of the model, scaling to institutional multi-campus adoption requires transitioning from free-tier workarounds to **enterprise cloud infrastructure**.

```
Free Tier Limitations vs. Cloud Max Capabilities
┌────────────────────────┬─────────────────────┬───────────────────────────┐
│ Metric / Component     │ Current Free Tier   │ Cloud Max Specification   │
├────────────────────────┼─────────────────────┼───────────────────────────┤
│ Object Storage         │ ~10 GB fragmented   │ 10 TB – 50 TB Scalable S3 │
│ Egress Bandwidth       │ 100 GB/month limit  │ 20 TB+/month Unthrottled  │
│ Exam Surge Concurrency │ Throttled / Dropped │ 25,000+ Concurrent Scale  │
│ Search Capability      │ Keyword filename    │ Multimodal Vector Search  │
│ OCR Processing         │ None (Images blind) │ GPU Cloud OCR for Notes   │
│ Service Level Target   │ Best-effort         │ 99.99% High Availability  │
└────────────────────────┴─────────────────────┴───────────────────────────┘
```

#### Critical Infrastructure Pillars Funded by the Grant:

#### Pillar A: High-Performance Object Storage & Global CDN
- **Scalable Object Storage:** S3/Google Cloud Storage compatible buckets with lifecycle management (Hot for current semester notes, Warm for past 2 years, Cold archival for 10-year question papers).
- **Global Anycast Edge Network:** Low-latency CDN edge delivery ensuring sub-20ms file streaming across India, eliminating buffering during critical pre-exam study hours.
- **High Egress Allowances:** Freedom from bandwidth caps that currently threaten platform availability during finals week.

#### Pillar B: Serverless Compute & High-Availability Database
- **Auto-Scaling Compute:** Managed serverless functions to handle token generation, file integrity verification, and dynamic manifest compression.
- **Managed PostgreSQL with pgvector:** High-availability database cluster with automated failover, read replicas, and vector index support for academic search.
- **Redis In-Memory Cache:** Sub-millisecond caching for global manifest lookups and rate limiting.

#### Pillar C: Cloud GPU & AI Document Intelligence (Cloud Max Core)
- **Handwritten Note Multimodal OCR:** Processing tens of thousands of scanned handwritten lecture notes using cloud GPU instances to extract readable text, LaTeX mathematical formulas, and circuit schematics.
- **Dense Vector Search:** Generating embeddings for every document chunk, enabling semantic search (e.g., searching for "thermodynamic entropy derivation" retrieves the exact page in a 200-page scanned notebook).
- **RAG Academic Study Assistant:** A bounded, grounded conversational assistant that allows students to ask questions directly against their official course syllabi and lecture materials with zero hallucinations.

---

### 5. Detailed Resource Sizing & Budget Justification

The following itemized budget outlines the exact cloud resource allocation requested over a 12-month period:

| Cloud Resource Category | Specifications & Sizing | Purpose & Workload Justification | Estimated Monthly Cost | 12-Month Total |
|:---|:---|:---|:---:|:---:|
| **Cloud Object Storage (Hot Tier)** | 10 TB Standard Multi-Region S3 / GCS Storage | Primary storage for active semester notes, slides, lab guides, and syllabi. | \$230 | \$2,760 |
| **Cloud Object Storage (Cold Tier)** | 30 TB Glacier / Coldline Archive Storage | 10-year question banks, past project reports, and archival video lectures. | \$60 | \$720 |
| **Global CDN & Egress Bandwidth** | 15 TB – 25 TB monthly egress allowance | High-throughput, low-latency streaming to 10,000+ concurrent students. | \$450 | \$5,400 |
| **Serverless Compute / Edge Workers** | 20M requests/month, 128MB–512MB RAM | Pre-signed URL token dispatching, webhook validation, and manifest generation. | \$85 | \$1,020 |
| **Managed PostgreSQL + pgvector** | 4 vCPU, 16 GB RAM, 250 GB SSD (HA Pair) | User profiles, subject taxonomies, audit logs, and 1536-dim vector embeddings. | \$260 | \$3,120 |
| **Redis In-Memory Cluster** | 2-Node In-Memory Cluster (6 GB RAM) | Manifest caching, rate-limiting counters, and active session states. | \$75 | \$900 |
| **GPU Compute for AI & OCR** | 1× NVIDIA L4 / T4 Cloud GPU Instance (On-Demand / Spot) | Batch OCR processing of scanned notes and embedding generation. | \$380 | \$4,560 |
| **Security, WAF & Key Management** | Cloud KMS + Enterprise WAF rules | Cryptographic envelope encryption and DDoS attack protection. | \$60 | \$720 |
| **Total Cloud Grant Requested** | **12-Month Comprehensive Cloud Infrastructure** | **Institutional Academic Infrastructure** | **\$1,600 / mo** | **\$19,200** |

*(Note: We warmly welcome direct cloud credit allocations, Cloud Max organizational tiers, or in-kind cloud services equivalent to this scope).*

---

### 6. 12-Month Implementation Roadmap

```
Phase 1: Cloud Migration & Foundation (Months 1–3)
├── Deploy multi-region Cloud Object Storage buckets with automated lifecycle policies.
├── Migrate existing academic repository to primary cloud storage with SHA-256 validation.
├── Configure Anycast CDN edge distributions, Brotli compression, and custom domain SSL.
└── Implement Cloud KMS for zero-secret serverless token authentication.

Phase 2: High-Availability Database & Scaled Ingestion (Months 4–6)
├── Deploy Managed PostgreSQL with pgvector and automated point-in-time recovery (PITR).
├── Integrate Redis cluster for sub-millisecond manifest caching.
├── Launch expanded contribution gateway with automated viral and MIME-type security checks.
└── Stress test architecture under simulated 25,000 concurrent user loads.

Phase 3: AI Document Intelligence & Multimodal OCR (Months 7–9)
├── Stand up GPU-accelerated OCR pipeline for scanned and handwritten engineering notes.
├── Generate vector embeddings across all indexed lecture slides, textbooks, and lab guides.
├── Ship semantic search interface on filevault.cc with highlighted citation snippets.
└── Deploy automated duplicate detection and perceptual hashing.

Phase 4: RAG Academic Study Assistant & Multi-Campus Expansion (Months 10–12)
├── Roll out grounded RAG study assistant for syllabus-aligned exam revision.
├── Onboard sister NIT and premier engineering campuses onto federated FileVault instances.
├── Publish comprehensive project impact report, open-access dataset, and architecture case study.
└── Transition platform into long-term self-sustaining institutional academic consortium.
```

---

### 7. Measurable Impact & Key Performance Indicators (KPIs)

The success of the Cloud Grant partnership will be measured against clear, objective milestones:

```
┌──────────────────────────────────────┬───────────────────────┬──────────────────────────┐
│ Performance Metric                  │ Baseline (Current)    │ Year 1 Target (Post-Grant│
├──────────────────────────────────────┼───────────────────────┼──────────────────────────┤
│ Active Engineering Student Users     │ 2,500 students        │ 15,000+ students         │
│ Total Indexed Academic Resources     │ ~2,000 documents      │ 25,000+ documents        │
│ Peak Exam Concurrency Handling       │ 4,000 requests        │ 25,000+ requests         │
│ Average Page & Search Latency (TTFB) │ 180ms                 │ &lt; 50ms at Edge           │
│ Search Success Rate (Finding Notes)  │ 62% (Filename only)   │ 96% (Semantic + OCR)     │
│ Platform Uptime SLA                  │ 99.8%                 │ 99.99%                   │
│ Student Hours Saved per Exam Cycle   │ ~15,000 hours         │ 100,000+ hours           │
└──────────────────────────────────────┴───────────────────────┴──────────────────────────┘
```

---

### 8. Value Proposition for the Cloud Provider

Supporting FileVault offers unprecedented strategic value to the sponsoring cloud provider:

1. **Direct Developer Mindshare:** NITK Surathkal graduates enter top global technology firms (Google, Microsoft, Amazon, NVIDIA, Apple) every year. Associating your cloud ecosystem with their daily academic hub creates lifelong brand loyalty among premier software engineers.
2. **Flagship Academic Case Study:** Demonstrates how modern cloud infrastructure (Edge compute, S3/GCS tiering, and GPU AI inference) can solve real-world education challenges at institutional scale.
3. **Public Recognition & Co-Branding:** Prominent placement of *"Powered by [Cloud Provider Name] Cloud Max / Academic Grants"* on the [filevault.cc](https://filevault.cc) homepage, README badges, and presentation materials.
4. **Social & Educational Equity:** Direct alignment with ESG and educational access charters, democratizing access to premier study materials for underprivileged students who cannot afford commercial subscriptions.

---

### 9. Conclusion & Call to Action

FileVault has already demonstrated real-world adoption, engineering efficiency, and genuine impact across the NITK student community with zero commercial backing. With the support of a **Cloud Grant / Cloud Max Subscription**, we can provide an unshakeable, intelligent foundation that ensures every engineering student has the resources they need to excel.

We welcome the opportunity to discuss this proposal with your academic relations and cloud grant review committee.

**Submitted with pride by:**  
**Sai Varshith M**  
B.Tech Scholar, National Institute of Technology Karnataka (NITK), Surathkal  
Creator & Lead Architect, FileVault  
Website: [https://filevault.cc](https://filevault.cc)  
GitHub Organization: [https://github.com/FileVault-NITK](https://github.com/FileVault-NITK)  
Email: `saivarshith.nitk@gmail.com`
