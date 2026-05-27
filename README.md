## Objective 
Investigate suspicious network and HTTP activity to identify potential reconnaissance, exploitation, and post-exploitation behavior.



## Initial Reconnaissance

During my analysis of network traffic and HTTP logs, I observed multiple requests originating from the same source IP address, indicating potential reconnaissance activity against the target system.

The traffic showed communication from source IP **10.251.95.4** to destination IP **10.251.96.5**. Analysis of port activity indicated that the attacker scanned ports **1–1024**, suggesting broad service discovery and early-stage reconnaissance.

Further investigation revealed the use of tools consistent with **Gobuster v3.0.1** and **sqlmap v1.4.7**, indicating automated enumeration and exploitation attempts.



## Credential Exposure

While analyzing HTTP POST requests and following the HTTP stream, I identified credentials being transmitted insecurely.

The password value `Admin%401234` was captured and decoded to `Admin@123`, confirming exposure of sensitive authentication data.


## Web Shell Upload and Execution

By filtering HTTP traffic using `http.request.method == POST`, I identified malicious file upload activity.

The attacker successfully uploaded a web shell named:

**dbfuncations.php**

This file was confirmed as the web shell used for remote command execution.



## Command Execution Analysis

The web shell accepted a command execution parameter:

- **Parameter:** `cmd`

The initial command executed was:

- `id`

This confirmed successful remote command execution on the compromised system.



## Post-Exploitation Activity

Further analysis indicated that the attacker established a reverse shell connection for persistent access.

- **Shell Type:** Reverse shell  
- **Port Used:** 4422



## Summary of Findings

- Reconnaissance activity detected (ports 1–1024 scanned)
- Use of Gobuster and sqlmap identified
- Credentials exposed in HTTP traffic
- Web shell uploaded: `dbfuncations.php`
- Remote command execution confirmed
- Reverse shell established on port 4422
