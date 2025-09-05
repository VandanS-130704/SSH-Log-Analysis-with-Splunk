# SSH-Log-Analysis-with-Splunk

## 🎯 Objective

In this project:
1. I learned how to ingest and analyze SSH logs using Splunk.
2. I detected failed and successful SSH authentication attempts.
3. I identified unusual SSH activity that may indicate brute-force or unauthorized access.

---

## 🖥️ Lab Setup

- ✅ **Splunk**: Already installed and accessible.
- ✅ **Data Source**: JSON-formatted Zeek-style SSH logs.
- 🌐 **Log File**: Download and upload to Splunk using the steps below.

📥 **[Download SSH Log file](https://drive.google.com/file/d/1-KEqITwCOoQSRS3SfnPk-bbwdnOfFNsB/view?usp=sharing)**

---

## ⚙️ Steps to Upload SSH Log into Splunk

1. Go to Splunk Web → **Settings > Add Data**.
2. Choose **Upload** and select `synthetic_zeek_ssh.json`.
3. Set Source type: `json` or create a new one `zeek:ssh`.
4. Index: Choose `main` or create a new index like `ssh_lab`.
5. Finish the upload and confirm indexing.

---

## 🔍 Project Tasks

Used SPL queries to complete the following analysis:

### ✅Task 1: Listed the top 10 endpoints with failed SSH login attempts
```spl
index="main" source="ssh_logs.json" auth_success=false
| stats count by "id.orig_h"
| sort -count
| head 10
```
### ✅Task 2: Found the number of total SSH connections
```spl
index="main" source="ssh_logs.json"
| stats count as total_ssh_connections
```
### ✅Task 3: Counted all event types (successful, failed, no-auth, multiple-failed) seen in the logs
```spl
index="main" source="ssh_logs.json"
| stats count by event_type
```
