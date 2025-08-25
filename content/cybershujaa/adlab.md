---
layout: page
title: Active Directory Lab Setup
date: 2024-06-12
author: c1ph3rbnuk
---
<img src="https://i1.wp.com/www.cloudcommunity.it/wp-content/uploads/2019/01/hero_windowsserver.jpg?fit=1920%2C1080&ssl=1" width="100%" height="auto">
So last time we introduced Active Directory, it's core components and also explained how authentication happens in Active Directory. Today, we will be building our lab right from installing the Windows Server to configuring AD Services, setting up a domain, adding users and group policies. Let's begin! :smiley:

### Lab Requirements
- 1 Windows Server. Either [Windows Server 2022](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2022) or [Windows Server 2019](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2019)
- 1 Windows Client Machines => [Windows 10 Enterprise](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-10-enterprise)
- At least 50GB of disk space
- At least 8GB of Memory
- Hypervisor => I'll be using [VirtualBox](https://www.virtualbox.org/)

Go ahead and install virtualbox and also download the ISO files.

### Installing Windows Server 2019
**Create a New Virtual Machine**    

Click "NEW" to create a a new VM and give it a name. Choose the Windows Server ISO file from your Downloads Path then click "Skip Unattended Installation"
<img src="../assets/images/cybershujaa/AD/vbox/setup1.png" width="100%" height="auto">
<br>
Next choose your memory space. 2GB should be enough.
<img src="../assets/images/cybershujaa/AD/vbox/memory.png" width="100%" height="auto">
<br>
Choose your disk space too. 25GB should be more than enough because we really are not going to create very large files inside the server.
<img src="../assets/images/cybershujaa/AD/vbox/disk.png" width="100%" height="auto">
<br>
Lastly Click Finish and start the machine.
<img src="../assets/images/cybershujaa/AD/vbox/finish.png" width="100%" height="auto">

<br>

**Setting Up** 

Once you the VM powers on the set up begins. Just follow the defaults selections. Select Language > Click Install.
On the operating system you want to install, make shure you select the `Windows Server Desktop Experience` because we want the Graphical Interface User(GUI) version.
<img src="../assets/images/cybershujaa/AD/vbox/gui.png" width="100%" height="auto">

<br>
Aggree on the terms and continue. For the type of installation, use the Custom Install because this is the first time we are installing a windows machine.
<img src="../assets/images/cybershujaa/AD/vbox/custom.png" width="100%" height="auto">

Click Next on everything else and let it install.
After everything installs you will be required to setup your Administrator Password. Make sure you note it down do that you don't forget it.

Finally you will have a similar screen to this after you've logged in!
<img src="../assets/images/cybershujaa/AD/init_setup.png" width="100%" height="auto">

<br>
Note that after successfull installation your screen will be small because you have not yet install the Geust Additions. Just install that from Devices > Install Guest Additions CD Image. Navigate to your This PC and you'll see a mounted VirtualBox Addditions drive. Run the setup64 executable and this will give you a for full screen display experience.

<br>

### What next?
After a successfull installation i renamed my PC into `ALLSAFE-DC` to signify it's a domain controller. I'll be using the Mr Robot theme for my namings throughout the setup.:see_no_evil:

### Installing the Active Directory Domain Services.  
The next thing we want to do is to install the Active Directory Domain Services on our Domain Controller.

Click **Add Roles and Features**  
<img src="../assets/images/cybershujaa/AD/addrole.png" width="100%" height="auto">

Click Next and Next...Then on the server roles, select the Active Directory Domain Services. Add it as a feature then install.
<img src="../assets/images/cybershujaa/AD/chooseADds.png" width="100%" height="auto">

<br>

The next is is that we want to make our server be the domain controller. After the service has been installed youll be prompted to promote it to become the domain controller. Click it.
<img src="../assets/images/cybershujaa/AD/promote.png" width="100%" height="auto">

<br>

Add a new forest then choose a name for your root domain. Again i will proceed with my theme `ECORP.local`. Click Next.
<img src="../assets/images/cybershujaa/AD/domain.png" width="100%" height="auto">

<br>

You will be required to type in the Administrator password that you set during installation. Enter it and click Next..Next..
<img src="../assets/images/cybershujaa/AD/admin.png" width="100%" height="auto">

<br>

A prerequisite check will be performed and after it passes successfully. you will click install.
<img src="../assets/images/cybershujaa/AD/check.png" width="100%" height="auto">

<br>

Your machine will restart immediately after the install and you will be able to login to the domain now as the Administrator.
<img src="../assets/images/cybershujaa/AD/login t domain.png" width="100%" height="auto">

<br>

### Installing the Active Directory Certificate Services
The Active Directory certificate services are used to provide digital certificates that can be used for things like Identity verification and encryption in Active Directory enviroments.
So on the Server Roles again select "Active Directory Certificate Services" and simply follow the default configuration to the end.
<img src="../assets/images/cybershujaa/AD/ADcertificate.png" width="100%" height="auto">
<img src="../assets/images/cybershujaa/AD/ca.png" width="100%" height="auto">
<br>

### Installing Windows 10 Workstation
This simple. Just follow the same setup process to where you will be required to create a microsoft account. You don't need to create one. Just proceed with creating a Local User.
<br>

### SetUp sor far
<img src="../assets/images/cybershujaa/AD/sofar.png" width="100%" height="auto">

<br>

### Setting Up Users, Groups and Policies
Last time we established that users are the main reason why we care about Active Directory. So, let's set up some users, group them and enforce some policies.
<img src="../assets/images/cybershujaa/AD/usermanagement.png" width="100%" height="auto">
<br>

We can notice that the Default users together with the Security group users like Domain Admins are all bundled together. We can tidy that up by separating them. We'll proceed to creating a "Group" organizational unit that will store all Security group users together.
<img src="../assets/images/cybershujaa/AD/groupou1.png" width="100%" height="auto">
<img src="../assets/images/cybershujaa/AD/users_separate.png" width="100%" height="auto">
<img src="../assets/images/cybershujaa/AD/securityg_users.png" width="100%" height="auto">
<br>

Next we'll create a two copies of the Administrator to clone another Admin user called Mr Robot and a service account called SQLService which will be sued to run the SQL Service. 
<img src="../assets/images/cybershujaa/AD/adminclone.png" width="100%" height="auto">

We can see below that Mr Robot and the SQLService account were created successfully. To fully setup the service account we will run the following commands on the command prompt.    

`setspn -a ALLSAFE-DC/SQLService.ECORP.local:1337 ECORP\SQLService`    

`setspn -T ECORP.local -Q */* `   

The first command adds a Service Principal Name to the SQLService account. SPNs are unique identifiers for services running on servers. This is used to ensure that Kerberos authentication can correctly identify and authenticate to the SQL Service running on SQLService.ECORP.local on port 1337.
The second command queries and lists all SPNs in the ECORP.local domain to check if the SPN was registered successfully.

<img src="../assets/images/cybershujaa/AD/setupserviceaccount.png" width="100%" height="auto">

Next we will create two other low level users Tyrell Wellic and Elliot ALderson.
<img src="../assets/images/cybershujaa/AD/lowleveluser.png" width="100%" height="auto">
<br>

### Creating a File Share
We are going to create a file share called `hackmeifyoucan` that we will abuse during our attacks in the later chapters.
<img src="../assets/images/cybershujaa/AD/fileshare.png" width="100%" height="auto">
<img src="../assets/images/cybershujaa/AD/fileshare1.png" width="100%" height="auto">
<br>

### Creating Group Policies
Lastly we will create Group Policy Object(GPO) for the whole domain, We could create GPOs for specific OU but we'll just create one for the whole domain. Our group policy will be to disable windows defender on our lab environment so that we can successfully run attacks withount having to care about the Windows Antivirus yelling to us "I've blocked a malware!!!"
<br>

Search for group policy in the search icon.
<img src="../assets/images/cybershujaa/AD/grouppolicy.png" width="100%" height="auto">
<br>

We can see there is already a Domain group policy. We can confirm the scope and it's our `ECORP.local` domain.
<img src="../assets/images/cybershujaa/AD/defaultdomainpolicy.png" width="100%" height="auto">
<br>

Create a GPO for the whole domain.
<img src="../assets/images/cybershujaa/AD/gpo.png" width="100%" height="auto">
<br>

Right click on it to edit the policy.
<img src="../assets/images/cybershujaa/AD/disablegpocreated.png" width="100%" height="auto">
<br>

Enable the "Turn Off Windows Defender Antivirus"
<img src="../assets/images/cybershujaa/AD/antivirus.png" width="100%" height="auto">
<br>

Lastly, make sure the policy is enforced!!
<img src="../assets/images/cybershujaa/AD/enforcepolicy.png" width="100%" height="auto">

<br>

### Joining our Machines to the Domains
Now it's time to join our client workstation to the domain. Before that, let's confirm our Domain Controller IP address.
<img src="../assets/images/cybershujaa/AD/ipdc.png" width="100%" height="auto">

<br>

We are going to configure the IP address of the Domain controller as the DNS server for our client machine so that it can be able to identify it on the network.
<img src="../assets/images/cybershujaa/AD/dnsserver.png" width="100%" height="auto">
<br>

We can now proceed to joining the domain.
<img src="../assets/images/cybershujaa/AD/joindomain.png" width="100%" height="auto">
<br>

We can confirm from the server that we have successfully joined the domain on Tools > Active Directory Users and Computers.
<img src="../assets/images/cybershujaa/AD/successjoin.png" width="100%" height="auto">
<br>

The next thing I did is to ensure that network discovery is enable and that we can access the `ALLSAFE-DC` network share.
<img src="../assets/images/cybershujaa/AD/enablenetdiscovery.png" width="100%" height="auto">
<img src="../assets/images/cybershujaa/AD/netshare.png" width="100%" height="auto">
<br>
<br>

And that's all for our lab setup. Meet me in the next article where we will start the fun part, Attacking our environment!:sunglasses: See ya!:v: