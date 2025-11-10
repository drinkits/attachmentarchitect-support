# Attachment Architect - User Guide
## Smart Attachment Management for Jira Cloud

**Version:** 3.15.0  
**Last Updated:** November 2025

---

## 📖 Table of Contents

1. [What is Attachment Architect?](#what-is-attachment-architect)
2. [Getting Started](#getting-started)
3. [Running Your First Scan](#running-your-first-scan)
4. [Understanding the Dashboard](#understanding-the-dashboard)
5. [Analyzing Your Data](#analyzing-your-data)
6. [Cleaning Up Duplicates](#cleaning-up-duplicates)
7. [Cleaning Up Trash Files](#cleaning-up-trash-files)
8. [Settings & Configuration](#settings--configuration)
9. [Audit Trail](#audit-trail)
10. [Trial vs. Paid Features](#trial-vs-paid-features)
11. [Troubleshooting](#troubleshooting)
12. [FAQ](#faq)
13. [Support](#support)

---

## What is Attachment Architect?

Attachment Architect helps Jira administrators **eliminate storage waste** by finding and removing duplicate attachments and **low‑value trash files** (logs, dumps, temp, system). It's like having a smart assistant that:

- 🔍 **Scans** your site with a two‑phase engine (unified progress + ETA)
- 🧭 **Scopes** by entire site or selected projects (no JQL required)
- 📊 **Analyzes** storage usage across 7 dimensions
- 🎯 **Identifies** duplicates and “Frozen Dinosaurs” (large files on old issues)
- 🧹 **Cleans** duplicates and trash with safe, bulk actions
- 📝 **Tracks** everything in an enterprise audit log

### Why You Need It

- **Save Money:** Reduce storage costs by 20-40% on average
- **Improve Performance:** Faster backups and better Jira performance
- **Stay Compliant:** Full audit trail for GDPR and compliance requirements
- **Save Time:** 2 hours vs. 2 weeks of manual cleanup

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

### Step 1: Start a Scan

1. Open **Attachment Architect** from Jira Settings
2. Click **Start New Scan**
3. Choose **Scope**: Entire site or one/more Projects
4. Confirm **Start Scan**

> During scans, a unified progress bar and ETA display status. You can keep using the dashboard thanks to **stale‑data mode**; it shows the last completed results until the new scan finishes.

### Step 2: Wait for Completion

- **Small instances** (< 1,000 issues): 30 seconds - 1 minute
- **Medium instances** (1,000 - 10,000 issues): 2-5 minutes
- **Large instances** (10,000+ issues): 5-15 minutes

**What happens during a scan:**
- ✅ Two‑phase engine collects issue IDs, then analyzes in parallel
- ✅ Reads attachment metadata (filename, size, upload date)
- ✅ Calculates file hashes (SHA‑256) to identify duplicates
- ✅ Analyzes storage patterns by project, user, file type, age, status, heat
- ❌ **Never reads file contents** (privacy‑first design)

### Step 3: View Results

Once complete, you'll see:
- **Total storage** used by attachments
- **Duplicate storage** and **Trash storage** that can be reclaimed
- **Waste percentage** (duplicates + trash / total)
- **Quick Wins** – Top 3 highest‑impact duplicate groups
- **Scope badge** – Which projects the results reflect

---

## Understanding the Dashboard

### Global Statistics (Top Cards)

```
┌─────────────────┬─────────────────┬─────────────────┬─────────���───────┐
│  Total Storage  │ Duplicate Waste │ Waste Percentage│ Potential Savings│
│     50.2 GB     │     15.3 GB     │      30.5%      │    €184/year    │
└─────────────────┴─────────────────┴─────────────────┴─────────────────┘
```

- **Total Storage:** All attachment space used
- **Duplicate Waste:** Space consumed by duplicate files
- **Waste Percentage:** How much of your storage is duplicates
- **Potential Savings:** Estimated yearly cost savings (at €0.10/GB/month)

### Quick Wins Table

Shows the **top 3 individual files** with the most duplicates:

| File Name | Duplicates | Wasted Space | Action |
|-----------|------------|--------------|--------|
| requirements.pdf | 49 copies | 245 MB | View Details |
| screenshot.png | 38 copies | 152 MB | View Details |
| design.sketch | 25 copies | 125 MB | View Details |

**Tip:** Start here for maximum impact with minimum effort!

---

## Analyzing Your Data

### Visual Analysis Tabs

Click the **"Visual Analysis"** tab to explore your data:

#### 1. By Project

**What it shows:** Storage usage per project

**Use it to:**
- Identify which projects consume the most space
- Find "zombie projects" with no recent activity
- Plan project archival strategies

**Example:**
```
PROJECT-A: ████████████████████ 15.2 GB (30%)
PROJECT-B: ████████████ 8.5 GB (17%)
PROJECT-C: ████████ 5.3 GB (11%)
```

#### 2. By File Type

**What it shows:** Storage breakdown by file extension

**Use it to:**
- Understand what types of files are most common
- Identify oversized file types (videos, ZIPs)
- Set policies based on file type

**Example:**
```
.pdf:  ████████████████ 12.3 GB (25%)
.png:  ████████████ 9.8 GB (20%)
.zip:  ████████ 6.5 GB (13%)
```

#### 3. By User

**What it shows:** Storage usage per user

**Use it to:**
- See which users upload the most files
- Identify power users vs. occasional uploaders
- Track duplicate upload patterns

**Example:**
```
John Smith:  ████████████████ 8.2 GB (16%)
Jane Doe:    ████████████ 6.5 GB (13%)
Bob Johnson: ████████ 4.3 GB (9%)
```

#### 4. By Age

**What it shows:** Storage by file age

**Use it to:**
- Find old files for archival
- Implement retention policies
- Identify stale attachments

**Example:**
```
0-90 days:   ████████████ 8.5 GB (17%)
90-365 days: ████████████████ 12.3 GB (25%)
1-2 years:   ████████████ 9.8 GB (20%)
2-4 years:   ████████ 6.5 GB (13%)
4+ years:    ████████████ 9.1 GB (18%)
```

#### 5. By Status

**What it shows:** Storage by issue status (To Do, In Progress, Done)

**Use it to:**
- See how much storage is in completed issues
- Identify bottlenecks (storage stuck in "Backlog")
- Optimize workflow efficiency (smart grouping shows top in‑progress statuses)

**Example:**
```
Done:        ████████████████████ 25.3 GB (50%)
In Progress: ████████████ 15.2 GB (30%)
To Do:       ████████ 9.7 GB (19%)
```

---

## Cleaning Up Duplicates

### Action Center

Click the **"Action Center"** tab to manage duplicates:

#### Quick Wins Tab

**Best for:** Fast, high-impact cleanup

1. Review the list of duplicate files
2. Click **"View Details"** on any file
3. See all locations where the file appears
4. Click **"Delete Duplicates"**
5. Confirm deletion

**What gets deleted:**
- ✅ All duplicate copies
- ❌ Canonical file (kept safe)

**Example:**
```
File: requirements.pdf (5 MB)
Canonical: PROJECT-123 (keep this)
Duplicates:
  ☑ PROJECT-124 (delete)
  ☑ PROJECT-125 (delete)
  ☑ PROJECT-126 (delete)
  ... 46 more
```

#### All Duplicates Tab

**Best for:** Comprehensive cleanup

1. Browse the complete list of all duplicate files
2. Use filters to narrow down:
   - **File Type:** .pdf, .png, .zip, etc.
   - **Project:** Specific projects
   - **Size:** Minimum file size
3. Select files to clean up
4. Click **"Bulk Delete"**

**Bulk deletion limits:**
- **Trial users:** Up to 20 files (lifetime limit)
- **Paid users:** Up to 100 files per operation (unlimited operations)

---

## Cleaning Up Trash Files

**Best for:** Quick, low‑risk savings

1. Open **Storage Hygiene**
2. Review categories: **Logs**, **Dumps**, **Temp**, **System**
3. Select files (checkboxes) and click **Delete Selected**
4. Watch progress; success/failure counts are shown

**Safety:**
- Highlights files on active issues to reduce risk
- Type‑to‑confirm bulk deletes
- Full audit trail for every deletion

#### Archive Candidates Tab

**Best for:** Finding inactive projects

Shows projects with:
- No updates in 180+ days
- Significant storage usage (> 1 MB)

**Use it to:**
- Identify projects for archival
- Contact project owners before cleanup
- Plan long-term storage optimization

---

## Settings & Configuration

### Accessing Settings

1. Open **Attachment Architect**
2. Click the **"Settings"** tab

### Available Settings

#### Scope

Choose whether to scan the **entire site** or **selected projects**.

#### Activity Panel

**What it does:** Shows deletion history on Jira issues

**Options:**
- ✅ **Enabled:** Activity panel appears on issues with deletion history
- ❌ **Disabled:** Activity panel hidden (default)

**How to enable:**
1. Go to **Settings** tab
2. Toggle **"Show Activity Panel on Issues"** to ON
3. Click **"Save Settings"**

**What users see:**
- On any issue where files were deleted
- A panel showing:
  - What was deleted
  - When it was deleted
  - Who deleted it
  - Why it was deleted (if reason provided)
  - Link to canonical file (if accessible)

---

## Audit Trail

### Viewing Audit Logs

1. Open **Attachment Architect**
2. Click the **"Audit Log"** tab

### What's Logged

Every action is recorded:

| Action | Details Logged |
|--------|----------------|
| **Scan Started** | Who, when, scan ID |
| **Scan Completed** | Duration, files found, duplicates detected |
| **Scan Failed** | Error message, context |
| **Files Deleted** | Who, what, when, where, why |
| **Settings Changed** | What changed, old value, new value |

### Filtering Logs

Use filters to find specific events:

- **Action Type:** Scan, Deletion, Settings
- **User:** Filter by who performed the action
- **Date Range:** Specific time period
- **Issue Key:** Actions related to specific issues

### Exporting Logs

**For compliance reporting:**

1. Apply filters to narrow down events
2. Take screenshots or copy data
3. Contact support for bulk export (coming soon)

---

## Trial vs. Paid Features

### Free Trial (30 Days)

✅ **Included:**
- Full dashboard access
- Unlimited scans
- All analytics and visualizations
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
3. Check Jira status page for outages
4. Contact support if still stuck after 30 minutes

#### Scan Failed

**Symptoms:** Error message appears

**Solutions:**
1. Click **"Start New Scan"** to retry
2. Check if you have admin permissions
3. Verify Jira instance is accessible
4. Contact support with error message

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
1. Click **"Start New Scan"**
2. Wait for scan to complete
3. Dashboard will populate automatically

#### Numbers Don't Match Jira

**Cause:** Scan data is outdated

**Solution:**
1. Run a new scan to refresh data
2. Dashboard shows data from last completed scan

---

## FAQ

### General Questions

**Q: Does the app read my file contents?**  
A: No. We only read metadata (filename, size, upload date). We never access file contents.

**Q: Is my data secure?**  
A: Yes. All data stays in your Jira instance. We use Atlassian Forge (SOC 2, ISO 27001 certified).

**Q: Can I undo a deletion?**  
A: No. Deletions are permanent. Always review carefully before deleting.

**Q: How often should I scan?**  
A: Monthly for most instances. Weekly for high-activity instances.

### Technical Questions

**Q: How long does a scan take?**  
A: 2-5 minutes for 10,000 issues. Scales linearly with instance size.

**Q: Does scanning affect Jira performance?**  
A: No. Scans run in the background with minimal impact.

**Q: What happens if I close the browser during a scan?**  
A: Scan continues in the background. Refresh the page to see progress.

**Q: Can multiple admins use the app?**  
A: Yes. All Jira admins can access the app. Actions are logged per user.

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
| **Run a scan** | Dashboard → "Start New Scan" → Confirm |
| **View duplicates** | Action Center → Quick Wins tab |
| **Delete duplicates** | View Details → Select files → "Delete Duplicates" |
| **Check trial status** | Look at banner at top of dashboard |
| **Enable Activity Panel** | Settings → Toggle ON → Save |
| **View audit log** | Audit Log tab → Apply filters |

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
- Provide deletion reasons for audit trail
- Enable Activity Panel for transparency

❌ **DON'T:**
- Delete files without reviewing
- Run multiple scans simultaneously
- Ignore trial limit warnings
- Delete canonical files manually

---

## Glossary

**Attachment:** A file uploaded to a Jira issue

**Canonical File:** The original file we keep (oldest upload)

**Duplicate:** An exact copy of a file (same content, different location)

**Hash:** A unique fingerprint of a file's contents (SHA-256)

**Quick Win:** A high-impact duplicate file (many copies, large size)

**Scan:** The process of analyzing all attachments in your Jira instance

**Storage Waste:** Space consumed by duplicate files

**Trial Limit:** Maximum deletions allowed during free trial (20 files)

---

## Version History

### v3.15.0 (November 2025)
- Unified progress bar + ETA (incl. first scans)
- Stale‑data mode for uninterrupted dashboards
- Storage Hygiene: detect and bulk delete logs/dumps/temp/system files
- Project scoping (scan entire site or selected projects)
- Heat Index improvements and Quick Wins polishing
- Audit log enhancements

### v3.0.0 (January 2025)
- ✅ Activity Panel settings fix
- ✅ Enhanced security (SAST + SCA scans)
- ✅ Production deployment
- ✅ Improved error handling

### v2.0.0 (December 2024)
- ✅ Bulk deletion (up to 100 files)
- ✅ Trial limit enforcement
- ✅ Dashboard real-time updates
- ✅ Comprehensive audit logging

### v1.0.0 (November 2024)
- ✅ Initial release
- ✅ Basic scanning and analytics
- ✅ Duplicate detection
- �� Manual cleanup

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

*Last updated: November 2025 | Version 3.15.0*
