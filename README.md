# Attachment Architect - Complete User Guide

A comprehensive guide to all features and functionality of Attachment Architect for Jira Cloud.

---

## Table of Contents

1. [Accessing the App](#accessing-the-app)
2. [Dashboard](#dashboard)
3. [Duplicates Management](#duplicates-management)
4. [Storage Hygiene](#storage-hygiene)
5. [Security Risks](#security-risks)
6. [Settings & Audit Log](#settings--audit-log)
7. [Attachment Explorer](#attachment-explorer)
8. [Attachment Activity Panel](#attachment-activity-panel)
9. [Licensing](#licensing)
10. [Troubleshooting](#troubleshooting)
11. [Best Practices](#best-practices)
12. [Support](#support)

---

## Accessing the App

### Admin Dashboard (Settings)

Navigate to: **Settings (⚙️) → Apps → Attachment Architect**

The admin dashboard contains 5 main tabs:

| Tab | Purpose |
|-----|---------|
| **Dashboard** | Scan results and KPI metrics |
| **Duplicates** | Manage and delete duplicate files |
| **Storage Hygiene** | Remove trash and low-value files |
| **Security Risks** | Identify files with security concerns |
| **Settings & Audit Log** | Configuration and activity history |

### Public Explorer (Apps Menu)

Navigate to: **Apps → Attachment Architect**

Features:
- Search attachments by name
- Filter by metadata (project, type, size, author, age)
- Manage personal folders
- View attachment details

### Issue Context (Activity Panel)

When enabled by an admin, each Jira issue displays an **Attachment Activity Panel** showing:
- Deletion history
- Canonical file references
- Links to related issues

### Issue View Attachment Panel (Issue Panel)

Attachment Architect adds a dedicated **Attachments** panel inside the Jira Issue View using Jira’s **Issue Panel** module.

**Where you’ll find it:**
- Open any Jira issue.
- Open the **Attachments** panel provided by Attachment Architect (it appears as its own panel in the issue view).

**What it is:**
- A compact, virtualized attachment table for the *current issue only*.
- Designed for quick triage: filter, select, preview, and run bulk actions.

**Toolbar (top of the panel):**
- **Filter filename…** (instant, client-side)
- **File Type** filter (dropdown)
- **Size** filter (dropdown)
- **Expand** button (opens the full Attachment Explorer in a modal)

**Table columns (Issue Panel view):**
- **Select** (checkbox per row + select-all in header)
- **Type** (file-type icon / thumbnail)
- **Name** (filename link; clicking it downloads the attachment)
- **Folders** (folder chip; opens the file’s folder(s) in the full Explorer modal)
- **Size**
- **Uploaded**

**What you can do:**
- **Select files:** single, multi-select, or select-all
- **Download:** click the filename to download a single file
- **Preview:** click the file-type icon/thumbnail to open preview
- **Folders:** click a folder chip to open the full Explorer focused on that folder
- **Bulk actions:** when one or more files are selected, a floating action bar appears with:
  - **Add to Folder**
  - **Download**
  - **Delete**
- **Expand:** open the full Attachment Explorer in a modal, pre-scoped to the current issue

#### Preview behavior (Issue View)

In the Issue Panel, preview is opened by clicking the **file-type icon/thumbnail**.

**Supported previews:**
- **Images & videos:** full-screen gallery preview (includes navigation)
- **PDF:** in-browser preview
- **Word (.docx):** in-browser preview
- **Code/text:** in-browser code viewer (search + navigation)
- **ZIP / archives:** in-browser archive inspector with per-file preview/download

#### Preview support matrix (formats & limits)

The table below summarizes what can be previewed in-browser and the hard size limits enforced for safety and performance.

| Category | Preview | How it opens | Size limit | Notes |
|---|---|---|---:|---|
| Images | Yes | Type icon/thumbnail → Preview | 15 MB | Also supports image MIME types (`image/*`). |
| Videos | Yes (limited) | Type icon → Preview | 100 MB | Only browser-compatible formats are supported (MP4, WebM). WebM may not play in Safari. |
| PDF | Yes | Type icon → Preview | 15 MB | Larger PDFs are download-only. |
| Word (.docx) | Yes | Type icon → Preview | 15 MB | `.doc` (legacy Word) is not supported for preview. |
| Code / Text | Yes | Type icon → Preview | 5 MB | Syntax highlighting is disabled above 1 MB (raw text mode; search still works). |
| Log / TXT | Yes | Type icon → Preview | 10 MB | Uses fast regex highlighting; higher limit than code files. |
| ZIP archives | Yes (browse) | Type icon → Browse archive | 500 MB (browse) | Browsing reads archive structure without downloading the full ZIP. |
| Files inside ZIP | Yes (if supported type) | ZIP → Preview on an entry | Per type (see above) | Single-file extraction has a hard limit (50 MB) due to Forge timeouts; larger entries require downloading the full ZIP. |

**ZIP extraction limit (inside ZIP viewer):**
- Maximum single-file extraction (preview/download of an entry): **50 MB**.

**ZIP Preview — Nested preview (inside archive):**
- You can preview supported files inside a ZIP without downloading the whole archive.
- Nested preview opens on top of the ZIP viewer.

**Keyboard (ESC) rules:**
- For ZIP nested previews: **ESC closes the nested preview first**, then **ESC closes the ZIP viewer**.
- For other previews: **ESC closes the preview**.

**Cinematic Mode footer (ZIP preview):**
- ZIP previews in Issue View include a “CINEMATIC MODE” footer in the letterbox area.
- This is purely UI copy (does not change functionality).

#### Expand to full Explorer

Use **Expand** in the Issue panel toolbar to open the full **Attachment Explorer** in a modal.
- The Explorer opens pre-scoped to the current issue using JQL.

---

## Dashboard

### Purpose

The Dashboard displays a summary of your most recent scan with key performance indicators (KPIs) and multi-dimensional analysis views.

### Scanning Workflow

#### Step 1: Start a Scan

1. Click **"Start the Audit"** button
2. Select your scan scope:
   - **Full Instance** — Scan the entire Jira instance
   - **Specific Projects** — Scan only selected projects
3. Confirm the scan

#### Step 2: Monitor Progress

- Real-time progress bar with percentage and ETA
- Can close browser window — scan continues in background
- Can cancel scan with **Cancel** button
- Estimated duration shown based on issue count

#### Step 3: View Results

After completion, the dashboard displays:

| Metric | Description |
|--------|-------------|
| **Digital Hoard** | Total attachment storage used |
| **Déjà Vu Data** | Duplicate storage (potential savings) |
| **Digital Landfill** | Trash file storage (logs, dumps, temp) |
| **Panic Level** | Overall inefficiency percentage (0-100%) |

### Analysis Views (Desktop Only)

After scanning, explore your data across 7 dimensions:

#### 1. Project Bloat Map
- Storage usage per project (treemap visualization)
- Identify which projects consume the most space
- Color-coded by waste percentage (green/yellow/red)

#### 2. File Type Analysis
- Storage breakdown by file extension (bubble chart)
- Identify oversized file types
- Average file size per type

#### 3. User Leaderboard
- Storage usage per user
- Top quota consumers
- Duplicate upload patterns

#### 4. Digital Archaeology
- Storage by file age (stacked bar chart)
- Age brackets: 0-90 days, 90-365 days, 1-2 years, 2-4 years, 4+ years
- Identify candidates for archival

#### 5. Workflow Analysis
- Storage by issue status
- Identify bottlenecks
- See how much storage is in completed vs. active issues

#### 6. Frozen Dinosaurs (Heat Index)
- Large files on old issues (highest cleanup priority)
- Heat score based on file size × issue age
- Scatter chart visualization

#### 7. Archive Candidates
- Projects with no updates in 180+ days
- Identify projects for archival
- Contact project owners before cleanup

### Quick Wins

The dashboard highlights the **top 3 duplicate files** with the biggest impact:

- **File Name** — The duplicate file
- **Total Wasted Space** — Storage wasted (e.g., "245 MB from 49 copies")
- **Action** — View details or delete

Click **"View Details"** to see all locations where the file appears.

---

## Duplicates Management

### Purpose

Find and delete duplicate files to reclaim storage space.

### Main Features

#### Quick Wins Tab
- Highest-impact duplicates sorted by wasted space
- Filterable by project and file type
- Sortable columns
- Pagination

#### Bulk Cleanup
- Select multiple duplicates
- Delete in batches (50 files per operation)
- Confirmation modal with type-to-confirm safety check

#### Duplicate Details Modal
- Shows all locations where the file appears
- **Canonical file** (oldest copy) is marked with ✅ and kept safe
- Links to all affected Jira issues
- File metadata (size, upload date, author)

### Deletion Process

1. Open the **Duplicates** tab
2. Review the list of duplicate files
3. Click **"View Details"** on any file to see all copies
4. Select duplicates to delete (canonical file is protected)
5. Click **"Delete Selected"**
6. Confirm deletion (may require type-to-confirm)
7. Deletion event is logged in **Audit Log**

### Safety Features

- Canonical file (oldest) is always protected
- Shows which file is canonical before deletion
- Links to all affected issues
- Full audit trail of all deletions
- Trial users limited to 20 total deletions

---

## Storage Hygiene

### Purpose

Automatically detect and remove "trash" files — low-value files that consume storage without providing value.

### What Gets Detected as Trash

| Category | Examples |
|----------|----------|
| **Log Files** | *.log, *.trace, debug files, error logs |
| **Database Dumps** | *.sql, *.dump, *.bak, backup files |
| **Temporary Files** | *.tmp, *.temp, *.cache, *.old |
| **Build Artifacts** | *.class, *.o, *.pyc, compiled files |
| **Archives** | *.zip, *.tar, *.gz (when duplicates exist) |

### Features

- **Sortable Table** — Click column headers to sort by:
  - File Name (alphabetical)
  - Issue Key
  - Waste Impact (size)
  - Issue Status
  - Age (days since creation)

- **Filters**:
  - Search by filename or issue key
  - Filter by file type (extension)
  - Filter by issue status
  - Filter by age range

- **Pagination** — Configurable items per page (10, 25, 50, 100)

- **Selection** — Select individual files or all files on current page

### Deletion Process

1. Open the **Storage Hygiene** tab
2. Review detected trash files
3. Use filters to narrow down (optional)
4. Select files to delete
5. Click **"Download Backup"** (opens Jira's native Backup Manager)
6. After backup is created, click **"Permanent Delete"**
7. Acknowledge risks and confirm deletion
8. Deletion event is logged in **Audit Log**

### Safety Features

- **Active Issue Warning** — Files on active issues highlighted in yellow
- **Backup Strategy Modal** — Directs you to Jira's native backup manager
- **Risk Acknowledgment** — Must acknowledge risks before deleting
- **Type-to-Confirm** — Extra confirmation for bulk deletes
- **Full Audit Trail** — Every deletion is logged with context

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

## Security Risks

### Purpose

Identify files with potential security concerns based on filename patterns and optional deep content scanning.

### Risk Severity Levels

#### CRITICAL 🔴
- Private keys (*.key, *.pem, id_rsa)
- Database dumps (*.sql, *.dump)
- Credentials files (.env, secrets.*)

#### HIGH 🟠
- Config files (*.conf, *.yaml, *.ini)
- AWS credentials
- API key files

#### MEDIUM 🟡
- Source code (*.js, *.py, *.java)
- Business documents (*.xlsx, *.docx)
- Log files

#### LOW 🟢
- Backup files (*.bak, *.backup)
- Archives (*.zip, *.tar)
- Text files

### Features

- **KPI Cards** — Summary metrics by severity level
- **Filterable Table** — Click severity cards to filter
- **Sortable Columns** — Sort by severity, filename, issue, etc.
- **Pagination** — Configurable items per page
- **Deep Content Scanning** (Optional) — Scan text files for sensitive data

### Deep Content Scanning

When enabled, scans text files < 5MB for:
- Passwords
- AWS Keys
- Bearer Tokens
- Credit Cards (Luhn validation)
- Social Security Numbers (SSN)
- Internal IP addresses

**Enable in:** Settings → Security & Scanning → Toggle ON

### Actions

- **Review Content** — Click to scan file (if scannable)
- **Download** — Download file for local inspection
- **Navigate to Issue** — Open the issue containing the file
- **Scan Results Modal** — Shows findings from deep content scan

### Important Notes

- **Read-Only View** — Security Risks tab is for awareness only
- **No Direct Deletion** — Remediate through issue management
- **Privacy-First** — Only scans filenames by default
- **Opt-In Scanning** — Deep content scanning must be enabled in Settings

---

## Settings & Audit Log

### Settings Section

#### Scan Scope Configuration
- **Purpose** — Define which data is scanned
- **Options**:
  - **Full Instance** — Scan the entire Jira instance
  - **Specific Projects** — Scan only selected projects

#### Activity Panel
- **Purpose** — Show attachment deletion history on issues
- **Default** — Disabled (stealth mode)
- **Enable** — Settings → Activity Panel → Toggle ON

#### Security Scanning
- **Purpose** — Enable deep content scanning for sensitive data
- **Default** — Disabled
- **Enable** — Settings → Security & Scanning → Toggle ON

#### Heat Index Thresholds
- **Large File Threshold** (MB) — Default: 10 MB
- **Ancient History Threshold** (days) — Default: 365 days
- Customize what qualifies as a "Frozen Dinosaur"

#### Auto-Pilot (Automated Scanning)
- **Purpose** — Schedule automatic scans
- **Frequency** — Daily, Weekly, or Monthly
- **Prerequisite** — At least one completed scan required
- **Enable** — Settings → Auto-Pilot → Toggle ON

#### Factory Reset
- **Purpose** — Wipe all index data and start fresh
- **Use Case** — Emergency recovery if scanner is stuck
- **Warning** — Dangerous operation, use only when necessary

### Audit Log

Displays all system events with full context:

| Event Type | Details |
|------------|---------|
| **Scan Started** | Who, when, scope, estimated issues |
| **Scan Completed** | Duration, files found, duplicates, waste % |
| **Scan Cancelled** | Who, when, progress at cancellation |
| **Scan Failed** | Error message and context |
| **Files Deleted** | Who, what, when, where, why, count |
| **Settings Changed** | What changed, old value, new value, who |

#### Filtering Options
- **Action Type** — Scan, Deletion, Settings
- **User** — Filter by who performed the action
- **Issue Key** — Actions related to specific issues
- **Date Range** — Specific time period

#### Expandable Details
Click the **▶** arrow to expand event details:
- Full context for each action
- Before/after values for settings changes
- List of affected issues for deletions
- Waste percentage indicators for scans

---

## Attachment Explorer

### Purpose

Search and filter attachments across your Jira instance. Manage personal folders for organization.

### Search & Filter Features

- **Search** — Find attachments by filename
- **Filters** — Project, file type, size, author, age, etc.
- **Virtualized List** — Efficient rendering for large datasets
- **Issue Links** — Click to navigate to the issue

### JQL Mode: My Filters (Starred Filters)

When using **JQL** mode in Attachment Explorer, you can quickly load your starred Jira filters.

**How to use:**
1. Switch to **JQL** mode.
2. Click the ⭐ icon in the toolbar (tooltip: **"Load saved filter"**).
3. Select one of your starred Jira filters.
4. The filter JQL is inserted into the JQL input (you can still edit it before searching).

**Notes:**
- Only shows filters you have starred in Jira.
- If you have many filters, a search input appears in the popup.

### Image Preview: Multiple Images + Select

Clicking an image attachment opens a full-screen image preview where you can navigate through all images and select while reviewing.

**What you can do in the preview:**
- **Next/Previous image:** use on-screen arrows or keyboard arrow keys.
- **Select/Deselect current image:** click the checkbox in the toolbar or press **Space**.
- **Download:** use the download button.
- **Zoom:** use zoom controls (scroll/pinch supported).
- **Close:** press **Esc**.

**Notes:**
- Selection is synced with the main results selection.

### Code / Log / TXT Preview (Built-in Viewer)

Attachment Explorer supports in-browser preview for common code and text formats.

**How to use:**
1. In **Attachment Explorer**, click a supported text/code attachment.
2. The viewer opens in a modal with search and navigation.
3. Use **Download** if preview is unavailable for the file.

#### What you can do in the viewer
- **Search in file**: type in the search box.
  - `Enter` = next match
  - `Shift + Enter` = previous match
  - `Ctrl/Cmd + F` focuses the search box
- **Filter mode**: filters visible lines to those matching the search query.
- **Word wrap**: toggle wrapping on/off.
- **Copy**: copy the full file content to clipboard.
- **Download**: download the original attachment.

#### Performance & safety limits
To keep the UI fast and avoid browser lockups, preview has hard limits:

- **Code files** (most extensions below):
  - Preview limit: **5 MB**
  - Syntax highlighting limit: **1 MB**
  - If file is **> 1 MB**, the viewer switches to **RAW** mode (plain text, search still works).
- **Log files** (`.log`, `.out`, `.err`, `.txt`):
  - Preview limit: **10 MB**

If the file is above the preview limit, it will be **download-only**.

#### Supported file types (by extension)

**Log & text (10 MB preview limit):**
- `.log`, `.out`, `.err`, `.txt`

**Web / frontend:**
- `.js`, `.mjs`, `.cjs`, `.jsx`, `.ts`, `.tsx`

**Config / data:**
- `.json`, `.yaml`, `.yml`, `.xml`, `.toml`, `.ini`, `.env`

**Database:**
- `.sql`

**Markup / styles:**
- `.html`, `.htm`, `.xhtml`, `.css`, `.scss`, `.sass`, `.less`

**Scripts / shell:**
- `.sh`, `.bash`, `.zsh`, `.bat`, `.cmd`, `.ps1`, `.psm1`

**Backend languages:**
- `.py`, `.python`, `.java`, `.c`, `.h`, `.cpp`, `.cc`, `.cxx`, `.hpp`, `.cs`, `.go`, `.rs`, `.php`, `.rb`, `.swift`, `.kt`, `.kts`, `.scala`, `.groovy`, `.gradle`

**Docs / misc text formats:**
- `.md`, `.markdown`, `.rst`, `.csv`, `.properties`, `.diff`, `.patch`, `.graphql`, `.gql`

**DevOps / config-like:**
- `.dockerfile`, `.docker`, `.makefile`, `.cmake`, `.nginx`, `.apache`, `.htaccess`

#### Supported file types (special filenames)
Some common filenames without an extension are also supported:
- `Dockerfile`, `Makefile`, `Jenkinsfile`, `Vagrantfile`, `.env*`, `.gitignore`, `.dockerignore`

#### MIME type support (fallback)
If the file extension is missing or unusual, preview may still be enabled based on MIME type:
- `text/*`
- `application/json`
- `application/xml`
- `application/javascript`
- `application/typescript`
- `application/x-yaml`
- `application/x-sh`
- `application/x-python`

### Folders (Personal Collections)

Personal folders for organizing attachments by topic or project.

#### Available Actions

| Action | Description |
|--------|-------------|
| **Create Folder** | New folder with custom name |
| **Rename Folder** | Change folder name |
| **Delete Folder** | Remove folder (attachments stay on issues) |
| **Add to Folder** | Select files and add to folder |
| **Remove from Folder** | Remove file from folder (stays on issue) |
| **View Contents** | See all files in folder |

#### Limits

- **Max folders per user** — 20
- **Max files per folder** — 500
- **Scope** — Personal (tied to your user account)

#### Smart Caching

Folders use intelligent caching to minimize Forge Storage operations:

- **Parallel Loading** — All folder items loaded simultaneously
- **Cache Warming** — Background pre-loading of folder data
- **Optimistic Updates** — Cache updated before storage write
- **Membership Cache** — Pre-computed file-to-folder mappings

---

## Attachment Activity Panel

### Purpose

Display attachment deletion history on Jira issues for transparency and compliance.

### What It Shows

- **Deletion Events** — What was deleted, when, by whom
- **Canonical File** — Reference to the original file (if accessible)
- **Issue Links** — Links to related issues

### Enabling the Panel

1. Go to **Settings & Audit Log** tab
2. Toggle **"Show Attachment Activity Panel"** to ON
3. Save settings
4. Panel now appears on issues with deletion history

---

## Licensing

### Trial (30 Days)

- ✅ Full access to all features
- ✅ Unlimited scans
- ✅ All analytics and visualizations
- ✅ Security risk detection
- ✅ Audit trail
- ⚠️ **Limited to 20 file deletions** (lifetime limit)
- After limit reached → App becomes read-only

### Paid Subscription

- ✅ Everything in trial, plus:
- ✅ **Unlimited deletions**
- ✅ Priority support
- ✅ Regular feature updates
- ✅ No restrictions

### Inactive (License Expired)

- ✅ Can view dashboard
- ✅ Can run scans
- ✅ Can see analytics
- ✅ Can view security risks
- ✅ Can view audit logs
- ❌ Cannot delete files
- ❌ Cannot change settings
- ❌ Security Risks tab disabled

### Checking Trial Status

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
- Can still view data and run scans
- Cannot delete files or change settings

---

## Troubleshooting

### "No Data / Empty Dashboard"

**Solution:**
- Run a scan and wait for completion
- Dashboard shows data from last completed scan

### "Numbers Don't Match Jira"

**Solution:**
- Dashboard displays data from the last completed scan
- Run a new scan to refresh the data
- Check the scope badge — may be scanning a subset of projects

### "Can't Delete (Permission Denied)"

**Solution:**
- Verify you have Jira admin permissions
- Check if your license allows deletions (trial limit or inactive)
- Contact your Jira admin if needed

### "Scan is Stuck"

**Solution:**
1. Refresh the page (scan continues in background)
2. Wait 5+ more minutes (large instances take time)
3. Check Phase 1 reassurance banner (collecting IDs is slow)
4. Check Jira status page for outages
5. If still stuck after 30 minutes → Settings → Factory Reset

### "Deep Scan Fails"

**Solution:**
- File may be too large (> 5MB)
- File may not be text format
- Try downloading and inspecting locally
- Check if deep scanning is enabled in Settings

### "Can't Cancel Scan"

**Solution:**
1. Wait for current batch to complete (up to 5 minutes)
2. Refresh page to see updated status
3. Scan will auto-cancel at next checkpoint

---

## Best Practices

### ✅ DO

- **Scan monthly** — Keep data fresh and accurate
- **Review Quick Wins first** — Maximum impact with minimum effort
- **Create backup before mass deletion** — Safety first
- **Enable Activity Panel** — Transparency and compliance
- **Review Security Risks regularly** — Catch issues early
- **Use project scoping** — Targeted scans for specific areas
- **Check issue status** — Avoid deleting from active work

### ❌ DON'T

- **Delete without reviewing** — Always check before deleting
- **Ignore active issue warnings** — Yellow highlights are important
- **Delete without backup** — Deletions are permanent
- **Rush through security remediation** — Take time to investigate
- **Delete canonical files manually** — App protects them for a reason
- **Run multiple scans simultaneously** — Can cause conflicts
- **Ignore trial limit warnings** — Plan ahead for subscription

---

## Support

**Support Portal:** https://drinkits.atlassian.net/servicedesk/customer/portal/34

**Response Time:** Within 24 hours (weekdays)

### Before Contacting Support

1. ✅ Refresh the page
2. ✅ Check this user guide
3. ✅ Run a new scan
4. ✅ Verify you have admin permissions
5. ✅ Check Jira status page

### When Contacting Support, Include

- Your Jira instance URL
- App version (shown in dashboard)
- What you were trying to do
- Error message (if any)
- Screenshots (if applicable)
- Browser and Jira version

---

## Quick Reference

### Common Tasks

| Task | Steps |
|------|-------|
| **Run a scan** | Dashboard → "Start the Audit" → Choose Scope → Confirm |
| **View duplicates** | Duplicates tab → Review list → Click "View Details" |
| **Delete duplicates** | Select files → "Delete Selected" → Confirm |
| **Remove trash files** | Storage Hygiene → Select files → "Permanent Delete" → Confirm |
| **Check security risks** | Security Risks tab → Review by severity |
| **View audit log** | Settings & Audit Log → Scroll to "The Paper Trail" |
| **Enable Activity Panel** | Settings → Activity Panel → Toggle ON → Save |
| **Configure scan scope** | Settings → Scan Scope → Select projects → Save |
| **Create a folder** | Explorer → "New Folder" → Enter name |
| **Add to folder** | Explorer → Select files → "Add to Folder" → Choose folder |

### Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl/Cmd + R` | Refresh dashboard |
| `Esc` | Close modal / close image preview |
| `Tab` | Navigate between fields |
| `Enter` | Confirm action |
| `Space` | Toggle selection in image preview (when open) |
| `←` / `→` | Previous/next image in image preview (when open) |

---

**Last Updated:** January 2026

For the latest updates and feature announcements, visit the Atlassian Marketplace listing.
