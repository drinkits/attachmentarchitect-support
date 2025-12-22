# Attachment Architect - User Guide
## Smart Attachment Management for Jira Cloud

**Version:** 3.29.0  
**Last Updated:** January 2025

---

## 📖 Table of Contents

1. [What is Attachment Architect?](#what-is-attachment-architect)
2. [Getting Started](#getting-started)
3. [Running Your First Scan](#running-your-first-scan)
4. [Understanding the Dashboard](#understanding-the-dashboard)
5. [Analyzing Your Data](#analyzing-your-data)
6. [Action Center - Cleaning Up Duplicates](#action-center---cleaning-up-duplicates)
7. [Storage Hygiene - Removing Trash Files](#storage-hygiene---removing-trash-files)
8. [Security Risks - Finding Sensitive Files](#security-risks---finding-sensitive-files)
9. [Settings & Configuration](#settings--configuration)
10. [Audit Trail](#audit-trail)
11. [Trial vs. Paid Features](#trial-vs-paid-features)
12. [Troubleshooting](#troubleshooting)
13. [FAQ](#faq)
14. [Support](#support)

---

## What is Attachment Architect?

Attachment Architect helps Jira administrators **eliminate storage waste** by finding and removing duplicate attachments and **low‑value trash files** (logs, dumps, temp, system). It's like having a smart assistant that:

*   🔍 **Scans** your site with a two‑phase engine (unified progress + ETA)
    
*   🧭 **Scopes** by entire site or selected projects (no JQL required)
    
*   📊 **Analyzes** storage usage across 7 dimensions
    
*   🎯 **Identifies** duplicates and "Frozen Dinosaurs" (large files on old issues)
    
*   🧹 **Cleans** duplicates and trash with safe, bulk actions
    
*   🛡️ **Detects** security risks (PII, credentials, sensitive files)
    
*   📝 **Tracks** everything in an enterprise audit log
    

### Why You Need It

*   **Save Money:** Reduce storage costs by 20-40% on average
    
*   **Improve Performance:** Faster backups and better Jira performance
    
*   **Stay Compliant:** Full audit trail for GDPR and compliance requirements
    
*   **Enhance Security:** Find and remediate sensitive files before they become incidents
    
*   **Save Time:** 2 hours vs. 2 weeks of manual cleanup

---

## Getting Started

### Prerequisites

- **Jira Cloud** instance (any plan)
- **Jira Administrator** role
- **5 minutes** for initial setup

### Installation

1. Go to **Atlassian Marketplace**
2. Search for **"Attachment Architect"**
3. Click **"Try it free"** or **"Buy now"**
4. Click **"Get it now"** to install
5. Wait for installation to complete (30-60 seconds)

### Accessing the App

1. In Jira, click **⚙️ Settings** (top right)
2. Click **"Apps"** in the left sidebar
3. Click **"Attachment Architect"** in the Apps menu

**Or use the direct URL:**
```
https://your-site.atlassian.net/jira/settings/apps/attachment-architect
```

---

## Running Your First Scan

### Step 1: Configure Scan Scope

1. Open **Attachment Architect** from Jira Settings
2. Click **"Start the Audit"**
3. **Choose Scope**:
   - **Entire Site**: Scan all projects (recommended for first scan)
   - **Selected Projects**: Choose specific projects to scan
4. Review estimated issue count
5. Click **"Confirm & Start Scan"**

> **Pro Tip:** Start with a full site scan to get the complete picture, then use project scoping for targeted re-scans.

### Step 2: Monitor Progress

The scan runs in two phases:

**Phase 1: Mapping the Territory (0-5%)**
- Collects issue IDs from Jira API
- Progress may appear slow but backend is working hard
- Safe to close window - scan continues in background

**Phase 2: Analyzing Issues (5-100%)**
- Processes each issue and its attachments
- Shows real-time progress and ETA
- Displays processing speed (issues/second)

**Scan Duration:**
- **Small instances** (< 1,000 issues): 30 seconds - 1 minute
- **Medium instances** (1,000 - 10,000 issues): 2-5 minutes
- **Large instances** (10,000+ issues): 5-15 minutes

**What happens during a scan:**
- ✅ Two‑phase engine collects issue IDs, then analyzes in parallel
- ✅ Reads attachment metadata (filename, size, upload date, author)
- ✅ Calculates file hashes (SHA‑256) to identify duplicates
- ✅ Analyzes storage patterns by project, user, file type, age, status
- ✅ Detects trash files (logs, dumps, temp files)
- ✅ Identifies security risks (sensitive filenames)
- ❌ **Never reads file contents** (privacy‑first design)

### Step 3: View Results

Once complete, you'll see:
- **Total storage** used by attachments
- **Duplicate storage** that can be reclaimed
- **Trash storage** (logs, dumps, temp files)
- **Waste percentage** (duplicates + trash / total)
- **Quick Wins** – Top 3 highest‑impact duplicate groups
- **Scope badge** – Which projects the results reflect

---

## Understanding the Dashboard

### Global Statistics (Top Cards)

```
┌─────────────────┬─────────────────┬��────────────────┬─────────────────┬─────────────────┐
│  Digital Hoard  │  Déjà Vu Data   │ Digital Landfill│  Panic Level    │    On Fire 🔥   │
│    50.2 GB      │    15.3 GB      │     8.2 GB      │      47%        │   23.5 GB       │
└─────────────────┴─────────────────┴─────────────────┴─────────────────┴─────────────────┘
```

- **Digital Hoard:** Total attachment storage used
- **Déjà Vu Data:** Space wasted by duplicate files
- **Digital Landfill:** Space wasted by trash files (logs, dumps, temp)
- **Panic Level:** Waste percentage (duplicates + trash / total)
- **On Fire 🔥:** Potential savings (duplicates + trash combined)

### Scope Badge

Shows which projects are included in the current scan results:
- **"Entire Site"** - All projects scanned
- **"3 Projects"** - Specific projects scanned (click to see list)

### Quick Wins Table

Shows the **top 3 individual files** with the most duplicates:

| File Name | Duplicates | Wasted Space | Pain Level | Action |
|-----------|------------|--------------|------------|--------|
| requirements.pdf | 49 copies | 245 MB | 🔥🔥🔥 | View Details |
| screenshot.png | 38 copies | 152 MB | 🔥🔥 | View Details |
| design.sketch | 25 copies | 125 MB | 🔥 | View Details |

**Tip:** Start here for maximum impact with minimum effort!

---

## Analyzing Your Data

### Visual Analysis Tabs

Click the **"Visual Analysis"** tab to explore your data across 7 dimensions:

#### 1. Project Bloat Map

**What it shows:** Storage usage per project with treemap visualization

**Use it to:**
- Identify which projects consume the most space
- Find "zombie projects" with no recent activity
- Plan project archival strategies
- See garbage ratio (waste %) per project

**Color coding:**
- 🟢 Green: Clean (< 15% waste)
- 🟡 Yellow: Messy (15-30% waste)
- 🔴 Red: Hoarder (> 30% waste)

#### 2. File Type Analysis

**What it shows:** Storage breakdown by file extension with bubble chart

**Use it to:**
- Understand what types of files are most common
- Identify oversized file types (videos, ZIPs)
- Set policies based on file type
- See average file size per type

**Bubble size** = Average file weight. Large bubbles in top-right = storage bullies.

#### 3. Storage Hoarder Leaderboard (By User)

**What it shows:** Storage usage and waste percentage per user

**Use it to:**
- See which users upload the most files
- Identify "Ctrl+C / Ctrl+V" award winners (highest duplicate ratio)
- Track duplicate upload patterns
- Plan user training

**Features:**
- Top 5 Quota Busters (by total storage)
- Top 5 highest waste percentage users

#### 4. Digital Archaeology (By Age)

**What it shows:** Storage by file age with stacked bar chart

**Use it to:**
- Find old files for archival ("Paleozoic Era" = 2+ years)
- Implement retention policies
- Identify stale attachments
- See waste percentage by age bracket

**Age brackets:**
- 0-90 days (Freshly Minted)
- 90-365 days (This year)
- 1-2 years
- 2-4 years
- 4+ years (The Paleozoic Era)

#### 5. Workflow Analysis (By Status)

**What it shows:** Storage by issue status with smart grouping

**Use it to:**
- See how much storage is in completed issues
- Identify bottlenecks (storage stuck in "Backlog")
- Optimize workflow efficiency
- Find issues to archive

**Smart grouping:** Shows top in-progress statuses, groups others as "Other In Progress"

#### 6. Frozen Dinosaurs (Heat Index)

**What it shows:** Large files on old issues (highest cleanup priority)

**Use it to:**
- Find "set it and forget it" files
- Identify extinct projects
- Prioritize cleanup efforts
- See files by heat score (size × age)

**Priority levels:**
- 🦕 Frozen Dinosaurs (large + old)
- 🔥 Large Files (> 10 MB)
- 🕰️ Old Issues (> 1 year)
- ✅ Active Files

#### 7. Archive Candidates (Zombie Projects)

**What it shows:** Projects with no updates in 180+ days

**Use it to:**
- Identify projects for archival
- Contact project owners before cleanup
- Plan long-term storage optimization
- See "extinction event" candidates

---

## Action Center - Cleaning Up Duplicates

### Quick Wins Tab

**Best for:** Fast, high-impact cleanup

1. Review the list of duplicate files sorted by impact
2. Click **"View Details"** on any file
3. See all locations where the file appears
4. **Canonical file** (oldest) is marked with ✅ and kept safe
5. Select duplicates to delete (or use "Select All Duplicates")
6. Click **"Delete Selected"**
7. Confirm deletion

**What gets deleted:**
- ✅ All selected duplicate copies
- ❌ Canonical file (always kept safe)

**Safety features:**
- Type-to-confirm for bulk deletes
- Shows which file is canonical
- Links to all affected issues
- Full audit trail

### All Duplicates Tab

**Best for:** Comprehensive cleanup with advanced filtering

**Filters available:**
- **Search:** Filename or issue key
- **File Type:** .pdf, .png, .zip, etc.
- **Project:** Specific projects
- **Min Size:** Minimum file size

**Bulk deletion limits:**
- **Trial users:** Up to 20 files (lifetime limit)
- **Paid users:** Unlimited deletions

---

## Storage Hygiene - Removing Trash Files

**NEW FEATURE:** Automatically detect and remove low-value files

### What Are Trash Files?

Files that provide minimal value but consume storage:

- **Log Files:** *.log, *.trace, debug files, error logs
- **Database Dumps:** *.sql, *.dump, *.bak, backup files
- **Temporary Files:** *.tmp, *.temp, *.cache, *.old
- **Build Artifacts:** *.class, *.o, *.pyc, compiled files
- **Archives:** *.zip, *.tar, *.gz (when duplicates exist)

### How to Use Storage Hygiene

1. Open **Storage Hygiene** tab
2. Review detected trash files
3. Use filters to narrow down:
   - **Search:** Filename or issue key
   - **File Type:** Specific extensions
   - **Status:** Issue status
4. Select files using checkboxes
5. Click **"Download Backup"** (opens Jira Backup Manager)
6. After backup, click **"Permanent Delete"**
7. Confirm deletion

### Safety Features

- **Active Issue Warning:** Files on active issues highlighted in yellow
- **Backup Strategy Modal:** Directs you to Jira's native backup
- **Risk Acknowledgment:** Must acknowledge risks before deleting
- **Type-to-Confirm:** Extra confirmation for bulk deletes
- **Full Audit Trail:** Every deletion logged

### Best Practices

✅ **DO:**
- Always create a backup before mass deletion
- Review files on active issues carefully
- Start with small batches (10-20 files)
- Check issue status before deleting

❌ **DON'T:**
- Delete files without backup
- Ignore active issue warnings
- Delete files you're unsure about
- Rush through the process

---

## Security Risks - Finding Sensitive Files

**NEW FEATURE:** Detect files with potential security risks

### What Gets Detected?

Files identified by filename patterns:

**CRITICAL Severity:**
- Private keys (*.key, *.pem, id_rsa)
- Database dumps (*.sql, *.dump)
- Credentials files (.env, secrets.*)

**HIGH Severity:**
- Config files (*.conf, *.yaml, *.ini)
- AWS credentials
- API key files

**MEDIUM Severity:**
- Source code (*.js, *.py, *.java)
- Business documents (*.xlsx, *.docx)
- Log files

**LOW Severity:**
- Backup files (*.bak, *.backup)
- Archives (*.zip, *.tar)
- Text files

### Deep Content Scanning (Optional)

For text files < 5MB, enable deep scanning to search for:
- Passwords
- AWS Keys
- Bearer Tokens
- Credit Cards (Luhn validation)
- SSNs
- Internal IPs

**Enable in Settings → Security & Scanning → Real-Time Upload Scanner**

### How to Use Security Risks

1. Open **Security Risks** tab
2. Review summary cards (Critical, High, Medium, Low)
3. Click severity card to filter
4. For each file:
   - Click **"Review Content"** to scan (if scannable)
   - Click **"Download"** to inspect locally
   - Navigate to issue to remediate
5. Take action:
   - Delete file if confirmed sensitive
   - Move to secure location
   - Update issue with remediation notes

### Important Notes

- **Read-Only View:** Security Risks tab is for awareness only
- **No Direct Deletion:** Remediate through issue management
- **Privacy-First:** Only scans filenames by default
- **Opt-In Content Scanning:** Deep scanning must be enabled in Settings

---

## Settings & Configuration

### Accessing Settings

1. Open **Attachment Architect**
2. Click the **"Settings"** tab

### Available Settings

#### 1. Scan Scope Configuration

**What it does:** Define which projects to scan

**Options:**
- **Entire Site:** Scan all projects (default)
- **Selected Projects:** Choose specific projects

**How to configure:**
1. Go to Settings → Scan Scope
2. Select scope type
3. If "Selected Projects", choose projects from list
4. Click "Save Scope"

#### 2. On-Issue Visibility (Activity Panel)

**What it does:** Shows deletion history on Jira issues

**Options:**
- ✅ **Enabled:** Activity panel appears on issues with deletion history
- ❌ **Disabled:** Stealth mode (default)

**How to enable:**
1. Go to **Settings** tab
2. Toggle **"Show Attachment Activity Panel"** to ON
3. Click **"Save Settings"**

**What users see:**
- Panel on issues where files were deleted
- What was deleted, when, by whom, why
- Link to canonical file (if accessible)

**"Ghost Protocol":** When disabled, existing panels show placeholder but hide data

#### 3. Security & Scanning

**What it does:** Enable real-time upload scanning for sensitive content

**Options:**
- ✅ **Enabled:** Scan every text file upload (< 5MB)
- ❌ **Disabled:** Filename-only detection (default)

**How to enable:**
1. Go to Settings → Security & Scanning
2. Toggle **"Enable Real-Time Upload Scanner"** to ON
3. Click "Save Settings"

**Scanner Specs:**
- Scan Cap: 5 MB (physics is real)
- Targets: Text files (logs, code, JSON, SQL)
- Detection: High sensitivity (credit cards, AWS keys, private keys, SSNs)
- Engagement Rules: Observe & Report (file remains attached, alarms go off)

#### 4. Dinosaur Definitions (Heat Index Thresholds)

**What it does:** Calibrate criteria for "Dead Weight"

**Settings:**
- **Large File Threshold:** Files larger than X MB (default: 10 MB)
- **Ancient History Threshold:** Issues older than X days (default: 365 days)

**How to configure:**
1. Go to Settings → Dinosaur Definitions
2. Enter thresholds (1-1000 MB, 1-3650 days)
3. Click "Update Rules"

---

## Audit Trail

### Viewing Audit Logs

1. Open **Attachment Architect**
2. Scroll to **"The Paper Trail"** section in Settings tab

### What's Logged

Every action is recorded with full context:

| Action | Details Logged |
|--------|----------------|
| **Scan Started** | Who, when, scan ID, scope |
| **Scan Completed** | Duration, files found, duplicates detected, waste % |
| **Scan Cancelled** | Who, when, progress at cancellation |
| **Scan Failed** | Error message, context |
| **Files Deleted** | Who, what, when, where, why, count |
| **Settings Changed** | What changed, old value, new value, who |

### Filtering Logs

Use filters to find specific events:

- **Action Type:** Scan, Deletion, Settings
- **User:** Filter by who performed the action
- **Issue Key:** Actions related to specific issues
- **Date Range:** Specific time period

### Expandable Details

Click the **▶** arrow to expand event details:
- Full context for each action
- Before/after values for settings changes
- List of affected issues for deletions
- Waste percentage indicators for scans

### Pagination

- Configurable items per page (10, 25, 50, 100)
- Navigate between pages
- Shows range (e.g., "Showing 1 to 25 of 150 entries")

---

## Trial vs. Paid Features

### Free Trial (30 Days)

✅ **Included:**
- Full dashboard access
- Unlimited scans
- All analytics and visualizations
- Security risk detection
- Audit trail
- Up to **20 file deletions** (lifetime limit)

❌ **Limited:**
- Deletion limit: 20 files total
- After limit reached, app becomes read-only

### Paid Subscription

✅ **Everything in trial, plus:**
- **Unlimited deletions**
- **Priority support**
- **Regular feature updates**
- **No restrictions**

### Checking Your Trial Status

Look for the banner at the top of the dashboard:

```
🎁 Trial: 15 days remaining | 5 of 20 deletions used
```

### What Happens After Trial?

**Option 1: Subscribe**
- Click **"Subscribe"** in the banner
- Choose your plan
- Continue using all features

**Option 2: Don't Subscribe**
- App becomes **read-only**
- You can still:
  - ✅ View dashboard
  - ✅ Run scans
  - ✅ See analytics
  - ✅ View security risks
  - ✅ View audit logs
- You cannot:
  - ❌ Delete files
  - ❌ Change settings

---

## Troubleshooting

### Scan Issues

#### Scan is Stuck

**Symptoms:** Progress bar not moving for 10+ minutes

**Solutions:**
1. Refresh the page (scan continues in background)
2. Wait 5 more minutes (large instances take time)
3. Check Phase 1 reassurance banner (collecting IDs is slow)
4. Check Jira status page for outages
5. Contact support if still stuck after 30 minutes

#### Scan Failed

**Symptoms:** Error message appears

**Solutions:**
1. Click **"Start New Scan"** to retry
2. Check if you have admin permissions
3. Verify Jira instance is accessible
4. Contact support with error message

#### Can't Cancel Scan

**Symptoms:** Cancel button not working

**Solutions:**
1. Wait for current batch to complete (up to 5 minutes)
2. Refresh page to see updated status
3. Scan will auto-cancel at next checkpoint

### Deletion Issues

#### "Permission Denied" Error

**Cause:** You don't have DELETE_ATTACHMENTS permission

**Solution:**
1. Ask your Jira admin to grant you permission
2. Or ask them to perform the deletion

#### "Trial Limit Exceeded" Error

**Cause:** You've used all 20 trial deletions

**Solution:**
1. Subscribe to unlock unlimited deletions
2. Or wait for trial to end and subscribe

#### Deletion Succeeded But File Still Visible

**Cause:** Browser cache or Jira indexing delay

**Solution:**
1. Hard refresh the page (Ctrl+F5 or Cmd+Shift+R)
2. Wait 1-2 minutes for Jira to update
3. Check if file is actually gone (try to download it)

### Dashboard Issues

#### Dashboard Shows "No Data"

**Cause:** No scan has been run yet

**Solution:**
1. Click **"Start the Audit"**
2. Wait for scan to complete
3. Dashboard will populate automatically

#### Numbers Don't Match Jira

**Cause:** Scan data is outdated

**Solution:**
1. Run a new scan to refresh data
2. Dashboard shows data from last completed scan
3. Check scope badge - may be scanning subset of projects

#### Stale Data Mode

**Symptoms:** Banner says "Showing data from previous scan"

**Explanation:** This is normal during re-scans. Dashboard shows last completed results until new scan finishes.

**Solution:** Wait for scan to complete, then data auto-refreshes.

---

## FAQ

### General Questions

**Q: Does the app read my file contents?**  
A: No (by default). We only read metadata (filename, size, upload date). Deep content scanning is opt-in and only for text files < 5MB.

**Q: Is my data secure?**  
A: Yes. All data stays in your Jira instance. We use Atlassian Forge (SOC 2, ISO 27001 certified).

**Q: Can I undo a deletion?**  
A: No. Deletions are permanent. Always review carefully and create backups before deleting.

**Q: How often should I scan?**  
A: Monthly for most instances. Weekly for high-activity instances. After major migrations or cleanups.

**Q: Can I scan specific projects only?**  
A: Yes! Use the Scan Scope feature in Settings to select specific projects.

### Technical Questions

**Q: How long does a scan take?**  
A: 2-5 minutes for 10,000 issues. Scales linearly with instance size.

**Q: Does scanning affect Jira performance?**  
A: No. Scans run in the background with minimal impact. Uses scheduled triggers every 5 minutes.

**Q: What happens if I close the browser during a scan?**  
A: Scan continues in the background. Refresh the page to see progress.

**Q: Can multiple admins use the app?**  
A: Yes. All Jira admins can access the app. Actions are logged per user.

**Q: What's the difference between duplicates and trash files?**  
A: Duplicates are exact copies of the same file. Trash files are low-value files (logs, dumps, temp) regardless of duplication.

### Security Questions

**Q: What security risks does the app detect?**  
A: Filename-based detection (config files, keys, dumps) by default. Optional deep content scanning for passwords, API keys, credit cards, SSNs.

**Q: Does deep scanning read all my files?**  
A: No. Only text files < 5MB when explicitly enabled in Settings. Binary files are never scanned.

**Q: Can I delete files directly from Security Risks tab?**  
A: No. Security Risks is read-only for awareness. Remediate through issue management.

### Billing Questions

**Q: How much does it cost?**  
A: See pricing on the Atlassian Marketplace listing.

**Q: Can I cancel anytime?**  
A: Yes. Cancel through Atlassian billing. No long-term contracts.

**Q: What happens if I cancel?**  
A: App becomes read-only. Your data remains accessible but you can't delete files.

**Q: Do you offer refunds?**  
A: Follow Atlassian's standard refund policy (typically 30 days).

---

## Support

### Getting Help

**📧 Email Support:**
- Submit a ticket: https://drinkits.atlassian.net/servicedesk/customer/portal/34
- Response time: Within 24 hours (weekdays)

**📚 Documentation:**
- User Guide: This document
- Privacy Policy: See Marketplace listing
- Release Notes: See version history

**🐛 Report a Bug:**
1. Go to support portal
2. Click "Report a Bug"
3. Include:
   - What you were doing
   - What happened
   - Screenshots (if applicable)
   - Browser and Jira version

**💡 Request a Feature:**
1. Go to support portal
2. Click "Feature Request"
3. Describe your use case
4. We review all requests monthly

### Before Contacting Support

**Please try these first:**
1. ✅ Refresh the page
2. ✅ Check this user guide
3. ✅ Run a new scan
4. ✅ Verify you have admin permissions
5. ✅ Check Jira status page

**When contacting support, include:**
- Your Jira instance URL
- App version (shown in dashboard)
- What you were trying to do
- Error message (if any)
- Screenshots

---

## Quick Reference

### Common Tasks

| Task | Steps |
|------|-------|
| **Run a scan** | Dashboard → "Start the Audit" → Choose Scope → Confirm |
| **View duplicates** | Action Center → Quick Wins tab |
| **Delete duplicates** | View Details → Select files → "Delete Duplicates" |
| **Remove trash files** | Storage Hygiene → Select files → Download Backup → Permanent Delete |
| **Check security risks** | Security Risks tab → Review by severity |
| **Check trial status** | Look at banner at top of dashboard |
| **Enable Activity Panel** | Settings → Toggle ON → Save |
| **Configure scan scope** | Settings → Scan Scope → Select projects → Save |
| **View audit log** | Settings → Scroll to "The Paper Trail" → Apply filters |

### Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl/Cmd + R` | Refresh dashboard |
| `Esc` | Close modal |
| `Tab` | Navigate between fields |
| `Enter` | Confirm action |

### Best Practices

✅ **DO:**
- Run scans monthly
- Review Quick Wins first
- Check canonical file before deleting
- Create backups before mass deletion
- Provide deletion reasons for audit trail
- Enable Activity Panel for transparency
- Review security risks regularly
- Use project scoping for targeted scans

❌ **DON'T:**
- Delete files without reviewing
- Run multiple scans simultaneously
- Ignore trial limit warnings
- Delete canonical files manually
- Delete trash files without backup
- Ignore active issue warnings
- Rush through security risk remediation

---

## Glossary

**Attachment:** A file uploaded to a Jira issue

**Canonical File:** The original file we keep (oldest upload)

**Duplicate:** An exact copy of a file (same content, different location)

**Hash:** A unique fingerprint of a file's contents (SHA-256)

**Quick Win:** A high-impact duplicate file (many copies, large size)

**Scan:** The process of analyzing all attachments in your Jira instance

**Storage Waste:** Space consumed by duplicate files and trash files

**Trial Limit:** Maximum deletions allowed during free trial (20 files)

**Trash Files:** Low-value files (logs, dumps, temp) that consume storage

**Frozen Dinosaurs:** Large files on old issues (highest cleanup priority)

**Heat Index:** Priority score based on file size × issue age

**Scope:** Which projects are included in scan (entire site or selected)

**Stale Data Mode:** Dashboard shows previous scan results during re-scan

**Deep Content Scanning:** Optional feature to scan file contents for sensitive data

**Security Risk:** File with potential security concerns (PII, credentials, etc.)

---

## Version History

### v4.0.0 (January 2025)
- ✅ Storage Hygiene: Detect and bulk delete trash files (logs, dumps, temp, system)
- ✅ Security Risks: Detect sensitive files by filename patterns
- ✅ Deep Content Scanning: Optional scanning for PII, credentials, secrets
- ✅ Project Scoping: Scan entire site or selected projects
- ✅ Unified Progress Bar + ETA for all scans
- ✅ Stale Data Mode: Uninterrupted dashboard during re-scans
- ✅ Enhanced Audit Log: Expandable details, email on hover
- ✅ Cancel Scan: Graceful cancellation with progress preservation
- ✅ Heat Index Improvements: Scatter chart visualization
- ✅ User Analysis: Email display on hover
- ✅ Witty IT-Savvy tone throughout UI

### v3.15.0 (November 2024)
- ✅ Unified progress bar + ETA (incl. first scans)
- ✅ Stale‑data mode for uninterrupted dashboards
- ✅ Project scoping (scan entire site or selected projects)
- ✅ Heat Index improvements and Quick Wins polishing
- ✅ Audit log enhancements

### v3.0.0 (January 2024)
- ✅ Activity Panel settings fix
- ✅ Enhanced security (SAST + SCA scans)
- ✅ Production deployment
- ✅ Improved error handling

### v2.0.0 (December 2023)
- ✅ Bulk deletion (up to 100 files)
- ✅ Trial limit enforcement
- ✅ Dashboard real-time updates
- ✅ Comprehensive audit logging

### v1.0.0 (November 2023)
- ✅ Initial release
- ✅ Basic scanning and analytics
- ✅ Duplicate detection
- ✅ Manual cleanup

---

## Legal & Compliance

**Privacy:** See our [Privacy Policy](PRIVACY_POLICY.md)

**Security:** 
- SAST scan: 0 vulnerabilities
- SCA scan: Backend clean
- GDPR & CCPA compliant
- SOC 2 & ISO 27001 certified (via Forge)

**Data Processing:**
- Data controller: Your organization
- Data processor: Atlassian
- Sub-processor: drinkits DEV

---

**🎉 You're all set! Start optimizing your Jira storage today.**

**Questions?** Contact support: https://drinkits.atlassian.net/servicedesk/customer/portal/34

---

*Last updated: January 2025 | Version 3.29.0*
