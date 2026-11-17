# Penetration Testing Methodology

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 25–66. Examples are lab-specific and need verification.

A penetration test generally moves through five phases. Each phase builds on the evidence gathered in the one before it.

## 1. Information Gathering

- **Passive information gathering (OSINT)** — collecting data without touching the target directly (WHOIS, search engines, public records, social media).
- **Active information gathering** — interacting with the target to collect data directly.

Examples: network mapping, host discovery, port scanning, service detection, and OS detection.

## 2. Enumeration

Identifying services and the operating system running on each host, then drawing out further detail from them.

Examples: service enumeration, user enumeration, share enumeration.

## 3. Exploitation (Initial Access)

1. **Vulnerability analysis and threat modeling** — identifying and prioritizing vulnerabilities.

   Examples: vulnerability analysis, vulnerability identification.

2. **Exploitation** — developing or adapting exploits and using them against a vulnerable service.

   Examples: developing/modifying exploits, service exploitation.

## 4. Post-Exploitation

Actions taken after gaining a foothold on a target:

1. Local enumeration
2. Privilege escalation
3. Credential access
4. Persistence
5. Defense evasion
6. Lateral movement

## 5. Reporting

Documenting findings so they are reproducible and actionable:

1. Report writing
2. Recommendations
