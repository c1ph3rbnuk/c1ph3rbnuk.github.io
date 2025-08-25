---
layout: page
title: Access Control Security
date: 2024-06-10
author: c1ph3rbnuk
---

### What is Access Control Security?
<img src="../assets/images/cybershujaa/no-acess.jpg" width="100%" height="auto">

> _"Access control is a security technique that regulates who or what can view or use resources in a computing environment[TechTarget]."_    

This is important to protect the confidentiality, integrity and availability of data.

#### Types of Access Controls
Access controls are of two types `Physical` and `Logical`.
- **`Physical Access Controls:`** - these focus on physical security, restricting physical access to buildings, datacenters, etc. It protects all company's sensitive areas from unauthorized access. This is achieved through gates and locks, security guards, identification badges, biometric systems, CCTV cameras etc.

- **`Logical Access Controls`** - these are measures set to regulate access to difgital resources such as file shares, networks and system files. They include authentication, authorization and identification protocols.
<br>
<br>

### Authentication, Authorization and Accounting
AAA is an access control framework that combines:    
1. Authentication - veryfying and validating users that they truly are who they say they are using credentials like usernames and passwords. However there are 3 types of Authentications:
    - Something you know - Passwords, Pins, Answers t security questions.
    - Something you have - Smart Cards, Tokens, Mobile Devices.
    - Something you are - Biometrics such as fingerprints, voice and face recognitions.
Using more than 1 os the above authentication processes is what is reffered to as MFA. 2FA uses two.
2. Authorization - determining what resources an authenticated user is permitted to view and access. This brings about priviledges and rights to resources as a user.
3. Accounting - this involves keeping track of the all users activity while logged in. This creates an audit trail of the user's actions in the system.
<br>
<br>

### Identity and Access Management(IAM)
Imagine a large technology company, say Google with thousands of employees, hundreds of departments and millions of sensitive cutomer data. Different employees need to access different systems and resources to perform their daily jobs e.g the HRs need to process payrolls while the Finance department needs to deal with financial records, same for the customer care service. However, we don't want the costomer care service employee to have all access to the information in the systems or maybe the HR see what the finance department are doing. How are we going to ensure that we have controll on what each user can and acnnot access?

The goal is to manage all these accounts, giving them different access rights so that everyone can oly see what they are allowed to see. That's where IAM comes in!

IAM is a framework of policies, processes and technologies that ensures the right individual has the appropriate access to a resource. 

#### IAM Components
<img src="../assets/images/cybershujaa/components.png" width="100%" height="auto">


### Access Control Models
There are 4 access control models:
- Discretionary Access Control (DAC) - in this type of access control, the owner of the file has the freedom to decide who can access their resources. Say Alice created a project folder, she can grant or deny accesss to the folder to any user she wants to.
- Mandatory Access Control (MAC) - in this type of access control, access is granted based on a pre-defined policy set by a central authority. Example, assume some government documents are classified into different levels; Confidential, Secret and Top Secret. You as a user John has a clearence level Secret. You cannot access Top Secret files even if the owner want's to grant you access. Untill your clearence level is elevated.
- Role-Based Access Control (RBAC) - here user are assigned roles(doctor, receptionist) and access is granted based on roles ather than individuals. Say if you are assigned the role of a doctor you can vire all patients records. But as a receptionist you cant.
- Attribute-Based Access Control (ABAC) - Attribute access grants permissions based on characteristics such as time of access and location. As an employee who works 9-5 you are only granted access to a resource during your work hours and if you try to access files past those hours you get denied. 

<br>
<br>

That's all for access control security principles. Next time we will look at some access control systems that are used to manage access such as the Active Directory Service. See ya! :relaxed: :v: