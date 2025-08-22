---
title: SIEM
date: 2023-08-11
---
![](img/user.png)

Security Information and Event Management is a solution for managing an organization security posture by providing a centralized platform that monitors and consolidates multiple security related events withing an orgnization's network. The SIEM solution build up from 2 key components.  
- **Security Information Management(SIM)** - this involves collecting all data from different log sources and end devices in the organizational network(firewall logs, system logs, application logs, web logs..etc) then stores them in a central repository or database where it can later be analyzed.
- **Security Event Management(SEM)** - SEM focuses on monitoring, evaluating and correlating events as they occur. this helps in identifying occurences of suspicious events like(unauthorised logins) in real time thus improving the incident response process.


### SIEM Components
1. **Log collection & Aggregation** - involves collecting, parsing and normalizing logs and event data from various sources(end user devices, network devices, servers, etc) using special programs called agents.  
2. **Log Management** - responsible for receiving log data from different sources, indexing and storing in a central repository ready to be accessible for analysis.  
3. **Security Monitoring** - this involves analyzing event data against pre-defined correlation rules to identify patterns and alert when unusual activities occur. Consider a scenario where you would like to detect a brute-force attach against a web server. Brute-force attack happens when an attacker repeatedly tries multiple usernames and passwords till they gain unauthorised access. A correlation rule here could perhaps be configured to detect multiple login failures on an account withing a short period of time and trigger an allert.   
4. **Visualization and Analytics** - this involves representing recurity events in visual form and dashboards. Visual representstions like charts and graphs offer direct insights when analyzing data and helps monitoring security trends and metrics.   
5. **Icident Response** - SIEMs may offer tools to facilitate incident management procedures. This may involve forensics analysis on host or containment and isolation of infected devices.
6. **Threat Intelligence** - SIEMs may integarate with threat intelligence feeds to enrich the analysis process by providing more information about the attacks like the tactics and tecniques used.

<br>

### Architecture

Image...

<br>

### Tools
There are a dozen of SIEM tools in the industry today. Some are free and others are paid. They all basically try to achieve the same thing but what really differentiates them is their data collection reach and correlation.

- **SPLUNK** - 
- **IBM Qradar** -
- **Log Rhythm** -
- **ELien Vault** -
- **Elastic Serch** - 


Next time we'll take a practical look on one of these tools; Splunk. We'll learn what it is, how it's deployed and how it's used. See ya :smiley:
