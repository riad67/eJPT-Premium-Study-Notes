<div align="center">

# eJPT Premium Study Notes

**A structured, GitHub-friendly rewrite of Riad Hossain's eJPT study notes and lab walkthroughs**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Status](https://img.shields.io/badge/status-community%20resource-blue)](#attribution-and-license)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

*Reconnaissance → Enumeration → Exploitation → Post-Exploitation → Web Applications*

</div>

---

## About

This repository reorganizes a large set of personal eJPT (eLearnSecurity Junior Penetration Tester) lab notes into a consistent, numbered folder structure so they're easy to browse, search, and link to on GitHub. Every note keeps a short provenance line pointing back to its place in the original source material.

>  **These are personal lab notes, not a certification guide.** Commands, IP addresses, credentials, and tool output are specific to the original lab environments they were written in. Treat every example as something to *verify*, not copy-paste blindly — see [Disclaimer](#disclaimer--responsible-use) below.

## Table of contents

- [Learning path](#learning-path)
- [How to use these notes](#how-to-use-these-notes)
- [Prerequisites](#prerequisites)
- [Repository structure](#repository-structure)
- [Disclaimer & responsible use](#disclaimer--responsible-use)
- [Attribution and license](#attribution-and-license)
- [Contributing](#contributing)

## Learning path

The sections below follow the eJPT assessment methodology end to end. Work through them in order, or jump straight to the topic you need — each section has its own index page.

| # | Section | Files | Focus |
|---|---------|:---:|---------|
| 01 | [Getting Started](01-getting-started/README.md) | 3 | Methodology overview, exam mindset |
| 02 | [Information Gathering](02-information-gathering/README.md) | 6 | OSINT, DNS recon, subdomains, email |
| 03 | [Active Reconnaissance](03-active-reconnaissance/README.md) | 5 | Host discovery, zone transfers, port scanning |
| 04 | [Footprinting and Scanning](04-footprinting-and-scanning/README.md) | 7 | Nmap-driven host and service discovery |
| 05 | [Service Enumeration](05-service-enumeration/README.md) | 14 | FTP, SMB, Apache, MySQL, SSH, SMTP |
| 06 | [Vulnerability Assessment](06-vulnerability-assessment/README.md) | 5 | DAVTest, Shellshock, WMAP scanning |
| 07 | [Host and Network Auditing](07-host-and-network-auditing/README.md) | 1 | Auditing fundamentals |
| 08 | [Host Attacks](08-host-attacks/README.md) | 20 | Windows & Linux host-based exploitation |
| 09 | [Network Attacks](09-network-attacks/README.md) | 5 | NetBIOS, SNMP, DNS/SMB relay |
| 10 | [Metasploit](10-metasploit/README.md) | 34 | Core framework usage end to end |
| 11 | [Exploitation](11-exploitation/README.md) | 26 | Manual and framework-assisted exploitation |
| 12 | [Post-Exploitation](12-post-exploitation/README.md) | 33 | Enumeration, persistence, pivoting, cleanup |
| 13 | [Web Applications](13-web-applications/README.md) | 3 | Drupal, WordPress, general web attacks |
| 14 | [Pivoting](14-pivoting/README.md) | 1 | Network pivoting |

**180 markdown files across 14 sections.**

## How to use these notes

1. Start with [Getting Started](01-getting-started/README.md) to see how the sections map to the official eJPT methodology.
2. Read a topic's reference notes before attempting its lab — most notes are adapted directly from lab walkthroughs.
3. Use the search bar (GitHub's repo search, or `grep -r "keyword" .` locally) to find every walkthrough that touches a given tool or service — several sections revisit the same service from different angles.
4. Keep your own lab log alongside these notes. IP addresses and credentials shown here belong to the original lab environments and will not match yours.

## Prerequisites

These notes assume basic familiarity with:

- Linux command-line usage and a Kali-based attacker workstation
- TCP/IP networking fundamentals (ports, protocols, DNS)
- A lab environment where you are authorized to test (e.g., INE/eLearnSecurity labs, your own home lab, or `TryHackMe`/`HackTheBox`-style ranges)

## Repository structure

```text
eJPT-Premium-Study-Notes/
├── 01-getting-started/
│   ├── README.md              ← section index
│   └── 01-*.md, 02-*.md, ...  ← individual notes
├── 02-information-gathering/
├── ...
├── 14-pivoting/
├── CONTRIBUTING.md
├── LICENSE
└── README.md                  ← you are here
```

Each note file follows the same layout: a title, a breadcrumb nav line back to the section index and home, a short provenance line, and then the walkthrough itself.

## Disclaimer & responsible use

- Only run the commands and techniques in these notes against systems you own or are explicitly authorized to test.
- These notes are **not an official certification syllabus**. Exam objectives, tool versions, and command syntax change over time — verify anything exam-critical against current official documentation.
- A successful scan or a flagged vulnerability does not, by itself, prove exploitability. Validate before you report.
- Some wording, formatting, and lab-specific details are inherited from the original source and may be incomplete, outdated, or lab-specific (fixed IPs, test credentials, etc.).

## Attribution and license

Original notes by **Riad Hossain** — [eJPT-Premium-Full-Note](https://github.com/riad67/eJPT-Premium-Full-Note). This repository is a cleaned-up, restructured derivative for easier reading and navigation.

The source repository identifies its license as MIT; see [LICENSE](LICENSE). Tools, frameworks, and resources referenced throughout the notes (Metasploit, Nmap, etc.) carry their own separate licenses — this repository's license does not extend to them.

## Contributing

Corrections, clarifications, and additional labs are welcome — see [CONTRIBUTING.md](CONTRIBUTING.md). This project is an independent study resource and is **not** an official INE or eLearnSecurity publication.
