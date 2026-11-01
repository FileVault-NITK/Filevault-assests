# Cloud Infrastructure Sizing & Technical Specification

## FileVault: Enterprise Cloud Resource Architecture & Capacity Planning

**Document Status:** Cloud Grant Specification (Ready for Review)  
**Associated Diagram:** `assets/diagrams/cloud-infrastructure-topology.svg`  
**Platform Target:** [https://filevault.cc](https://filevault.cc)  
**Lead Architect:** Sai Varshith M, National Institute of Technology Karnataka (NITK), Surathkal  

---

### 1. Overview & Cloud Topology

<div align="center">
  <img src="assets/diagrams/cloud-infrastructure-topology.svg" alt="Cloud Infrastructure Topology" width="100%"/>
</div>

To provide high-availability service for 15,000+ engineering students and researchers across India, FileVault requires a balanced, cost-optimized cloud topology. This specification provides granular capacity planning, resource sizing, and cost estimation for evaluating committees.

---

### 2. Workload & Traffic Modeling

Academic traffic follows a highly distinct seasonal pattern compared to standard SaaS products:

```
Traffic Demand Profiles
┌──────────────────────────────────────┬───────────────────────┬──────────────────────────┐
│ Parameter                            │ Regular Semester Mode │ Peak Examination Mode    │
├──────────────────────────────────────┼───────────────────────┼──────────────────────────┤
│ Daily Active Users (DAU)             │ 1,500 – 2,500         │ 10,000 – 18,000          │
│ Peak Concurrent Requests             │ 300 req/sec           │ 4,500 req/sec            │
│ Daily Transferred Egress             │ 80 GB – 150 GB        │ 1.2 TB – 2.8 TB / day    │
│ Average Request Latency Target       │ &lt; 50ms               │ &lt; 80ms under 10× surge │
│ File Stream Concurrency (PDF/Video)  │ 120 streams           │ 2,500+ streams           │
└──────────────────────────────────────┴───────────────────────┴──────────────────────────┘
```

#### Peak Exam Surge Analysis:
During the two-week mid-term and three-week end-term examination windows, request volumes surge by **600% to 1,000%**. Infrastructure must automatically scale out without administrative intervention, then scale down during vacation periods to preserve cloud credits.

---

### 3. Detailed Cloud Services Mapping

The architecture is designed to be cloud-agnostic, supporting seamless deployment on **Google Cloud Platform (GCP)**, **Amazon Web Services (AWS)**, or **Microsoft Azure**:

| Component Layer | AWS Equivalent | GCP Equivalent | Cloudflare / Independent | FileVault Role |
|:---|:---|:---|:---|:---|
| **Edge Distribution** | CloudFront + Shield | Cloud CDN + Cloud Armor | Cloudflare Enterprise | Global Anycast caching, DDoS defense, SSL termination |
| **Serverless Compute** | Lambda / CloudFront Functions | Cloud Functions (2nd Gen) / Run | Cloudflare Workers / Supabase Deno | Token generation, stream auth, dynamic manifest sync |
| **Primary Object Storage** | Amazon S3 Standard | Google Cloud Storage Standard | Cloudflare R2 / MinIO | Hot storage for active semester courseware & slides |
| **Cold Archival Storage** | Amazon S3 Glacier Flexible | GCS Coldline / Archive | Backblaze B2 | 10-year question banks & historical lecture media |
| **Relational Database** | Amazon Aurora PostgreSQL | Cloud SQL for PostgreSQL | Managed Supabase DB | Profiles, verified logs, taxonomies, RLS policies |
| **Vector Search Engine** | pgvector on Aurora / OpenSearch | Cloud SQL pgvector / Vertex AI | Supabase pgvector | 1536-dimensional dense vector embeddings |
| **In-Memory Cache** | Amazon ElastiCache (Redis) | Memorystore for Redis | Upstash / Redis Enterprise | Manifest caching, rate limits, active download locks |
| **AI / GPU Compute** | EC2 G4dn / G5 (T4 / A10G) | Compute Engine (NVIDIA L4) | Modal / RunPod / Vertex | Batch OCR on handwritten notes, LaTeX extraction |
| **Key Management** | AWS KMS | Cloud KMS | HashiCorp Vault | Envelope encryption and cryptographic token keys |

---

### 4. Component Sizing & Resource Specifications

#### 4.1 Tier 1: Cloud Object Storage Sizing
- **Hot Tier (Standard Multi-Region):**
  - **Initial Capacity:** 10,000 GB (10 TB).
  - **Storage Class:** Standard Object Storage with 99.999999999% (11 9's) annual durability.
  - **Byte-Range Support:** Full HTTP `Range: bytes=...` support enabled for in-browser streaming of 500MB+ lecture videos and PDF page-by-page rendering.
  - **Replication:** Dual-region active redundancy (e.g., Mumbai + Hyderabad for India regional low-latency).
- **Cold Tier (Archival):**
  - **Initial Capacity:** 30,000 GB (30 TB).
  - **Lifecycle Transition Policy:** Automatic transition from Hot to Cold for objects untouched for 180 consecutive days.
  - **Retrieval SLA:** Standard 3–5 hour retrieval window for historical curriculum archives.

#### 4.2 Tier 2: Egress & Edge Network
- **Monthly Egress Allocation:** 15,000 GB – 25,000 GB / month (15 TB – 25 TB).
- **Cache Optimization Rules:**
  - `files.json`: Cache for 300s, stale-while-revalidate for 86,400s.
  - Static media (PDF/PNG/SVG): Cache for 2,592,000s (30 days) with immutable cache headers.
  - Manifest Brotli compression level 11 applied at edge.
- **Estimated Cache Hit Ratio (CHR):** **98.4%**, drastically reducing origin read I/O operations and cost.

#### 4.3 Tier 3: Serverless Compute & Gateway
- **Monthly Invocations:** ~20,000,000 requests.
- **Execution Profile:**
  - Average execution time: 18ms.
  - Allocated Memory: 256 MB.
  - Concurrency Limit: Auto-scale from 0 to 1,000 concurrent instances in < 200ms.
- **Cold-Start Elimination:** Keep-alive edge workers maintain warm pools during active exam hours (06:00 to 23:00 IST).

#### 4.4 Tier 4: Managed PostgreSQL & Vector Search Sizing
- **Compute:** 4 vCPU, 16 GB RAM.
- **Storage:** 250 GB NVMe SSD with automated storage auto-scaling up to 1 TB.
- **Index Configuration:**
  - `pgvector` extension enabled.
  - HNSW (Hierarchical Navigable Small World) index with `m=16` and `ef_construction=64`.
  - Sub-15ms cosine similarity distance queries over 500,000 document chunks.
- **High-Availability Configuration:**
  - Active-Standby multi-AZ replica with automated failover (< 30 seconds).
  - Point-in-time recovery (PITR) with continuous WAL archiving.

#### 4.5 Tier 5: GPU Document Intelligence Node
- **Instance Specification:** 1× NVIDIA L4 (24 GB VRAM) or NVIDIA T4 (16 GB VRAM).
- **Operation Schedule:** Batch processing (scheduled off-peak runs, ~4 hours daily during semester or on-demand when large professor collections are uploaded).
- **Throughput:** ~1,200 PDF pages processed per hour (OCR + LaTeX math formula parsing + embedding generation).

---

### 5. Annual Cloud Budget & Cost Breakdown

The table below presents the projected commercial cloud consumption model, demonstrating high architectural efficiency:

```
Itemized Cloud Cost Analysis (Monthly & Annualized)
┌───────────────────────────────────┬──────────────┬──────────────┬─────────────────────────┐
│ Cloud Infrastructure Item         │ Monthly Cost │ Annual Cost  │ Billing Sizing / Metric │
├───────────────────────────────────┼──────────────┼──────────────┼─────────────────────────┤
│ Hot Object Storage (10 TB)        │ $230.00      │ $2,760.00    │ $0.023 / GB-mo          │
│ Cold Archive Storage (30 TB)      │ $60.00       │ $720.00      │ $0.002 / GB-mo          │
│ Global CDN & Egress (20 TB/mo)    │ $450.00      │ $5,400.00    │ Tiered academic egress  │
│ Serverless Edge Compute (20M req) │ $85.00       │ $1,020.00    │ Invocations + GB-sec    │
│ Managed PostgreSQL (HA + Vector)  │ $260.00      │ $3,120.00    │ 4 vCPU, 16 GB, Multi-AZ │
│ In-Memory Redis Cache (6 GB)      │ $75.00       │ $900.00      │ High-availability pair  │
│ Cloud GPU Inference (Batch OCR)   │ $380.00      │ $4,560.00    │ NVIDIA L4/T4 spot usage │
│ Security, WAF & Cloud KMS         │ $60.00       │ $720.00      │ Rules + Key operations  │
├───────────────────────────────────┼──────────────┼──────────────┼─────────────────────────┤
│ TOTAL ESTIMATED SPEND             │ $1,600.00/mo │ $19,200.00   │ Fully Loaded Enterprise │
└───────────────────────────────────┴──────────────┴──────────────┴─────────────────────────┘
```

*Note: With an academic grant or Cloud Max sponsorship tier, this entire cost is covered through cloud credits or in-kind educational allocations, unlocking transformative value for thousands of students.*

---

### 6. Auto-Scaling, Observability & Health Rules

```
Auto-Scaling & Alerting Thresholds
├── Edge Functions Auto-Scale:
│   ├── Trigger: Inflight requests > 50 per instance
│   └── Scale Step: +10 instances, Max: 1,000 instances
├── PostgreSQL Read-Replica Scale:
│   ├── Trigger: CPU Utilization > 75% for 3 consecutive minutes
│   └── Action: Route read traffic to read-replica cluster
├── Storage Auto-Expansion:
│   ├── Trigger: Available storage < 20%
│   └── Action: Automatic volume expansion in 50 GB blocks
└── Health & Observability Alerts:
    ├── Edge P95 Latency > 150ms -> Pager alert to engineering team
    ├── Origin 5xx Error Rate > 0.5% -> Automatic fallback to stale cache
    └── Security: WAF block count > 500/min -> Automatic IP CIDR rate-limit
```

---

<div align="center">
<sub>FileVault Cloud Infrastructure Specification · National Institute of Technology Karnataka (NITK), Surathkal · © 2026</sub>
</div>
