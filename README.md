# KC7 Security Investigations

This repository contains security investigations I completed while working through the **KC7 Security Analyst I** learning path.

I created this repo to document how I approached the investigations, the KQL I used to work through the evidence, and the conclusions I reached from the available logs.

These are guided training scenarios provided by KC7, so I keep this repository separate from my self-built SOC home lab. The focus here is on investigation methodology, log analysis, and getting more comfortable working through security data with KQL.

## Investigations

| # | Investigation | Main areas covered |
|---|---|---|
| 01 | [CloutHaus: Social Media Leads to Compromise](./01-clouthaus/) | Suspicious logins, reconnaissance, OSINT, web activity, account compromise |
| 02 | [A Scandal in Valdoria: A Political Mystery](./02-scandal-in-valdoria/) | Email investigation, malicious downloads, process analysis, persistence, discovery, collection and exfiltration |

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

## Data Sources

Across the investigations I worked with tables such as:

- `Employees`
- `Email`
- `AuthenticationEvents`
- `InboundNetworkEvents`
- `OutboundNetworkEvents`
- `PassiveDns`
- `FileCreationEvents`
- `ProcessEvents`

## About KC7

[KC7](https://kc7cyber.com/) is a cybersecurity training platform built around investigation-style exercises using log data and Kusto Query Language (KQL).

The scenarios and datasets in this repository come from KC7. The notes, query organization, and investigation summaries reflect my own learning while completing the exercises.

## Status

I am currently working through the **Security Analyst I** path and will add selected investigations as I complete them.
