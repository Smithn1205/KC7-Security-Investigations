# Investigation 01: CloutHaus — Social Media Leads to Compromise

## Overview

This was one of the first longer investigations I completed in the KC7 Security Analyst I path.

The scenario starts with suspicious activity involving a CloutHaus employee and gradually develops into a broader account-compromise investigation. I used KQL to move between employee information, authentication activity, web traffic, passive DNS, and email-related evidence.

What I found useful about this investigation was learning not to rely on one suspicious event by itself. A strange login becomes much more meaningful when it lines up with unusual geography, an outdated User-Agent, reconnaissance activity, and later abuse of the compromised account.

## What I Investigated

I worked through several types of activity, including:

- identifying the employee and their normal system information
- reviewing suspicious authentication events
- comparing the source IP with the employee's expected location
- examining the User-Agent used during the suspicious login
- using Passive DNS to investigate infrastructure
- reviewing inbound website activity for reconnaissance
- identifying searches aimed at collecting personal information
- looking for signs that the compromised email account was being abused

## Investigation Approach

My general workflow was:

1. Start with the employee record to establish the username, hostname, IP address, and other baseline information.
2. Review authentication activity for anything that did not fit the expected pattern.
3. Pivot from suspicious IP addresses into DNS and network logs.
4. Review website activity to understand what the actor was researching.
5. Correlate the web activity with the compromised user.
6. Check for follow-on activity involving the user's email account.

This helped me understand the value of pivoting between tables instead of treating each log source separately.

## Example KQL

### Find the employee record

```kusto
Employees
| where name contains "Afomiya"
| project name, username, email_addr, hostname, ip_addr, user_agent, mfa_enabled
```

### Investigate activity from a suspicious IP

```kusto
InboundNetworkEvents
| where src_ip == "<suspicious IP>"
| project timestamp, src_ip, url
| order by timestamp asc
```

### Review Passive DNS for an IP

```kusto
PassiveDns
| where ip == "<suspicious IP>"
| project timestamp, domain, ip
```

### Search reconnaissance activity

```kusto
InboundNetworkEvents
| where src_ip == "<suspicious IP>"
| where url contains "Afomiya"
| project timestamp, url
| order by timestamp asc
```

## What I Learned

The biggest takeaway for me was how quickly several individually small indicators can build a much stronger picture.

A suspicious IP address by itself might not be enough. But when the same activity also involves an unusual country, an outdated browser, targeted searches about an employee, and account abuse, the compromise becomes much clearer.

I also got more comfortable using KQL operators such as:

- `where`
- `contains`
- `contains_cs`
- `project`
- `distinct`
- `count`
- `order by`

## Skills Demonstrated

- Authentication investigation
- KQL filtering and pivoting
- IP and domain analysis
- Passive DNS review
- Web reconnaissance analysis
- OSINT-related threat identification
- Account-compromise investigation

## Note

This investigation was completed using a guided KC7 training scenario. I have intentionally summarized the investigation rather than publishing every challenge question and answer.
