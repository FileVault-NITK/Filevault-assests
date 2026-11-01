# FileVault NITK - Cloud Grant & Technical Documentation

<div align="center">

<img src="https://img.shields.io/badge/-%F0%9F%9B%A1%EF%B8%8F_File_Vault_NITK-6366f1?style=for-the-badge&labelColor=090c15&color=6366f1" height="42" alt="File Vault NITK"/>

<br/><br/>

[![Institutional Initiative](https://img.shields.io/badge/Institution-NIT_Karnataka,_Surathkal-0284c7?style=flat-square&labelColor=0f172a)](https://www.nitk.ac.in)
[![Live Platform](https://img.shields.io/badge/Live_Site-filevault.cc-6366f1?style=flat-square&labelColor=0f172a)](https://filevault.cc)
[![Grant Proposal](https://img.shields.io/badge/Program-Cloud_Grant_&_Sponsorship-10b981?style=flat-square&labelColor=0f172a)](GRANT_PROPOSAL.md)
[![License](https://img.shields.io/badge/License-MIT-818cf8?style=flat-square&labelColor=0f172a)](LICENSE)

<br/>

> **Institutional-grade, zero-friction academic knowledge infrastructure**  
> Serving thousands of engineering students at **National Institute of Technology Karnataka (NITK), Surathkal**.  
> This repository contains the official **Cloud Grant Proposal**, **Technical Architecture Whitepaper**, **Infrastructure Sizing Specifications**, and **Visual System Assets** prepared for cloud sponsorship and grant evaluation.

---

</div>

## 📑 Executive Overview

**FileVault** ([filevault.cc](https://filevault.cc)) is a production-grade academic repository developed to eliminate knowledge fragmentation and academic resource disparities across higher education engineering programs. Originally engineered as an ultra-fast, zero-friction single-page portal for NITK Surathkal, FileVault has scaled to support thousands of active students with instant searching, in-browser previews of complex multi-format courseware, and automated dataset synchronization.

To elevate FileVault to a multi-campus, resilient, and AI-augmented academic repository, we are seeking a **Cloud Sponsorship / Cloud Grant Subscription**. This grant will fund the scalable cloud compute, multi-tier object storage, global CDN egress, and GPU-accelerated document intelligence infrastructure required to support over 15,000+ engineering students and researchers.

---

## 🏛️ System Architecture at a Glance

<div align="center">
  <img src="assets/diagrams/architecture-overview.svg" alt="FileVault Cloud Architecture Overview" width="100%"/>
</div>

---

## 📚 Documentation Suite

This repository is strictly structured as an **asset and documentation hub** with zero application source code. Reviewers and cloud evaluation committees can navigate the detailed dossiers below:

| Document | Primary Audience | Scope & Key Contents |
|:---|:---|:---|
| 📄 **[GRANT_PROPOSAL.md](GRANT_PROPOSAL.md)** | **Cloud Grant Committee & Sponsors** | Comprehensive formal proposal, institutional background, problem statement, resource request, 12-month roadmap, KPIs, and budget. |
| 🏗️ **[ARCHITECTURE_AND_SYSTEM_DESIGN.md](ARCHITECTURE_AND_SYSTEM_DESIGN.md)** | **System Architects & Lead Engineers** | Deep technical whitepaper detailing tier topology, client PWA design, Supabase edge functions, storage tiering, and caching. |
| ☁️ **[CLOUD_INFRASTRUCTURE_SPECIFICATION.md](CLOUD_INFRASTRUCTURE_SPECIFICATION.md)** | **DevOps & Cloud Infrastructure Teams** | Granular cloud resource sizing, compute/storage/network capacity planning, exam spike traffic modeling, and cost analysis. |
| ⇄ **[DATA_PIPELINE_AND_LIFECYCLE.md](DATA_PIPELINE_AND_LIFECYCLE.md)** | **Data Engineers & Platform Integrators** | End-to-end data lifecycle from student submission, anti-bot validation, OCR and vectorization, to CDN edge delivery. |
| 🛡️ **[SECURITY_COMPLIANCE_AND_GOVERNANCE.md](SECURITY_COMPLIANCE_AND_GOVERNANCE.md)** | **Security Officers & Compliance Auditors** | Defense-in-depth model: DDoS perimeter shield, tokenized stream security, PostgreSQL RLS, AES-256 encryption, and copyright governance. |
| 🤖 **[AI_AND_STUDY_ASSISTANT_ROADMAP.md](AI_AND_STUDY_ASSISTANT_ROADMAP.md)** | **AI / ML Researchers & Evaluators** | Technical specification for GPU multimodal OCR of handwritten notes, dense vector search (pgvector), and grounded RAG revision assistant. |
| 📊 **[PITCH_DECK.md](PITCH_DECK.md)** | **Executive Reviewers & Program Managers** | 10-slide high-impact presentation deck summarizing vision, traction, metrics, cloud requirements, and societal impact. |

---

## 🎨 Visual Assets & Technical Diagrams

All architectural blueprints are rendered as scalable, self-contained, publication-grade vector graphics:

- 📐 **[assets/diagrams/architecture-overview.svg](assets/diagrams/architecture-overview.svg)**: Complete 4-tier enterprise system architecture.
- ☁️ **[assets/diagrams/cloud-infrastructure-topology.svg](assets/diagrams/cloud-infrastructure-topology.svg)**: Cloud resource sizing, high-availability topology, and failover design.
- ⇄ **[assets/diagrams/data-flow-pipeline.svg](assets/diagrams/data-flow-pipeline.svg)**: 4-stage data ingestion, processing, distribution, and retrieval pipeline.
- 🛡️ **[assets/diagrams/security-model.svg](assets/diagrams/security-model.svg)**: Concentric defense-in-depth security architecture.

---

## 🎯 Key Project Metrics & Traction

```
├── Institutional Reach: National Institute of Technology Karnataka (NITK), Surathkal
├── Live Production Platform: https://filevault.cc
├── Target Academic Audience: 10,000+ Undergraduate & Postgraduate Engineers
├── Current File Index: Multi-gigabyte repository across 8+ Engineering Departments
├── Exam Period Peak Traffic: 25,000+ daily page views, 100+ GB egress bursts
└── Current Architecture: Static PWA + Supabase Edge Functions + Hugging Face Datasets
```

---

## 🤝 Contact & Principal Investigator

**Sai Varshith M**  
B.Tech Scholar, National Institute of Technology Karnataka, Surathkal  
Lead Architect & Creator of FileVault  
* Institutional Inquiries: `saivarshith.nitk@gmail.com`  
* Project Website: [https://filevault.cc](https://filevault.cc)  
* Organization: [FileVault-NITK](https://github.com/FileVault-NITK)

---

<div align="center">
<sub>FileVault is an open academic initiative dedicated to equitable, high-performance educational resource distribution. © 2026 FileVault NITK. Released under the MIT License.</sub>
</div>
