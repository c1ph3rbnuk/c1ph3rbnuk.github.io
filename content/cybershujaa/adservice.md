---
layout: page
title: Active Directory Overview
date: 2024-06-11
author: c1ph3rbnuk
---

### What is Active Directory?
<img src="../assets/images/cybershujaa/msad.png" width="100%" height="auto">
`"Imagine you work in a medium-size organization—about 3000 users, each with a PC, and 300 servers. Each user needs access to multiple servers. You wouldn’t even want to think about the chaos, never mind the work, involved in trying to manage user logon accounts and permissions across all of those individual systems. And by the time you get to organizations with 10,000, 50,000, or even 100,000 users, it’s impossible to manage each computer individually.`

Active Directory (AD) provides a centralized service that links all of those machines and enables a user to log on and access any of them provided they have been granted permission to do so." ~ Richard Siddaway(Active Directory in a Month of Lunches)

It is an Identity Management Service that let's you centrally manage user accounts, computer accounts and the different permissions each has on network resources. It organizes information into hierachical structures(folders within folders...) which helps is categorizing and managing different objects.
<br>

### Active Directory Components
1. **Physical Components**
- Domain Controller - A domain controller is a server within the domain that has AD Domain Services installed. It hosts a copy of the AD database (ntds.dit) and the SYSVOL share (containing logon scripts and Group Policy data files). Domain controllers respond to authentication attempts by users and computers.
- Active Directory Domain Service Data Store - contains the database files and processes that store and manage directory info for user, services and applications.    

2. **Logical COmponents**    
a. **_Objects_** - Every object has an associated set of attributes.
    - Users - they are the main reason why we care about active directory. Everyone logging into the network will require a user account.
    - Computers - they are a special form os user accounts that help authenticate computers to the network and establish trust relation ships between the computer and the domain.
    - Contacts - used primarity to assign email addresses to external users.
    - Groups - used to simplify the administration of access control
    - Printers - used to simplify the process of locating and connecting to printers.   

b. **Schema** - it is basically a blueprint of the entire enterprise environment. It defines every type of object that can be stored in the directory. It also enforces rules regarding object creation and configuration through constraints of values and mandatory attribute requirements.    

c. **Domain** - used to group and manage objects in an organization. An administrative boundary for applying policies to groups of objects. It is also an authentication/authorization boundary that provides a way to limit the scope of access to resources.    

d. **Organizational Unit(OU)** - An organizational unit (OU) is a container within a domain that can be used to hold user,
computer, group, and other OU objects. There are two main reasons to create an OU:
    - To control the delegation of administrative privileges—that is, a certain group of administrators can only control the users, groups, and computers in a certain OU.
    - To control the application of Group Policy.    

e. **Tree** - it is a hierarchy of domains. Domains within a tree share a common schema, a common configuration partition, and the enterprise admins and schema admins groups. They enable trusts between all domains in the forest.    

f. **Forest**  - this the whole off your active directory. It can contain more than one domain organized in trees.

g. **Trusts** - Different domains are linked together by trust. One of the commin types of trust is transitive e.g if A trusts B and B trusts C, then A also trusts C.

<br>

### Authentication in Active Directory
Active Directory Primarily uses Kerberos for authentication. Kerberos is an authentication protocol with the following steps. The Authentication is based on tickets. 
<img src="https://academy.hackthebox.com/storage/modules/74/Kerb_auth.png" width="100%" height="auto">
Domain Controllers have a Kerberos Key Distribution Center (KDC) that issues tickets. 
- When a user initiates a login request to a system, the client they are using to authenticate requests a ticket from the KDC, encrypting the request with the user's password. If the KDC can decrypt the request (AS-REQ) using their password, it will create a Ticket Granting Ticket (TGT) and transmit it to the user. 
- The user then presents its TGT to a Domain Controller to request a Ticket Granting Service (TGS) ticket, encrypted with the associated service's NTLM password hash. 
- Finally, the client requests access to the required service by presenting the TGS to the application or service, which decrypts it with its password hash. 
If the entire process completes appropriately, the user will be permitted to access the requested service or application.
~[HackTheBox]

#### Kerberos Authentication Analogy
Imagine you are attending a VIP hackathon called "GlobalHack" that only invited members can participate because winners are going to be awarded a job in NSA. 

1. **Registration and Check in(CLient Authentication)** - you arrive at the venue and you flash a wide smile to the registrar. :smiley: You proceed to say "Hello, I'm here for the hackathon event!" The registrar says, "Welcome, but i need to verify your identity first. Please show me your invitation." You present your invitation and the registrar scans it to validate your details. "Wow! Mr Robot, Congratulations! Here is your VIP badge :name_badge: and may the best Hacker win!" (That's simmilar to getting the ticket granting ticket. The badge prooves you are a verified attendee and you can access different challenge booths.)

2. **Choosing a challenge booth(Service Request)** - you enter the hackathon room and you notice various challnge booths ranging cryptohacks, Forensics and many more. You decide that you're going for the cryptohacks. I mean, why not. You like makng sense out of nonsense. So, you approach the booth manager and say, "I'd like to join the cryptohacks challenge." Naima the cryptohacks booth manager says "Please show me your VIP badge first." You then present your badge and she nods approvingly saying, "Mr Robot, it's trully a skill of great men to make sense out of nonsense! Here is a pass :key: that you will use to unlock the crypto challenges! Goodluck!"(This is similar to the domain controller issuing you with the ticket granting service ticket which will be required to access a particular service in this case the crypto challenges)

3. **Accessing the challenges(Service Access)** - You approach the challenge area and one of the organizers asks you for the password to access the challenges in which you present it to him. He says, "All set, Start Hacking" pointing you to one super computer :computer: where you can start solving the challenges.

#### NTLM Authentication
This is an older authentication supported in Active Directory for compatibility reasons. NTLMv1 uses the LM hash while NTLMv2 uses the NTLM hash. LAN Manager(LM) hashes are the oldest password storage used by windows os and are stored in the NTDS.dit database on a domain controller. They are very weak and easy to crack. NTLM hashes are the mordern ones with improved security. However they can still be easily bruteforced with tools like Hashcat.
<figure><img src="https://academy.hackthebox.com/storage/modules/74/ntlm_auth.png" width="100%" height="auto">Image from HTB</figure>



### Lightweight Directory Access Protocol(LDAP)
This is another protocol(port 389) used in AD for accessing directory information services. LDAP runs securely over SSL on port 636.
<figure><img src="https://academy.hackthebox.com/storage/modules/74/LDAP_auth.png" width="100%" height="auto">Image from HackThebox</figure>

<br>
<br>

That's all for today! Next we will look at How to set up our Lab environment i.e installing Windows Server, configuring a domain, adding users and implementing group policies. See ya :wave: