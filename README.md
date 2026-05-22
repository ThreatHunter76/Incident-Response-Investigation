# SOC Incident Response Investigation Lab

## Project Overview

This project demonstrates a complete Security Operations Center (SOC) incident investigation using Splunk SIEM. The investigation focused on identifying and analyzing a phishing-led compromise involving suspicious authentication activity, malware execution, PowerShell abuse, Command & Control (C2) communication, and possible data exfiltration.

The objective of this project was to simulate a real-world SOC analyst workflow by correlating multiple log sources, identifying Indicators of Compromise (IOCs), reconstructing the attack timeline, and recommending containment and remediation actions.

---

# Project Objectives

- Investigate suspicious authentication activity
- Detect possible brute force or credential stuffing attempts
- Analyze malware execution behavior
- Investigate suspicious PowerShell activity
- Detect Command & Control communication
- Identify possible data exfiltration activity
- Correlate events across multiple log sources
- Develop incident response and containment recommendations

---

# Tools & Technologies Used

| Tool | Purpose |
|---|---|
| Splunk Enterprise | SIEM and log analysis |
| Sysmon | Process and endpoint telemetry |
| Microsoft Defender | Malware detection |
| Kali Linux | SOC lab environment |
| CSV Log Sources | Simulated enterprise logs |

---

# Log Sources Analyzed

- Windows Security Logs
- Sysmon Logs
- DNS Logs
- Defender Logs
- Network Traffic Logs
- Firewall Logs
- VPN Logs
- Helpdesk/User Reports

---

# Incident Summary

During the investigation, multiple failed login attempts were identified against the user account:

```text
j.adewale
A successful authentication event was later observed from the same external IP address, indicating a possible credential compromise.

Shortly afterward, a suspicious executable:

update_kb5031.exe

was executed from the user’s Temp directory by:

OUTLOOK.EXE

Further analysis revealed:

Encoded PowerShell execution
Suspicious DNS queries
Malware detection alerts
Large outbound HTTPS traffic
Possible Command & Control communication
Potential data exfiltration activity

The investigation concluded that the attack likely originated from a phishing email leading to malware execution and post-exploitation activity.

Key Indicators of Compromise (IOCs)
Malicious IP Addresses
185.193.88.71
45.77.91.203
197.210.77.19
Suspicious Domain
cdn-updates365.com
Malicious File
update_kb5031.exe
Suspicious PowerShell Indicators
-enc
-nop
-w hidden
Splunk Queries Used
Authentication Investigation
index=soc_lab EventCode=4625 OR EventCode=4624
Malware Investigation
index=soc_lab update_kb5031.exe
PowerShell Investigation
index=soc_lab powershell.exe
DNS Investigation
index=soc_lab cdn-updates365.com
Data Exfiltration Investigation
index=soc_lab BYTES_OUT>10000000
Attack Chain Identified
Phishing Email
↓
OUTLOOK.EXE
↓
update_kb5031.exe
↓
Encoded PowerShell Execution
↓
Suspicious DNS Queries
↓
Outbound HTTPS Traffic
↓
Possible Data Exfiltration
MITRE ATT&CK Techniques Observed
Tactic	Technique
Initial Access	Phishing
Credential Access	Brute Force / Credential Stuffing
Execution	PowerShell
Defense Evasion	Obfuscated/Encoded Commands
Command & Control	Application Layer Protocol
Exfiltration	Exfiltration Over Web Services
Containment Actions Recommended
Isolate the affected endpoint from the network.
Disable or reset compromised user accounts.
Block malicious IP addresses and suspicious domains.
Terminate malicious PowerShell and suspicious processes.
Remove the malicious executable from affected systems.
Re-enable endpoint protection and perform full malware scans.
Investigate for lateral movement and additional compromised hosts.
Preserve forensic evidence for further analysis.
Key Lessons Learned

This project demonstrated the importance of:

SIEM-based threat detection
Event correlation
Authentication monitoring
Process analysis
DNS investigation
PowerShell abuse detection
Network traffic analysis
Incident response workflow

The investigation also highlighted how attackers combine phishing, malware execution, PowerShell abuse, and encrypted outbound traffic to compromise enterprise environments.

Skills Demonstrated
SIEM Investigation
Threat Hunting
Log Correlation
IOC Identification
Malware Analysis
PowerShell Investigation
Incident Response
Network Traffic Analysis
Splunk Querying
SOC Workflow Analysis
Conclusion

This SOC investigation successfully identified a phishing-led compromise involving suspicious authentication activity, malware execution, encoded PowerShell abuse, suspicious DNS communication, and potential data exfiltration.

By correlating logs across multiple security sources, the attack timeline was reconstructed and critical Indicators of Compromise were identified. This project demonstrates practical SOC analyst investigation techniques and real-world incident response methodology using Splunk SIEM.