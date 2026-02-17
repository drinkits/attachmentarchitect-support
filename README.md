# Attachment Architect - User Guide

A complete guide to all features of Attachment Architect for Jira Cloud.

---

## Table of Contents

1. [Where to Find the App](#1-where-to-find-the-app)
2. [Admin Console](#2-admin-console)
3. [Scanning](#3-scanning)
4. [Mission Control (Dashboard)](#4-mission-control-dashboard)
5. [Action Center](#5-action-center)
6. [Deep Analytics](#6-deep-analytics)
7. [Operations (Scans, Audit, Settings)](#7-operations)
8. [Attachment Explorer](#8-attachment-explorer)
9. [Issue Panel (Attachments)](#9-issue-panel-attachments)
10. [Attachment Activity Panel](#10-attachment-activity-panel)
11. [File Preview](#11-file-preview)
12. [OCR (Live Text)](#12-ocr-live-text)
13. [Folders (Personal Collections)](#13-folders-personal-collections)
14. [Licensing](#14-licensing)
15. [Troubleshooting](#15-troubleshooting)
16. [Support](#16-support)

---

## 1. Where to Find the App

Attachment Architect has four entry points in Jira:

| Entry Point | Who Can Access | How to Open |
|---|---|---|
| **Admin Console** | Jira admins | Jira settings → Apps → Attachment Architect |
| **Attachment Explorer** | All users | Apps menu → Attachment Explorer |
| **Attachments Issue Panel** | All users | Open any Jira issue → Attachments panel |
| **Attachment Activity** | All users (if enabled) | Open a Jira issue → Attachment Activity panel |

---

## 2. Admin Console

The Admin Console is the control room for Jira admins. It always opens on **Mission Control**.

### Sidebar Navigation

The left sidebar organizes all admin pages into four sections:

**Overview**
- 🎯 Mission Control - KPIs, health score, recommendations

**Action Center**
- 🛡️ Security Risks - PII and secret detection
- 📋 Duplicates - Hash-based duplicate groups + bulk delete
- 🧹 Storage Hygiene - Trash file detection + cleanup
- ⏱️ Frozen Dinosaurs - Heat index (stale attachments)

**Deep Analytics**
- 📈 Storage Velocity - Monthly growth chart
- 📂 By Project - Project storage breakdown
- 👤 By User - User storage breakdown
- 📄 By File Type - File type distribution
- ⏳ By Age - Age distribution
- 📦 Zombie Projects - Archive candidates

**Operations**
- 🔬 Scans - Scan history, trigger, export
- 📋 Audit Log - Action timeline
- ⚙️ Settings - Configuration
- ❓ Help & Support - Documentation, bug reports, feature requests

The sidebar can be collapsed to icon-only mode (52px). Collapse state is remembered.

---

## 3. Scanning

### What a Scan Does

A scan builds an **attachment index** — metadata only (filenames, sizes, hashes, issue keys). No file content is downloaded or stored.

The index powers:
- Dashboard KPIs and health score
- Duplicate detection (content hash grouping)
- Trash file detection (filename heuristics)
- Security risk detection (filename patterns)
- Heat index calculation
- All analytics pages

### Starting a Scan

1. Open Admin Console → **Scans** page
2. Click **Start New Scan**
3. The scan begins immediately (scans all issues with attachments)

### During a Scan

- Live progress bar with percentage and phase indicator
- You can close the browser — the scan continues in the background
- You can cancel at any time (stops at the next safe checkpoint)

---

## 4. Mission Control (Dashboard)

Mission Control shows a high-level overview of your attachment landscape.

### KPI Cards

After a scan completes, you see summary metrics including:
- Total attachment storage
- Duplicate storage (potential savings)
- Trash file storage
- Health score (0–100)

### Smart Recommendations

Context-aware suggestions based on scan results (e.g., "You have 2.3 GB of duplicates - clean up the top 5 groups to reclaim 80% of waste").

### Storage Velocity Chart

Monthly growth trend showing files added and bytes consumed over time.

### Top Offenders

Top projects, users, and file types by storage consumption.

---

## 5. Action Center

### 5.1 Security Risks

Detects files with potential security concerns based on **filename patterns**.

#### Severity Levels

| Level | Examples |
|---|---|
| **CRITICAL** | Private keys (`.key`, `.pem`, `id_rsa`), database dumps (`.sql`, `.dump`), credential files (`.env`, `secrets.*`) |
| **HIGH** | Config files (`.conf`, `.yaml`, `.ini`), AWS credentials, API key files |
| **MEDIUM** | Source code, business documents, log files |
| **LOW** | Backup files, archives, text files |

#### Features

- KPI cards showing count per severity
- Filterable and sortable table
- Click to navigate to the issue containing the file
- On-demand content scanning for text files (if enabled in Settings)

#### On-Demand Content Scanning

When enabled, scans text files (<5MB) for:
- Passwords and secrets
- AWS keys
- Bearer tokens
- Credit card numbers (Luhn validation)
- Social Security Numbers
- Internal IP addresses

Enable in: Settings → Security Sentinel toggle

### 5.2 Duplicates

Duplicates are grouped by **SHA-256 content hash**. The oldest copy is marked as the **canonical** (original) file and is protected from deletion.

#### Features

- Groups sorted by wasted space (highest impact first)
- Click **View Details** to see all locations where a file appears (up to 20 locations per group)
- Links to all affected Jira issues
- File metadata (size, upload date, author)

#### Deleting Duplicates

1. Open Duplicates page
2. Click **View Details** on a group
3. Select copies to delete (canonical file is protected)
4. Click **Delete Selected**
5. Confirm (type-to-confirm for bulk operations)
6. Deletion is logged in the Audit Log

### 5.3 Storage Hygiene

Detects "trash" attachments - low-value files that consume storage.

#### What Gets Detected

| Category | Examples |
|---|---|
| Log files | `*.log`, `*.trace`, debug files |
| Database dumps | `*.sql`, `*.dump`, `*.bak` |
| Temporary files | `*.tmp`, `*.temp`, `*.cache`, `*.old` |
| Build artifacts | `*.class`, `*.o`, `*.pyc` |

#### Deletion Safety Flow

1. Review detected trash files (filter by type, status, age)
2. Select files to delete
3. **Backup Strategy** step - directs you to create a Jira backup first
4. **Delete** step - confirm deletion (type-to-confirm)
5. Deletion is logged in the Audit Log

#### Safety Indicators

- Files on **active issues** are highlighted with a warning
- Files on **completed issues** are safer to delete

### 5.4 Frozen Dinosaurs (Heat Index)

Surfaces large files on stale issues - the highest-priority cleanup candidates.

Heat score is based on: **file size × issue staleness** (days since last update).

Paginated table with scatter chart visualization.

---

## 6. Deep Analytics

All analytics pages require at least one completed scan.

| Page | What It Shows |
|---|---|
| **Storage Velocity** | Monthly growth chart (files + bytes over time) |
| **By Project** | Storage per project (treemap visualization) |
| **By User** | Storage per user (top consumers, duplicate patterns) |
| **By File Type** | Storage per file extension (bubble chart) |
| **By Age** | Age distribution (0–30d, 30–90d, 90–180d, 180–365d, 365d+) |
| **Zombie Projects** | Projects with no updates in 180+ days (archive candidates) |

---

## 7. Operations

### 7.1 Scans

The Scans page shows:
- **Start New Scan** button — launches a scan immediately
- **Last scan summary** — metrics from the most recent completed scan
- **Scan history table** — all past scans with status, duration, file count, storage, duplicates, security risks, and trigger type (manual/auto)
- **Delta badges** — each scan row shows +/- changes compared to the previous scan (files, bytes, duplicates, risks)
- **Data export** — export scan data as CSV or ZIP (multiple datasets)

### 7.2 Audit Log

Records all significant actions:

| Event Type | What's Logged |
|---|---|
| Scan Started | Who, when, scope |
| Scan Completed | Duration, files found, duplicates, health score |
| Scan Cancelled | Who, when, progress at cancellation |
| Scan Failed | Error details |
| Files Deleted | Who, what files, from which issues, when |
| Settings Changed | What changed, old value → new value, who |

#### Filtering

- By action type
- By user
- By date range

Click the expand arrow (▶) on any event to see full details.

### 7.3 Settings

Settings are organized into sections:

#### General
- **Activity Panel** toggle - show/hide the Attachment Activity panel on issues (default: off)

#### Scanning & Detection
- **Security Sentinel** toggle - enable real-time upload scanning and on-demand content scanning
- **Large File Threshold** (MB) - what counts as a "large" file for heat index (default: 10 MB)
- **Old Issue Threshold** (days) - what counts as a "stale" issue for heat index (default: 365 days)

#### OCR Publishing
- **OCR Publishing** toggle - allow users to publish OCR text as Jira comments
- **PII Redaction** toggle - attempt to redact sensitive patterns before publishing
- **Max Characters** - maximum OCR text length per comment (1,000–15,000)

#### Danger Zone
- **Factory Reset** - wipes all index data and starts fresh. Type `DELETE` to confirm. Use only for recovery.

---

## 8. Attachment Explorer

### What It Is

The Attachment Explorer is a **live search** tool available to all Jira users via **Apps → Attachment Explorer**.

It queries the Jira API in real time - no scan required.

### Two Modes

| Mode | Description |
|---|---|
| **Basic** | Visual filters (project, file type, size, author, status, date range) |
| **Advanced (JQL)** | Raw JQL input with syntax validation |

### Safety Limit

Explorer enforces a **50,000 issue** safety limit. If your query matches more issues, you'll see a warning with an option to override (explicit confirmation required).

### Starred Filters (JQL Mode)

In JQL mode, click the ⭐ icon to load one of your starred Jira filters. The filter's JQL is inserted into the input field.

### Selection

Selection works like a desktop file manager:

| Action | Behavior |
|---|---|
| Click | Select one row (clears previous selection) |
| Ctrl/Cmd + Click | Toggle a row in/out of selection |
| Shift + Click | Select a contiguous range from the last anchor |

Selection is tracked by file ID - it survives sorting and filtering. The Shift anchor resets when sort/filter changes.

### Bulk Actions

When files are selected, a floating action bar appears with:
- **Add to Folder**
- **Download** (single or bulk)
- **Delete** (subject to permissions and licensing)

### Table Columns

- Checkbox (select)
- File type icon / thumbnail
- Filename
- Folder membership
- Issue key (link to issue)
- Size
- Upload date

---

## 9. Issue Panel (Attachments)

Attachment Architect adds an **Attachments** panel inside every Jira issue.

### What It Shows

A compact, virtualized attachment table for the current issue only.

### Toolbar

- Filter by filename (instant, client-side)
- File type filter
- Size filter
- **Expand** button - opens the full Attachment Explorer in a modal, pre-scoped to the current issue

### What You Can Do

- Preview files (click the file type icon/thumbnail)
- Select files (single, multi-select, or select-all)
- Download (click filename)
- Add to folder
- Delete (if permitted)

---

## 10. Attachment Activity Panel

A contextual panel on Jira issues that shows **attachment deletion history** for transparency and compliance.

### What It Shows

- What was deleted, when, by whom
- Reference to the canonical file (if applicable)
- Links to related issues

### Enabling

This panel is **off by default**. To enable:
1. Admin Console → Settings
2. Toggle **Activity Panel** to ON
3. Save

The panel only appears on issues that have deletion history.

---

## 11. File Preview

### Preview Support Matrix

| File Type | Preview | Size Limit | Notes |
|---|---|---:|---|
| Images (jpg, png, gif, bmp, svg, webp, ico) | ✅ Full-screen gallery | 15 MB | Navigation between images, zoom, select |
| Video (mp4, webm) | ✅ HTML5 player | 100 MB | WebM may not play in Safari |
| PDF | ✅ In-browser | 15 MB | Native text selection supported |
| Word (.docx) | ✅ In-browser | 15 MB | `.doc` (legacy) is NOT supported |
| Excel (.xlsx, .xls) | ✅ In-browser | 15 MB | `.xls` has limited fidelity |
| Code / text files | ✅ Syntax-highlighted viewer | 10 MB | Syntax highlighting disabled above 1 MB (raw text mode) |
| Log / txt files | ✅ Text viewer | 20 MB | Optimized for large text |
| ZIP archives | ✅ Browse contents | 500 MB | Only reads archive structure, not full download |
| Files inside ZIP | ✅ If supported type | Per type | Single-file extraction limit: 50 MB |
| Unsupported formats | ❌ Download only | - | 50% opacity icon, tooltip explains |

### Supported Code/Text Extensions

**Log & text:** `.log`, `.txt`, `.out`, `.err`

**Web:** `.js`, `.mjs`, `.cjs`, `.jsx`, `.ts`, `.tsx`

**Config:** `.json`, `.yaml`, `.yml`, `.xml`, `.toml`, `.ini`, `.env`

**Database:** `.sql`

**Markup:** `.html`, `.htm`, `.xhtml`, `.css`, `.scss`, `.sass`, `.less`

**Shell:** `.sh`, `.bash`, `.zsh`, `.bat`, `.cmd`, `.ps1`, `.psm1`

**Backend:** `.py`, `.java`, `.c`, `.h`, `.cpp`, `.cc`, `.cxx`, `.hpp`, `.cs`, `.go`, `.rs`, `.php`, `.rb`, `.swift`, `.kt`, `.kts`, `.scala`, `.groovy`, `.gradle`

**Docs:** `.md`, `.markdown`, `.rst`, `.csv`, `.properties`, `.diff`, `.patch`, `.graphql`, `.gql`

**DevOps:** `Dockerfile`, `Makefile`, `Jenkinsfile`, `Vagrantfile`, `.gitignore`, `.dockerignore`

### Code Viewer Features

- **Search in file** - `Enter` = next match, `Shift+Enter` = previous, `Ctrl/Cmd+F` focuses search
- **Filter mode** - show only lines matching the search query
- **Word wrap** toggle
- **Copy** full file content
- **Download** original attachment

### PDF Text Selection

PDF preview supports native text selection for PDFs with a text layer. Click and drag to select, then Ctrl/Cmd+C to copy. Scanned PDFs (image-only) do not have a text layer.

### ZIP Archive Browsing

ZIP files are browsed using **byte-range fetching** - only the archive directory (~64KB) is downloaded initially. Individual files are extracted on demand.

- Navigate the folder structure
- Preview supported files inside the archive
- Download individual files or the full archive

**Keyboard:** ESC closes nested preview first, then the ZIP viewer.

### Image Gallery

Clicking an image opens a full-screen gallery with:
- Next/previous navigation (arrows or keyboard ←/→)
- Select/deselect current image (checkbox or Space)
- Zoom controls
- Download
- Close with ESC

---

## 12. OCR (Live Text)

### What It Does

Extracts selectable, copyable text from image attachments using a built-in text scanner.

### How It Works

- OCR runs **entirely in your browser** (client-side)
- Uses offline language packs bundled with the app
- No data is sent to external services
- OCR results are **not stored** by the app

### How to Use

1. Open an image preview (from Explorer or Issue Panel)
2. Open the **Detected Text** panel
3. Select a language (if needed)
4. Copy the extracted text

### Bundled Languages (20)

| Language | Code |
|---|---|
| English | eng |
| German | deu |
| French | fra |
| Spanish | spa |
| Italian | ita |
| Portuguese | por |
| Dutch | nld |
| Russian | rus |
| Polish | pol |
| Ukrainian | ukr |
| Czech | ces |
| Swedish | swe |
| Turkish | tur |
| Japanese | jpn |
| Korean | kor |
| Chinese (Simplified) | chi_sim |
| Hindi | hin |
| Estonian | est |
| Latvian | lav |
| Lithuanian | lit |

### Limits

| Limit | Value |
|---|---|
| Max image dimension | 4,000 px (larger images are downscaled) |
| Max input size | ~25 MB |
| Timeout | 2 minutes per scan |

### Make Searchable (OCR → Comment)

If enabled by an admin, you can publish OCR text into the Jira issue as a **structured comment**, making it searchable via JQL (`comment ~ "keyword"`).

**How to use:**
1. Run OCR on an image
2. Click **Make Searchable**
3. The app posts (or updates) a comment on the issue

**Behavior:**
- One comment per attachment (no spam). If text hasn't changed, nothing is reposted.
- Rate limited: 30 publishes per user per 5 minutes
- Text is capped at the admin-configured maximum (up to 15,000 characters)
- Optional PII redaction (emails, phone numbers, credit cards, secrets) - enabled by default

**After publishing:** The action changes to **Copy JQL** so you can immediately search for the text.

---

## 13. Folders (Personal Collections)

### What They Are

Folders are personal collections for organizing attachments by topic, project, or workflow. They are tied to your Jira account - other users cannot see your folders.

### What You Can Do

| Action | Description |
|---|---|
| Create folder | New folder with a custom name |
| Rename folder | Change the folder name |
| Delete folder | Remove the folder (attachments stay on their Jira issues) |
| Add to folder | Select files → Add to Folder → choose folder |
| Remove from folder | Remove a file from a folder (stays on the issue) |
| View contents | Open a folder to see all files in it |

### Limits

| Limit | Value |
|---|---|
| Max folders per user | 20 |
| Max files per folder | 500 |

---

## 14. Licensing

### Trial (30 Days)

- ✅ Full access to all features
- ✅ Unlimited scans and analytics
- ⚠️ **Limited to 20 file deletions** (lifetime total)
- After limit → deletion is blocked

### Active (Paid Subscription)

- ✅ Everything, no restrictions
- ✅ Unlimited deletions

### Inactive (License Expired)

- ✅ Can view dashboards, run scans, see analytics
- ❌ Cannot delete files
- ❌ Cannot change settings

### Trial Status

A banner at the top of the Admin Console shows:
- Days remaining
- Deletions used out of 20

---

## 15. Troubleshooting

### No data in Admin Console

Run a scan and wait for it to complete. All dashboard data comes from the most recent completed scan.

### Numbers don't match Jira

Dashboard data reflects the **last completed scan**. Run a new scan to refresh.

### Permission denied on delete

- Deletions run as the current user - Jira permissions apply
- Check your license status (trial limit or inactive)
- Contact your Jira admin if needed

### Scan is stuck

1. Refresh the page (scan continues in background)
2. Wait - large instances can take time
3. Cancel and retry
4. If stuck for 30+ minutes → Settings → Factory Reset

### OCR not working

- Check that the image is under 25 MB and under 4,000 px
- Try a different language
- Refresh the page and retry

### Preview not available

- Check the file size against the limits in the [Preview Matrix](#preview-support-matrix)
- `.doc` (legacy Word) is not supported - only `.docx`
- Video formats other than MP4 and WebM are not supported

---

## 16. Support

**Support Portal:** https://drinkits.atlassian.net/servicedesk/customer/portal/34

- **Report a Bug:** https://drinkits.atlassian.net/servicedesk/customer/portal/34/group/34/create/43
- **Suggest a Feature:** https://drinkits.atlassian.net/servicedesk/customer/portal/34/group/34/create/44
- **Documentation:** https://github.com/drinkits/attachmentarchitect-support

### When Contacting Support

Include:
- Your Jira site URL
- What page you were on (Mission Control / Explorer / Issue Panel)
- What you clicked
- The exact error message (if any)
- Screenshots (if applicable)
- Browser and OS

---

**Last updated:** July 2025
