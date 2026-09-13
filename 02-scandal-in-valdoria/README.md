# Investigation 02: A Scandal in Valdoria — A Political Mystery

## Overview

This investigation was much larger than CloutHaus and was the first KC7 scenario where I felt like I was following a more complete intrusion from one stage to another.

The investigation involved email activity, malicious file downloads, endpoint file creation, PowerShell activity, persistence, remote access tooling, discovery commands, collection, archive creation, and eventual data exfiltration.

Rather than looking at one alert, I had to keep moving between different log sources and build a timeline of what the attackers did.

## Investigation Flow

The investigation covered activity such as:

1. reviewing suspicious emails and senders
2. identifying links and document downloads
3. confirming files appearing on disk
4. reviewing process execution after the download
5. identifying PowerShell activity
6. finding scheduled-task persistence
7. investigating `plink.exe`
8. identifying attacker discovery commands
9. following file movement and renaming
10. identifying 7-Zip archive creation
11. tracing data exfiltration using `curl`

This was useful because it showed how an incident can move from an email into endpoint activity and then into data theft.

## Log Sources I Used

- `Employees`
- `Email`
- `OutboundNetworkEvents`
- `FileCreationEvents`
- `ProcessEvents`
- `PassiveDns`

## Example KQL

### Find email activity from a domain

```kusto
Email
| where sender has "weprinturstuff.com"
| distinct sender
| count
```

### Find unique URLs visited by an IP

```kusto
OutboundNetworkEvents
| where src_ip == "<user IP>"
| distinct url
| count
```

### Confirm a downloaded document appeared on disk

```kusto
FileCreationEvents
| where hostname == "<hostname>"
| where filename endswith ".docx"
| order by timestamp asc
| project timestamp, hostname, filename, path
```

### Look for PowerShell scripts written after a document download

```kusto
FileCreationEvents
| where hostname == "<hostname>"
| where filename endswith ".ps1"
| order by timestamp asc
```

### Investigate process activity around a script

```kusto
ProcessEvents
| where hostname == "<hostname>"
| where process_commandline contains ".ps1"
| project timestamp, process_name, process_commandline
| order by timestamp asc
```

### Find scheduled-task creation

```kusto
ProcessEvents
| where hostname == "<hostname>"
| where process_commandline contains "schtasks"
| where process_commandline contains "/create"
| project timestamp, process_commandline
```

### Search for Plink execution

```kusto
ProcessEvents
| where hostname == "<hostname>"
| where process_commandline contains "plink"
| project timestamp, process_name, process_commandline
```

### Find discovery activity

```kusto
ProcessEvents
| where hostname == "<hostname>"
| where process_commandline contains "whoami"
   or process_commandline contains "ipconfig"
   or process_commandline contains "arp"
   or process_commandline contains "tasklist"
   or process_commandline contains "net view"
| project timestamp, process_commandline
| order by timestamp asc
```

### Find archive creation using 7-Zip

```kusto
ProcessEvents
| where hostname == "<hostname>"
| where process_commandline contains "7z"
| project timestamp, process_commandline
| order by timestamp asc
```

### Find curl-based upload activity

```kusto
ProcessEvents
| where hostname == "<hostname>"
| where process_commandline contains "curl"
| project timestamp, process_commandline
| order by timestamp asc
```

## What I Learned

This investigation helped me understand why timeline building matters.

At first, events such as a document download, a PowerShell process, `schtasks.exe`, `plink.exe`, 7-Zip, and `curl` can look like separate pieces of activity. Once they are placed in chronological order, they tell a much clearer story.

I also learned the difference between checking:

- **network access** with `OutboundNetworkEvents`
- **whether a file actually appeared on disk** with `FileCreationEvents`
- **what executed afterward** with `ProcessEvents`

That distinction was especially useful when validating whether a suspicious link resulted in an actual downloaded file.

## ATT&CK Behaviors Observed

The scenario included behavior consistent with several common attacker techniques:

- Phishing / malicious file delivery
- PowerShell execution
- Scheduled task persistence
- Remote access / tunneling with Plink
- System and account discovery
- File and directory discovery
- Archive collection using 7-Zip
- Exfiltration over web protocols using `curl`

I treated the ATT&CK mapping as a way to organize the behavior rather than as the starting point of the investigation.

## Skills Demonstrated

- Email investigation
- KQL query development
- Network and endpoint correlation
- File creation analysis
- Windows process analysis
- PowerShell investigation
- Persistence identification
- Discovery command analysis
- Data staging and archive analysis
- Exfiltration investigation
- Timeline reconstruction

## Note

This investigation was completed using a guided KC7 training scenario. I have not reproduced the full challenge or every answer. The purpose of this write-up is to document the investigative process and the security concepts I practiced.
