---
title: "Registry Forensics Cheatsheet"
weight: 2
draft: false
description: "A cheatsheet for the Windows Registry Forensics"
date: "2022-01-02"
tags: ["forensics", "registry", "windows"]
---

### The Registry
The Windows Registry located at **`Windows\System32\config`** is a large database that stores configuration settings for Microsoft Windows and its applications. It contains system settings, user preferences, and more.  

On a live system, the registry can be accessed using **`regedit`** (Registry Editor). Tools like **RegRipper** can be used to browse registry hives from image files.  

---

### Structure
The Registry is organized as a **tree structure** with keys and subkeys. The root is called `HKEY`, and it contains several subkeys representing different areas of the system.  

1. **Hives** – logical groups of keys and values.  
   - **HKLM (HKEY_LOCAL_MACHINE)** → Local machine configuration  
   - **HKCU (HKEY_CURRENT_USER)** → Current user configuration  
   - **HKCR (HKEY_CLASSES_ROOT)** → File associations & class definitions  
   - **HKU (HKEY_USERS)** → All user accounts  

2. **Keys** – containers that hold configuration data. Example: `HKLM\Software` (installed software info).  

3. **Subkeys** – child keys beneath a parent key.  

4. **Values** – name–value pairs holding specific configuration details.  

---

### Registry Forensics
The Windows Registry holds **artifacts** valuable in digital forensics. These reveal user activity, system info, device usage, and attacker traces.  

Below are common forensic registry keys:

---

## 🧑‍💻 User Activity

<table>
<thead>
<tr>
<th style="width:20%">Artifact</th>
<th style="width:35%">Registry Key</th>
<th style="width:45%">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>MRUs (Most Recently Used)</td>
<td><code>HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\RunMRU</code></td>
<td>Tracks programs run recently.</td>
</tr>
<tr>
<td>Typed Paths</td>
<td><code>HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\TypedPaths</code></td>
<td>Stores paths typed into File Explorer.</td>
</tr>
<tr>
<td>Recent File History</td>
<td><code>HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\OpenSaveMRU</code></td>
<td>Tracks recently opened/saved files via common dialogs.</td>
</tr>
<tr>
<td>Program Usage (UserAssist)</td>
<td><code>NTUSER.DAT\...\Explorer\UserAssist\{GUID}\Count</code></td>
<td>Counts program executions by the user.</td>
</tr>
<tr>
<td>Last Key Viewed</td>
<td><code>NTUSER.DAT\...\Applets\Regedit\LastKey</code></td>
<td>Last accessed key in Registry Editor.</td>
</tr>
<tr>
<td>LNK Files</td>
<td><code>HKCU\...\Explorer\RecentDocs</code></td>
<td>Shortcuts referencing files (even deleted ones). Useful for MAC times, original paths, volumes, etc.</td>
</tr>
<tr>
<td>Jump Lists</td>
<td>(AutomaticDestination / CustomDestination files)</td>
<td>Lists recently accessed files/programs by app. Tools: <i>jump_list_parser, jump_list_extractor</i>.</td>
</tr>
</tbody>
</table>

---

## ⚙️ System Information

<table>
<thead>
<tr>
<th style="width:20%">Artifact</th>
<th style="width:35%">Registry Key</th>
<th style="width:45%">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Advanced Settings</td>
<td><code>HKCU\...\Explorer\Advanced</code></td>
<td>File Explorer customization settings.</td>
</tr>
<tr>
<td>Computer Name</td>
<td><code>SYSTEM\ControlSet001\Control\ComputerName\ComputerName</code></td>
<td>System hostname.</td>
</tr>
<tr>
<td>Windows Version Info</td>
<td><code>HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion</code></td>
<td>Windows version and build details.</td>
</tr>
<tr>
<td>Installed Applications</td>
<td><code>HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\App Paths\</code></td>
<td>List of installed apps and executables.</td>
</tr>
<tr>
<td>Services</td>
<td><code>SYSTEM\ControlSet001\Services\</code></td>
<td>Installed services and drivers.</td>
</tr>
<tr>
<td>UAC Status</td>
<td><code>HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System</code></td>
<td><b>EnableLUA=1</b> → UAC enabled, <b>=0</b> → disabled.</td>
</tr>
<tr>
<td>Last Logged-in User</td>
<td><code>HKLM\...\Authentication\LogonUI\LastLoggedOnUser</code></td>
<td>Tracks the last user to log in.</td>
</tr>
</tbody>
</table>

---

## 💾 Devices & Storage

<table>
<thead>
<tr>
<th style="width:20%">Artifact</th>
<th style="width:35%">Registry Key</th>
<th style="width:45%">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Auto-Run Programs</td>
<td><code>HKLM/HKCU\...\Run, RunOnce</code></td>
<td>Programs launched at logon.</td>
</tr>
<tr>
<td>ShellBags</td>
<td><code>HKCU\SOFTWARE\Microsoft\Windows\Shell\BagMRU</code><br><code>HKCU\SOFTWARE\Microsoft\Windows\Shell\Bags</code></td>
<td>Folder view preferences. Reveals deleted folders. Tool: <i>ShellBags Explorer</i>.</td>
</tr>
<tr>
<td>Mounted Devices</td>
<td><code>HKLM\SYSTEM\CurrentControlSet\Enum\USBSTOR</code><br><code>HKLM\SYSTEM\MountedDevices</code></td>
<td>USB/device connection history.</td>
</tr>
<tr>
<td>SRUM Database</td>
<td><code>C:\Windows\System32\sru\SRUDB.dat</code></td>
<td>Tracks every executed application (even deleted ones). Tools: <i>srum_dump, srum_extractor</i>.</td>
</tr>
</tbody>
</table>

---

## 🌐 Network & Security

<table>
<thead>
<tr>
<th style="width:20%">Artifact</th>
<th style="width:35%">Registry Key</th>
<th style="width:45%">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Firewall Status</td>
<td><code>HKLM\SYSTEM\...\FirewallPolicy</code></td>
<td><b>EnableFirewall=1</b> → enabled, <b>=0</b> → disabled.</td>
</tr>
<tr>
<td>Remote Desktop</td>
<td><code>HKLM\SYSTEM\...\Control\Terminal Server</code></td>
<td>Contains RDP settings and status.</td>
</tr>
<tr>
<td>Shared Folders</td>
<td><code>HKLM\SYSTEM\...\LanmanServer\Shares</code></td>
<td>Information about shared resources.</td>
</tr>
<tr>
<td>Network Interfaces</td>
<td><code>HKLM\SYSTEM\...\Tcpip\Parameters\Interfaces</code></td>
<td>Network adapter configurations.</td>
</tr>
<tr>
<td>Network List</td>
<td><code>HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList</code></td>
<td>List of networks previously connected to.</td>
</tr>
<tr>
<td>User Accounts</td>
<td><code>HKLM\SAM\Domains\Account\Users\Names\</code></td>
<td>All local user accounts (including WDAGUtilityAccount).</td>
</tr>
<tr>
<td>Timezone</td>
<td><code>SYSTEM\ControlSet001\Control\TimeZoneInformation</code></td>
<td>System timezone settings.</td>
</tr>
<tr>
<td>Prefetch & Superfetch</td>
<td><code>HKLM\SYSTEM\...\PrefetchParameters</code><br><code>HKLM\SYSTEM\...\Superfetch</code></td>
<td>Performance data. Also useful for execution history.</td>
</tr>
</tbody>
</table>

---

### Summary
Registry forensics provides investigators with insights into user actions, system configurations, network history, device usage, and persistence mechanisms. Proper analysis can reveal attacker activity and digital evidence.  
