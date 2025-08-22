---
title: Endpoint Security
date: 2023-07-21
series: ["Socs"]
series_order: 6
---
<img src="img/endpoint.png" width="600">

An endpoint is any device that is connected to a network; from laptops, PCs, servers, smart phones to all IoT devices and more. The number of endpoints in networks today has exploded. Todays' policies like BYOD(Bring Your Own Device) that allow employees to use their personal devices to access co-operate resources together with the remote workforces which has recently become the new norm - have greatly increased the attack surface.  
- `Attack surface refers to a potential entry points and weaknesses that attackers could use to gain unauthorised access to systems. Basically all ways to break into a system.`


 __Every endpoint connected to the co-operate network is a gateway for cyber criminals to inflict more pain.__

### What is Endpoint Security?
Endpoint security is the approach to protect and secure all these devices that connect to the network from cyber threats. It includes the tools and technologies set to detect and defend the end-user devices from all sorts of malicious activity.

### Endpoint Security Controls
1. **Host Based Intrusion Detection System**(HIDS) - this is a system that monitors and analyses activities on an endpoint device based on predefined signatures(characteristics that identify specific known threats) and alerts security personel. It also logs those activities for further later investigation. One example of a popular HIDS is [OSSEC](https://ossec.net).

2. **Host Based Intrusion Prevention System**(HIPS) - this system is simillar to HIDS but with added ability to take actions like blocking and shutting down identified threats to contain them.

3. **Anti-Virus(AV) Products** - Also known as Anti-virus softwares, they protect devices from malwares and viruses. There are 2 types of AV solutions:
- Signature Based - these operate on a large database of "known-bad" malware signatures. Its detection involves comparing files and applications against these signatures and if a match hits they have the ability to delete that file, alert the user or take appropriate action. Note that a solution like this that relies on a list of signatures for known malicious files isn't so efficient in identifying new and previously unknown attacks(Zero day exploits). 
- Behavior Based - this other type focuses on analyzing the behavior of programs rather than relying on predefined signatures. This AV type documents the normal activity and then monitors the system to identify any software that can be performing any abnormal activities and then takes an action against it[cybertalents].

4. **Host Based Firewalls** - unlike network firewalls that protect the entire network, host based firewalls are designed to secure a single endpoint such as a PC. They have the ability to control applications communicating over the network. Endpoint firewalls can block ports, filter traffic based on predefined rules and generate logs and alerts whenever they detect security threats. These logs are valuable for further forensics analysis.

5. **EndPoint Detection and Response(EDR)** - this is an advanced technology with similar functionality as HIDS and HIPS. EDRs offer continous  monitoring, analysis of endpoint activities and collection of all these data. It has the ability to contain incidents and take actions like alerting and stoping malicious programs. In cases of confirmed attacks this tool has the ability to isolate all infected machines from the network. This tool works to reduce the attacker's dwell time and to speed the Incident response process.(We'll talk about the Incident Response process in future!)   
**Components of an EDR**
* Data collection agents - these are softwares that collect data like file changes, processes running and network activities from the endpoints.
* Automated Response rules - these are pre-configured rules that identify whether a certain activity is a threat or not and automatically take an action against it [cybertalents].
* Forensics Tools - these are tools used by security analysts to investigate incidents or even to perform a threat-hunting process [cybertalents].
6. **Vulnerability Management and Compliance** - this is a process that involves scanning endpoints regularly and performing vulnerability assesments to identify potential weakness and mitigate them before the attacker does. Offense in the best defense. Types of vulnerability scans:
- External Vulnerability scans -  this scan is performed with zero privileges to the system and it aims to identify possible entry points from the attackers view.
- Internal Vulnerability scan - this type of scan is done inside the organization's network where the scanner already has an access to the system. It covers even co-operate devices that are not accessible over the internet.

**Compliance Scanning** - when something is compliant, it means it meets all the required standards and regulations set in it's specific context. Compliance scanning focuses on industry's regulatory requirements. An example of these regulations is HIPAA(Health Insuarance Portability and Accountability) which sets guidlines and requirements for maintaining privacy of individual's health information. Compliance scan should be done regulary to ensure all endpoints meet the necessary regulatory obligations.
 
 <br>

Endpoint  security is very critical. And, safeguarding individual devices from the cyber adversaries is yet another way to strengthen the organization's overall cybersecurity resillience. In future series we'll discuss **OSSEC** ; an open source Host Based Intrusion Detection System and also talk about the Linux Firewall and how we can utilize the **iptables** utility to write firewall rules to deny traffic. But before that, we are going to shift to something new next time -- the fascinating world of Web Security -- how to protect web applications that are open to the world. We will start slow with how web works but ramp fast to the top ten web attacks and how to mitigate them.

See you next time! :smiley: