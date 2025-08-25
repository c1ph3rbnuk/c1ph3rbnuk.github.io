---
layout: page
title: SMB
date: 2024-06-02
author: c1ph3rbnuk
---

### What is SMB?

The Server Message Block(SMB) protocol is a network communication protocol designed by IBM primarily for sharing files, printers and other resources over the network. This protocol is widely used by the Windows Operating system for file sharing. SMB operates on port 139(NetBIOS over TCP/IP) and directly on port 445 by default and follows the client-server architecture for communication.    

<img src="../assets/images/cybershujaa/smb.webp" width="100%" height="auto">

> _NetBIOS(Network Basic Input and Output Service) is a legacy protocol that allows applications in different computers to communicate over LAN._    

Currently, the latest version of SMB is version 3.1.1 which is more secure and uses stronger encryptions compared to the previous versions SMB1 ans SMB2. SMB exploitation is very common. One of the imfamous attacks, the Wannacry Ransomware, back in 2017 took advantage of a vulnerability within the implementation of the SMBv1 (EternalBlue CVE-2017-0144) to remotely execute arbtrary code infecting thousands of computers over 150 countries including critical infrastructure such as the UK National Health Service.    

Other popular SMB vulnerabilities existing include SMBGhost(CVE-2020-0796) in SMBv3 that allows for remote code execution by exploiting a buffer overflow within the compression feature of the protocol, SMBBleed(CVE-2020-1206) also in SMBv3 that allows ann attacker to leak kernel memory of the server leading to sensitive data exposure.    

### SMB Enumeration
SMB enumeration refers the process of gathering information about the target system using the SMB protocol. This could include trying to identify any shared files/resources over the network. It is a very process during reconnaissance that can help uncover potential attack vectors(entry points). It could also reveal some user aaccounts in the system.

#### Port scanning
First we try to identy if port 139,445 are open.  

<img src="../assets/images/cybershujaa/smbservice.png" width="100%" height="auto">

We can then use the default sccript `-sC` and try to enumerate the two services for more information. 

<img src="../assets/images/cybershujaa/basicscript.png" width="100%" height="auto">

We can also try to list the shares using the `smbclient` tool. From the screenshot below, we are not able to anonymously list the shares. 

<img src="../assets/images/cybershujaa/smblist.png" width="100%" height="auto">

The next step we could take is ti enumerate the services using the nmap smb scripts `/usr/share/nmap/scripts/smb*`