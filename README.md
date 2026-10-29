## Windows Event Log Analysis

---

### Overview

In this lab, I used Windows logs to troubleshoot and identify multiple system issues. The main goal was to use **Event Viewer** to investigate errors and then apply troubleshooting techniques learned from previous IT Support labs.

The lab included five different issues involving:

* Updating outdated software
* Finding and deleting large or corrupted files
* Modifying file permissions
* Finding and terminating specific processes
* Using Windows logs to identify the source of problems

The main troubleshooting workflow was:

**Review Logs → Identify the Issue → Investigate → Apply a Fix → Verify the Fix**

---

### Tools & Resources

* Windows Virtual Machine (Qwiklabs)
* Windows Event Viewer
* Windows File Explorer
* Windows PowerShell
* VLC Media Player
* Windows file and folder permissions
* `taskkill` command
* Process IDs (PIDs)


### Lab Type:
Windows / IT Support Hands-On Lab

---
---

### 1. Start the Windows Lab

**1.** Start the Qwiklabs lab.

**2.** Click **Start Lab**.

**3.** Select **Open Windows VM**.

**4.** A Windows virtual machine will open in a new tab.

---

### 2. Open Windows Event Viewer

Windows **Event Viewer** is used to view system and application logs.

### Steps

**1.** Open the **Start** menu.

**2.** Search for:

```text
Event Viewer
```

