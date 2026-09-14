# KC7 Security Investigations

This repository contains security investigations I completed while working through the **KC7 Security Analyst I** learning path.

I created this repo to document how I approached the investigations, the queries and tools I used to work through the evidence, and the conclusions I reached from the available data.

These are guided training scenarios provided by KC7, so I keep this repository separate from my self-built SOC home lab. The focus here is on investigation methodology, log analysis, threat-intelligence enrichment, and getting more comfortable working through security data with tools such as KQL and VirusTotal.

## Investigations

| # | Investigation | Main areas covered |
|---|---|---|
| 01 | [CloutHaus: Social Media Leads to Compromise](./01-clouthaus/) | Suspicious logins, reconnaissance, OSINT, web activity, account compromise |
| 02 | [A Scandal in Valdoria: A Political Mystery](./02-scandal-in-valdoria/) | Email investigation, malicious downloads, process analysis, persistence, discovery, collection and exfiltration |
| 03 | [VirusTotal Fundamentals](./03-virustotal-fundamentals/) | Malware triage, file metadata, certificate analysis, YARA/Sigma, sandbox behavior, indicator pivoting and passive DNS |
| 04 | [Jojo's Hospital: A Ransomware Investigation](./04-jojos-hospital/) | Ransomware investigation, process analysis, command-and-control, discovery, data staging and exfiltration |

## Skills I Practiced

- Writing and refining KQL queries
- Filtering and correlating events across different log sources
- Investigating suspicious authentication activity
- Reviewing email and web activity
- Tracking file downloads and file creation events
- Investigating Windows process execution
- Identifying attacker discovery activity
- Following data collection and exfiltration behavior
- Building an attack timeline from separate pieces of evidence
- Triaging suspicious files in VirusTotal
- Reviewing file metadata and code-signing information
- Interpreting crowdsourced YARA and Sigma detections
- Investigating sandbox file, registry, and process behavior
- Pivoting between files, domains, IP addresses, and passive DNS
- Using threat-intelligence context to strengthen an investigation
- Correlating endpoint and network activity across compromised hosts

## Investigation Sources & Tools

Across the investigations I have worked with data and tools including:

- `Employees`
- `Email`
- `AuthenticationEvents`
- `InboundNetworkEvents`
- `OutboundNetworkEvents`
- `PassiveDns`
- `FileCreationEvents`
- `ProcessEvents`
- VirusTotal file, domain, IP, relations, behavior, and community data
- MITRE ATT&CK

## About KC7

[KC7](https://kc7cyber.com/) is a cybersecurity training platform built around investigation-style exercises using security data and analyst tools.

The scenarios and datasets in this repository come from KC7. The notes, query organization, and investigation summaries reflect my own learning while completing the exercises.

## Status

**Security Analyst I completed — 7 of 7 modules (100%).**

The path covered event triage, KQL investigation, phishing and malicious indicators, VirusTotal IOC analysis, and end-to-end security investigation workflows.
