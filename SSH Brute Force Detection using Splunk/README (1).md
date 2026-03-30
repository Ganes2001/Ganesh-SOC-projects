 SSH Brute Force Detection & Log Analysis using Splunk

 Overview

This project demonstrates detection and analysis of SSH brute force
attacks using Splunk SIEM. It involves log ingestion, query-based
analysis, and identification of suspicious activities from SSH logs.

------------------------------------------------------------------------

Objectives

-   Monitor SSH authentication activity\
-   Detect brute force attacks\
-   Identify suspicious IP addresses\
-   Analyze successful and failed login attempts\
-   Build queries for SOC-level investigation

------------------------------------------------------------------------

Lab Setup

-   SIEM Tool: Splunk Enterprise\
-   Log Source: SSH logs (/var/log/auth.log)\
-   Environment: Virtual Machine (Kali Linux + Ubuntu)\
-   Attack Tool: Hydra (for brute force simulation)

------------------------------------------------------------------------

Project Workflow

1.  SSH service enabled on target system\
2.  Brute force attack simulated using Hydra\
3.  Logs collected and forwarded to Splunk\
4.  Queries executed to detect suspicious patterns\
5.  Analysis performed to identify attacker behavior

------------------------------------------------------------------------

Splunk Queries

Log Validation

index=ssh_logs \| stats count by event_type

### Failed Login Analysis

index=ssh_logs event_type="Failed SSH Login" \| stats count by id.orig_h

### Brute Force Detection

index=ssh_logs event_type="Multiple Failed Authentication Attempts" \|
stats count by id.orig_h, id.resp_h

###  Successful Logins

index=ssh_logs event_type="Successful SSH Login" \| stats count by
id.orig_h, id.resp_h

###  Unauthenticated Connections

index=ssh_logs event_type="Connection Without Authentication" \| stats
count by id.orig_h

###  Time-based Analysis

index=ssh_logs event_type="Connection Without Authentication" \|
timechart count by id.orig_h

------------------------------------------------------------------------

##  Key Findings

-   Multiple failed login attempts detected\
-   Repeated attempts from same IP (brute force pattern)\
-   Suspicious successful logins observed\
-   Unauthenticated connection attempts identified

------------------------------------------------------------------------

##  MITRE ATT&CK Mapping

-   T1110 -- Brute Force

------------------------------------------------------------------------

##  Screenshots

(Add screenshots here)

------------------------------------------------------------------------

##  Conclusion

This project successfully demonstrates detection of SSH brute force
attacks using Splunk. It highlights real-world SOC analyst tasks
including log analysis, threat detection, and investigation.

------------------------------------------------------------------------

##  Recommendations

-   Disable root login via SSH\
-   Implement strong password policies\
-   Enable account lockout mechanisms\
-   Use intrusion detection systems (IDS)\
-   Monitor logs continuously using SIEM
