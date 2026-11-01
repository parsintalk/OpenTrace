# OpenTrace

**Transparent Evidence for a Federated Software Ecosystem**

---

## 1. The Problem

Modern software ecosystems depend on package metadata distributed across multiple registries, vulnerability databases, and licensing sources. However, these sources may contain:

- Inconsistent package identifiers and version information.
- Conflicting license declarations.
- Missing or incomplete provenance records.
- Different release dates for apparently identical package versions.
- Insufficient evidence to establish whether two records represent the same software artifact.

These inconsistencies make software supply-chain auditing, dependency verification, and security analysis more difficult.

OpenTrace addresses this challenge by introducing an evidence-based reconciliation framework that preserves source information and makes uncertainty explicit.

---

## 2. Project Objectives

OpenTrace focuses on three primary technical objectives:

### 2.1 Evidence-Based Package Identity Resolution

Identify whether metadata records from different sources refer to the same package and version.

The matching process considers:

- Package name and normalized identifiers.
- Version information.
- Cryptographic checksums and hashes, when available.
- Build and artifact metadata.
- Source-specific identifiers.

Instead of relying exclusively on package names, OpenTrace evaluates multiple matching signals and records the evidence supporting each decision.

### 2.2 Provenance-Aware Metadata Normalization

Every collected metadata claim retains its original source and observation timestamp.

The normalization engine aims to:

- Standardize metadata representations.
- Preserve original source claims.
- Detect conflicting metadata.
- Maintain traceability between normalized records and their sources.
- Avoid silently overwriting conflicting information.

### 2.3 Federated Metadata Distribution

OpenTrace is designed around modular collectors and decentralized data distribution.

The project will investigate interoperability with the CodeSupply Federated Data Catalog and develop machine-readable exports and API interfaces compatible with its validated integration requirements.

---

## 3. Proposed Architecture

The proposed architecture consists of five logical components:

```
┌─────────────────────────────────────────────┐
│  External Metadata Sources                  │
│  npm, NuGet, ...                            │
└─────────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────────┐
│  Metadata Collectors                        │
│  Ingestion & Parsing                        │
└─────────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────────┐
│  Identity Resolution                        │
│  Matching Rules • Evidence Evaluation       │
└─────────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────────┐
│  Provenance & Conflict Engine               │
│  Normalization • Conflict Detection •       │
│  Evidence Graphs                            │
└─────────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────────┐
│  Federated API & Export                     │
│  JSON / Machine-readable • CodeSupply       │
│  Integration                                │
└─────────────────────────────────────────────┘
```

> **Note:** This diagram represents the proposed system architecture.

---

## 4. Core Technical Concepts

### 4.1 Package Identity Matching

OpenTrace uses a multi-signal matching approach.

For two metadata records, A and B, the system evaluates a set of matching signals:

| Signal | Description |
|--------|-------------|
| **Name** | Normalized package name |
| **Version** | Semantic version comparison |
| **Checksum** | Cryptographic artifact identity |
| **Build** | Build and artifact metadata information |
| **Source ID** | Original registry identifier |

The matching engine produces an explicit decision:

- **MATCHED:** Sufficient evidence supports identity equivalence.
- **UNRESOLVED:** Available evidence is insufficient.
- **CONFLICT:** Evidence contains contradictory identity information.

A conceptual matching score can be expressed as:

\[
S(A,B) = \sum_{i=1}^{n} w_i \, m_i(A,B)
\]

Where:

- \( w_i \) represents the weight assigned to a matching signal.
- \( m_i \) represents the normalized result of comparing that signal.
- \( S(A,B) \) represents the combined matching score.

Cryptographic checksum equality, when the checksum covers the same artifact representation, provides stronger evidence than name similarity alone.

### 4.2 Provenance Model

Each metadata claim is associated with:

- Source registry.
- Original package identifier.
- Package version.
- Metadata field.
- Observed value.
- Observation timestamp.
- Evidence reference.

This model enables historical traceability and reproducible metadata analysis.

### 4.3 Conflict Detection

Examples of conflicts include:

| Metadata Field | Source A | Source B |
|----------------|----------|----------|
| License | MIT | Apache-2.0 |
| Release Date | 2025-01-10 | 2025-01-12 |
| Package Version | 2.1.0 | 2.1.1 |

OpenTrace aims to preserve both claims and identify the nature of the discrepancy rather than automatically selecting one source as authoritative.

---

## 5. Planned Repository Structure

This is the proposed development structure. Components will be added as implementation progresses.

---

## 6. Development Roadmap

| Phase | Timeline | Planned Deliverables |
|-------|----------|----------------------|
| **Phase 1** | Months 1–2 | Methodology, provenance model, identity engine |
| **Phase 2** | Months 3–4 | npm/NuGet collectors, normalization, federation API |
| **Phase 3** | Months 5–6 | Benchmarking, validation, documentation, FOSS release |

### Target Evaluation Metrics

The project aims to evaluate its performance against an independently prepared test corpus.

| Metric | Target |
|--------|--------|
| Identity Resolution Precision | ≥ 95% |
| Conflict Detection Precision | ≥ 90% |
| Conflict Detection Recall | ≥ 90% |
| Evaluation Corpus | ≥ 10,000 records |

> These values are project targets, not yet experimentally validated results.

---

## 7. Technology Stack

The proposed implementation will use:

- **Python:** Core processing and evaluation components.
- **JSON:** Machine-readable metadata representation.
- **REST APIs:** Metadata access and interoperability.
- **GitHub Actions:** Continuous integration and regression testing.
- **PostgreSQL / Graph-oriented storage:** Evaluation of persistent metadata and evidence relationships.

Technology choices may be refined during the architecture and implementation phases.

---

## 8. Open-Source Principles

OpenTrace is designed around transparency, reproducibility, and interoperability.

The intended licensing model is:

- **Source code:** Apache License 2.0.
- **Project-created schemas and documentation:** CC-BY 4.0.
- **Project-created benchmark datasets:** CC0 where appropriate.
- **External metadata:** Original source licensing and redistribution conditions will be respected.

---

## 9. Expected Impact

OpenTrace aims to provide reusable infrastructure for:

- Software supply-chain security.
- Open-source dependency auditing.
- License compliance verification.
- Software metadata interoperability.
- Federated digital infrastructure.
- Civic technology and environmental monitoring platforms.

By making metadata claims traceable and conflicts visible, OpenTrace seeks to improve trust and reproducibility across software ecosystems.

---

## 10. Funding & Project Context

| Item | Detail |
|------|--------|
| **Funding Program** | NLnet CodeSupply Open Call (2026-11Y) |
| **Project Duration** | 6 Months |
| **Requested Funding** | 45,000 |
| **R&D Focus** | Federated metadata infrastructure, package identity resolution, provenance tracking, and software supply-chain verification |

---

## 11. Project Status

OpenTrace is currently presented as a research and development prototype proposal.

The repository will progressively include:

- Technical specifications.
- Core implementation modules.
- Metadata collection tools.
- Reproducible benchmark datasets.
- Automated evaluation scripts.
- Integration documentation.

Contributions, technical feedback, and collaboration from the open-source community are welcome.

---

**OpenTrace — Transparent Evidence for a Federated Software Ecosystem.**