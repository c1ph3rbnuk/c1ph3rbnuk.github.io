---
title: Introduction to Logs.
date: 2023-08-05
series: ["Socs"]
series_order: 11
---
<img src="img/nolog.png" height="200px">

Logs are records about the events and activities occuring within a computer system, network or applications. These records provide a chronological account of what has happened within a system. It could be errors raised by an application or what was recently downloaded and when. 

Logs are the heart of SOC operations. They offer visibility on systems, devices, application, users activities within a network which empowers SOC analysts to monitor, detect and respond to suspicious activities.

<br>

`Log file -  a file containing log records.`  
`Logging - the act of keeping a log file. `

### Events
An event is any occurrence that the operating system (OS) or a program wants to keep track of or alert the user about.[cybertalents] Examples of events are:
- Logon Events - when a user login/logout of a computer system.
- User events - when an account is created in a system or a password is changed.

Event logs are special files that record important events on a computer system.

### Log types

- **Security Logs** - there track security related events like user logins, access control changes(permissions & roles) and security policy violations. 
- **System logs** - record system-level events such as startups, shutdowns and hardware changes.
- **Application logs** - record errors, crashes encountered by application and user interactions with an application.
- **Network logs** - these capture network related events such as networrk traffic(Ip address, ports and protocols), successfull connections, blocked requests and network firewalls activity.
- **Web Server logs** - record details about HTTP requests, responses and accessed resources. It also captures issues encountered by the web server while processing requests.

### Event classification
This is the process of categorizing various events and event data based on a specific criteria. Events are classified as:  
- Error - error events indicate a significant problem such a failure in system or application. they require immediate attention and respone to restore functionality. 
- Warning - these signify potential issues that may lead to a problem in the future.
- Informational - these just provide status updates like a successfull login or a successful system update.

### Log attributes
- **Timestamp** - the date and time when the event occurred.
- **Source** - the application, system or component that generated the event.
- **User/Entity** - the user or process responsible for the event.
- **Description** - a brief detail of what happened.