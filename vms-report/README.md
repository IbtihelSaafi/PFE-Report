# Vulnerability Management System (VMS)
## End-of-Study Project Report — ISI Ariana 2025-2026
**Author:** Ibtihel SAAFI

---

## Project Overview

This repository contains the complete LaTeX source for the VMS end-of-study project report. The Vulnerability Management System is a web-based application built with Python/Flask that integrates with Tenable Nessus to provide a complete vulnerability lifecycle management platform with local AI remediation support via Ollama/Mistral 7B.

### Key Features
- 🔍 **Nessus Integration** — Automated scan import via Tenable REST API
- 🔄 **Lifecycle Management** — 6-state finding workflow (NEW → CLOSED)
- ⏱️ **SLA Enforcement** — Automatic deadlines: Critical 7d, High 15d, Medium 30d, Low 60d
- 🤖 **Local AI** — Ollama/Mistral 7B for privacy-preserving remediation guidance
- 🔑 **Deduplication** — Composite key (asset_id + plugin_id + port + protocol)
- 📧 **Notifications** — 5 automated email trigger types
- 👥 **RBAC** — 4 roles: Analyst, Sysadmin, Manager, Admin

### Technology Stack
| Layer | Technology |
|-------|-----------|
| Backend | Python 3.11, Flask 3.0 |
| Database | PostgreSQL 16, SQLAlchemy |
| AI/LLM | Ollama 0.3, Mistral 7B |
| Scanner | Tenable Nessus 10.7 |
| Frontend | Jinja2, Bootstrap 5 |
| Email | Flask-Mail, SMTP |
| Deployment | Docker, Docker Compose |

---

## Report Structure

```
main.tex                  ← Main document (compile this)
cover.tex                 ← Title page
cover_black.tex           ← Black separator cover (ISI-style)
signatures.tex            ← Signature approval page
dedication.tex            ← Dedication
acknowledgments.tex       ← Acknowledgments
abstract.tex              ← Abstract (EN + FR)
chap01_context.tex        ← Chapter 1: General Context
chap02_requirements.tex   ← Chapter 2: Requirements Analysis
chap03_technical.tex      ← Chapter 3: Technical Study ⭐
chap04_implementation.tex ← Chapter 4: Implementation & Results
conclusion.tex            ← Conclusion & Future Work
appendix.tex              ← SQL Schema, API Docs, Install Guide
references.bib            ← Bibliography
img/                      ← All diagrams and charts (PNG)
Makefile                  ← Build automation
```

---

## Quick Build

### Prerequisites

**Ubuntu/Debian:**
```bash
sudo apt install texlive-full biber
```

**macOS:**
```bash
brew install --cask mactex
```

**Windows:** Install [MiKTeX](https://miktex.org/) or [TeX Live](https://tug.org/texlive/)

### Build PDF

```bash
# Full build (recommended — runs 3 passes for TOC, refs, glossary)
make pdf

# Quick single-pass build
make quick

# Build and open
make view

# Clean auxiliary files
make clean
```

The output will be `main.pdf` in the project root.

---

## Source Code Repository

The VMS source code is available at:
**https://github.com/bahagmar/Vulnerability-Management-Tool**

---

## Lab Environment Summary

| VM | IP Address | OS | Vulnerabilities |
|----|-----------|-----|----------------|
| vm-01 | 192.168.162.10 | AlmaLinux 9 | 53 |
| vm-02 | 192.168.162.11 | AlmaLinux 9 | 51 |
| vm-03 | 192.168.162.12 | AlmaLinux 9 | 27 |
| **Total** | | | **131** |

Severity breakdown: Critical (8), High (18), Medium (22), Low (35), Info (48)

---

## Institution

**Institut Supérieur d'Informatique de l'Ariana (ISI Ariana)**  
Ariana, Tunisia | Academic Year 2025–2026
