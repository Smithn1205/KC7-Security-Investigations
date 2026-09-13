# Investigation 03: VirusTotal Fundamentals

## Overview

This module was different from the previous KC7 investigations because the focus was not mainly on querying a log dataset. Instead, I spent the investigation working directly in **VirusTotal** and learning how to move through a file report without relying only on the detection ratio.

I worked with several Windows samples and used the different VirusTotal tabs to build context around them. This included checking file metadata and certificate information, comparing vendor detections, reviewing crowdsourced rules, pivoting through related domains and IP addresses, and looking at sandbox behavior such as file, registry, and process activity.

The biggest takeaway for me was that a VirusTotal verdict is only one part of the investigation. A file with few detections can still be suspicious, while a legitimate-looking filename or certificate does not automatically make a file safe.

## What I Investigated

During the module I practiced:

- distinguishing legitimate Windows files from suspicious or renamed samples
- reviewing hashes, file type, version information, and certificate details
- interpreting antivirus detection results without treating the detection ratio as the final answer
- understanding how **masquerading** can make malicious activity appear legitimate
- reviewing **crowdsourced YARA** and **Sigma** detections
- using sandbox behavior to inspect file, registry, process, and service activity
- identifying persistence-related behavior in Windows
- pivoting from files to domains and IP addresses through the **Relations** tab
- using passive DNS to connect suspicious infrastructure
- using VirusTotal community comments, collections, and graphs as additional threat-intelligence context
- connecting observed behavior to MITRE ATT&CK techniques

## Investigation Workflow

My general workflow became:

1. Start with the file hash and check the basic metadata.
2. Review the detection ratio and compare how different security vendors classify the sample.
3. Check file version information and certificate/signing details rather than trusting the filename alone.
4. Review crowdsourced YARA and Sigma rules for additional indicators.
5. Move into **Relations** to identify connected files, domains, IP addresses, and infrastructure.
6. Pivot on suspicious indicators and compare dates to build context.
7. Review **Behavior** to see what the sample actually did in a sandbox.
8. Use community comments and collections when they provide useful context that automated analysis may have missed.
9. Map important behavior back to ATT&CK where it helps explain the technique.

## YARA vs. Sigma

One distinction that became much clearer during this module was the role of YARA and Sigma:

- **YARA** rules are mainly used to identify patterns and characteristics in files or malware samples.
- **Sigma** rules describe suspicious activity in logs and can be translated into SIEM-specific detection logic.

That helped connect VirusTotal analysis back to the detection work I am already practicing with KQL and SIEM data.

## ATT&CK Concepts Encountered

Some of the ATT&CK concepts I worked with included:

- **Masquerading — T1036**
- **DLL Search Order Hijacking — T1574.001**
- **Malvertising — T1583.008**

I used ATT&CK as a way to describe behavior after understanding what the sample was doing, rather than treating the technique ID as the starting point.

## What I Learned

The most useful part of the module was learning to treat VirusTotal as an investigation platform rather than simply a place to paste a hash and read a red/green score.

For example, I learned to ask:

- Is the filename consistent with the file metadata?
- Is the file signed, and what can the certificate actually tell me?
- Do the detection engines agree with each other?
- Are there useful YARA or Sigma matches?
- What files, domains, or IP addresses are related to the sample?
- What did the sandbox observe in the file system, registry, and process tree?
- Is the malware using anti-analysis techniques that may limit what the sandbox can see?
- Do community comments or collections provide context that the automated report does not?

That is a much more useful approach than relying on a single detection number.

## Skills Demonstrated

- VirusTotal file analysis
- File reputation and metadata review
- Code-signing and certificate analysis
- Malware triage
- YARA and Sigma awareness
- Sandbox behavior analysis
- Windows registry analysis
- Process-tree analysis
- Passive DNS investigation
- Indicator pivoting
- Threat-intelligence enrichment
- MITRE ATT&CK mapping

## Note

This investigation was completed through the guided **KC7 VirusTotal Fundamentals** module. I have summarized the methodology and concepts I practiced rather than reproducing the module's challenge questions and answers.
