# Jojo's Hospital: A Ransomware Investigation

## Overview

This investigation was the final module in the **KC7 Security Analyst I** path. The scenario follows a hospital compromise from the initial user activity through attacker discovery, command-and-control, data collection, exfiltration, and cleanup.

I used KQL to move between endpoint, authentication, and network evidence and reconstruct the sequence of events rather than treating each event in isolation.

> This is a guided KC7 training scenario. I have intentionally left challenge-answer details out of this write-up and focused on the investigation process and skills I practiced.

## What I Investigated

The investigation included:

- identifying suspicious document execution on an employee workstation
- following process activity after the initial execution
- identifying Cobalt Strike command-and-control activity
- reviewing attacker discovery commands
- correlating activity across more than one compromised host
- investigating access to internal network shares
- identifying data staged into ZIP archives
- tracing exfiltration with `curl`
- identifying cleanup commands used to remove staged files
- using timestamps to rebuild the attack sequence

## Data Sources

I worked mainly with:

- `ProcessEvents`
- `AuthenticationEvents`
- `OutboundNetworkEvents`
- `FileCreationEvents`
- employee / host context from the KC7 dataset

## Investigation Approach

### 1. Start from the suspicious document

I first narrowed `ProcessEvents` to the affected workstation and the timeframe in which the suspicious document was opened. This established a reliable starting point for the rest of the investigation.

### 2. Follow process activity

From the document execution, I reviewed subsequent commands and child processes to identify post-compromise activity. This included command execution, attacker tooling, and system-discovery behavior.

### 3. Pivot into network activity

After identifying suspicious endpoint activity, I correlated it with outbound connections to understand where the compromised host was communicating and to identify command-and-control infrastructure.

### 4. Follow discovery and collection

I tracked commands used to learn about the host and environment, then followed activity involving internal network shares and files that were collected for theft.

### 5. Identify staging and exfiltration

The attackers staged collected data into ZIP archives and transferred the archives to external infrastructure using `curl`. I used process command lines and timestamps to connect the collection, staging, and exfiltration steps.

### 6. Confirm cleanup

Finally, I identified commands used to delete the staged archives after exfiltration, showing an attempt to reduce traces left on the endpoint.

## Skills Practiced

- KQL filtering and timeline analysis
- endpoint process investigation
- parent/child process reasoning
- Cobalt Strike / C2 investigation
- Windows discovery-command analysis
- network-share investigation
- data staging and archive analysis
- exfiltration analysis
- command-line investigation
- event correlation across hosts and data sources
- building an attack narrative from individual events

## Key Takeaway

The most useful part of this investigation was seeing how separate events become meaningful when placed in sequence. A document opening, a suspicious process, an outbound connection, discovery commands, archive creation, `curl` traffic, and file deletion each provide only part of the picture. Correlating them into a timeline makes the attacker workflow much clearer.

## KC7 Path Completion

Completing this investigation also completed the **KC7 Security Analyst I** learning path: **7 of 7 modules (100%)**.