![1](https://i.imgur.com/W2txQE5.png)


**3.** Open **Event Viewer**.

![2](https://i.imgur.com/FkGlU3O.png)

**4.** In the left panel, expand:

```text
Windows Logs
```

**5.** Select:

```text
Application
```

The application logs contain the logs used for this lab.

![2](https://i.imgur.com/hSAU6zg.jpeg)

---

### 3. Identify the Lab Errors

Scroll through the Application logs and look for entries that:

* Have a time close to when the lab was started
* Have **Qwiklab** as the **Source**

The lab contains five issues that need to be investigated and fixed.

---

### 4. Troubleshoot Low Disk Space

#### Problem

Find the log with:

```text
Source: Qwiklab
Event ID: 5
```

![4](https://i.imgur.com/z6fw5Xe.jpeg)

The message indicates that disk space is very low.

The log identifies a large file but does not provide the file name.

---

#### Find the Large File

Open **File Explorer**.

![5](https://i.imgur.com/yPja50S.png)

Navigate to:

```text
C:\
```

Click the search bar.

A **Search Options** menu will appear.

Select:

```text
Size → Gigantic
```

![6](https://i.imgur.com/bUb6SM8.png)

This searches for files larger than 4 GB.

Look through the results and identify the largest file.

In the lab, the file was approximately **10 GB**.

![7](https://i.imgur.com/jtmPiiy.png)

---

#### Delete the File

**1.** Right-click the large file.

**2.** Select **Delete**.

![8](https://i.imgur.com/HV8dK4s.png)

**3.** Click **Continue** if prompted.

**4.** Because the file is too large for the Recycle Bin, Windows will ask whether you want to permanently delete it.

**5.** Select **Yes**.

![9](https://i.imgur.com/3cklKxU.png)

#### Important Note

Deleting the file fixes the disk-space problem, but the original Event Viewer log will **remain**. Event logs are not automatically deleted after the underlying problem is fixed.

---

### 5. Remove a Corrupted File

#### Task

Navigate to the:

```text
Users
```

directory.

Find the file named:

```text
corrupted file
```

Delete the file.

![10](https://i.imgur.com/2NindWA.png)

#### Skill Demonstrated

* File navigation
* File identification
* File deletion
* Troubleshooting corrupted files

---

### 6. Update VLC Media Player

#### Steps

1. Open **VLC Media Player**.

2. Check for updates.

3. Install the available update.

![11](https://i.imgur.com/hA5tBu0.png)
![12](https://i.imgur.com/wtqUGvT.png)
![13](https://i.imgur.com/dYXvKTr.png)
![14](https://i.imgur.com/euFSUzk.png)
![15](https://i.imgur.com/fbkzW0p.png)

#### Skill Demonstrated

* Software maintenance
* Updating outdated applications
* Troubleshooting software-related issues

---

### 7. Find and Terminate a Process

#### Step 1: Open PowerShell

Open **Windows PowerShell**.

#### Step 2: Find the Process

Search for:

```text
totally_not_malicious
```

Identify its **Process ID (PID)**.

#### Step 3: Terminate the Process

Use:

```powershell
taskkill /F /PID [PROCESS ID]
```

#### Step 4: Verify

Search for the process again.

If the process no longer exists, the termination was successful.

![16](https://i.imgur.com/NZKhkOL.png)

#### Skill Demonstrated

* Process monitoring
* PID identification
* PowerShell
* Process termination
* Basic incident-response techniques

---

### 8. Modify File Permissions

#### Task

Navigate to:

```text
Users\Temp
```

Find:

```text
super_secret_file.txt
```

Grant **Write** permission to everyone.

After changing the permissions, verify that the new permissions were applied successfully.

![17](https://i.imgur.com/sQJ9BMA.png)

#### Skill Demonstrated

* Windows file permissions
* Access control
* Permission troubleshooting
* File security

---

### 9. Troubleshooting Workflow

The overall troubleshooting process used in this lab can be summarized as:

```text
1. Open Event Viewer
        ↓
2. Review Application Logs
        ↓
3. Identify Qwiklab Events
        ↓
4. Determine the Problem
        ↓
5. Investigate the Cause
        ↓
6. Apply the Appropriate Fix
        ↓
7. Verify the Fix
```

This is a useful workflow for IT Support and cybersecurity troubleshooting.

---
---

### Key Concepts

| Concept          | Description                                                      |
| ---------------- | ---------------------------------------------------------------- |
| Event Viewer     | Windows tool used to view system and application logs            |
| Event Log        | Record of events and errors generated by Windows or applications |
| Event ID         | Number used to identify a specific type of event                 |
| Source           | Application or service that generated the event                  |
| PowerShell       | Windows command-line and scripting environment                   |
| PID              | Process ID used to identify a running process                    |
| `taskkill`       | Windows command used to terminate processes                      |
| File Permissions | Rules controlling what users can do with files                   |
| Disk Space       | Available storage capacity on a system                           |

---
---

### Cybersecurity Relevance

Log analysis is an important skill for both **IT Support** and **SOC Analyst** roles.

In cybersecurity, analysts frequently investigate logs to identify:

* Failed or suspicious activities
* Application errors
* Unauthorized changes
* Abnormal processes
* System problems
* Potential security incidents

This lab introduced a basic version of the same workflow used in security monitoring:

```text
Collect Logs
     ↓
Review Events
     ↓
Identify Anomaly
     ↓
Investigate
     ↓
Take Action
     ↓
Verify
```

For a SOC Analyst, the ability to understand **what happened, when it happened, what caused it, and what action was taken** is essential.

---
---

### Troubleshooting Notes

#### Event Viewer contains many logs

Focus on entries that:

* Have **Qwiklab** as the source
* Were generated around the time the lab started
* Match the event IDs or problems described in the lab

#### Large files are difficult to find

Use:

```text
File Explorer → C:\ → Search → Size → Gigantic
```

#### A deleted problem still appears in Event Viewer

This is expected. Fixing the underlying issue does not remove the historical event from the log.

#### A process does not terminate

Verify that you are using the correct **PID** and run PowerShell with the appropriate permissions.

---
---

### Skills Demonstrated

* Windows Event Viewer
* Log analysis
* Troubleshooting
* Windows File Explorer
* File management
* Software maintenance
* PowerShell
* Process management
* PID identification
* `taskkill`
* File permissions
* Basic incident investigation

---
