# Attachment Architect - User Guide (Jira Cloud)

This guide documents the **current, implemented** Attachment Architect functionality.

---

## Table of Contents

1. [Where to Find Attachment Architect](#1-where-to-find-attachment-architect)
2. [Admin Console](#2-admin-console)
   - [Mission Control (Dashboard)](#mission-control-dashboard)
   - [Action Center](#action-center)
   - [Deep Analytics](#deep-analytics)
   - [Operations](#operations)
3. [Scanning (Index Build)](#3-scanning-index-build)
4. [Attachment Explorer (Global Page)](#4-attachment-explorer-global-page)
   - [Basic vs Advanced (Raw JQL)](#basic-vs-advanced-raw-jql)
   - [Live Explorer Safety Limits](#live-explorer-safety-limits)
   - [Selection (Ctrl/Cmd + Click, Shift + Click)](#selection-ctrlcmd--click-shift--click)
   - [Folders (Personal Collections)](#folders-personal-collections)
   - [Bulk Actions](#bulk-actions)
5. [Issue View Modules](#5-issue-view-modules)
   - [Attachments Issue Panel](#attachments-issue-panel)
   - [Attachment Activity (Issue Context)](#attachment-activity-issue-context)
6. [File Preview](#6-file-preview)
   - [Preview Matrix (14 Viewer Types)](#preview-matrix-14-viewer-types)
   - [Image & Video Gallery](#image--video-gallery)
   - [PDF Viewer](#pdf-viewer)
   - [Word Document Viewer (.docx)](#word-document-viewer-docx)
   - [Excel / Spreadsheet Viewer (.xlsx, .xls, .ods)](#excel--spreadsheet-viewer-xlsx-xls-ods)
   - [PowerPoint Viewer (.pptx, .ppsx)](#powerpoint-viewer-pptx-ppsx)
   - [CSV / TSV Grid Viewer](#csv--tsv-grid-viewer)
   - [Code & Text Viewer (80+ languages)](#code--text-viewer-80-languages)
   - [Audio Player](#audio-player)
   - [Email Viewer (.eml)](#email-viewer-eml)
   - [Certificate Viewer (.pem, .crt, .cer)](#certificate-viewer-pem-crt-cer)
   - [Markdown Viewer (.md)](#markdown-viewer-md)
   - [Map / Geo Viewer (.kml, .kmz, .geojson, .gpx)](#map--geo-viewer-kml-kmz-geojson-gpx)
   - [Archive Inspector (.zip, .tar, .gz)](#archive-inspector-zip-tar-gz)
   - [Preview Size Limits](#preview-size-limits)
7. [OCR (Live Text Recognition)](#7-ocr-live-text-recognition)
   - [How OCR Works](#how-ocr-works)
   - [Make Searchable (OCR → Comment)](#make-searchable-ocr--comment)
8. [Licensing](#8-licensing)
9. [Troubleshooting](#9-troubleshooting)
10. [Support](#10-support)

---

## 1. Where to Find Attachment Architect

Attachment Architect has **four entry points** in Jira Cloud:

| Entry Point | Who Can Access | Where |
|---|---|---|
| **Admin Console** | Jira Admins | Jira settings → Apps → Attachment Architect |
| **Attachment Explorer** | All users | Apps menu → Attachment Explorer |
| **Attachments Panel** | All users | Issue sidebar → "Attachments" panel |
| **Attachment Activity** | All users | Issue context → "Attachment Activity" (conditional) |

---

## 2. Admin Console

The Admin Console is the control room for Jira administrators. It opens on **Mission Control** by default.

### Layout

- **Left sidebar** - collapsible navigation with icon-only mode
- **Primary content area** - tables, charts, and KPI tiles
- **Help & Support** - bottom of sidebar, links to documentation and support portal

### Sidebar Navigation

The sidebar is organized into four sections:

#### Mission Control (Dashboard)

The landing page. Shows key performance indicators (KPIs) at a glance:
- Total attachments indexed
- Total storage consumed
- Security risk count
- Duplicate count
- Scan status and last scan time

#### Action Center

Four specialized views for attachment governance:

| Page | Icon | Purpose |
|---|---|---|
| **Security Risks** | 🔒 | Detected risks based on filename patterns and content scanning. Filter by severity, open source issue, scan file content. |
| **Duplicates** | 📄 | Files grouped by content hash. View groups sorted by storage impact, inspect locations, delete duplicates (original copy protected). |
| **Storage Hygiene** | 🗑️ | "Trash" attachments (low-value files) detected by filename/type heuristics. Two-step safety deletion: Backup Strategy → Delete. |
| **Frozen Dinosaurs** | ⏱️ | Heat Index - surfaces large files on stale issues. Scatter chart visualization. Paginated table with sort/filter. High cleanup priority items first. |

#### Deep Analytics

Six analytics pages with Recharts visualizations:

| Page | What It Shows |
|---|---|
| **Storage Velocity** | Storage growth over time (monthly trend) |
| **By Project** | Storage breakdown per Jira project |
| **By User** | Storage consumption per user |
| **By File Type** | Distribution across 20 file categories |
| **By Age** | Attachment age distribution |
| **Zombie Projects** | Archive candidates - projects with attachments but no recent activity |

#### Operations

| Page | Purpose |
|---|---|
| **Scans** | Scan history, scan-to-scan comparison, CSV export of scan data |
| **Audit Log** | Full audit trail - scans, deletions, settings changes. Expandable rows with details. |
| **Settings** | Feature toggles, scanning/security configuration, OCR publishing settings, Auto-Pilot schedule, "Danger Zone" factory reset |

---

## 3. Scanning (Index Build)

### What a Scan Does

A scan builds an **attachment index** (metadata only - no file content is stored) that powers all dashboards, analytics, duplicate detection, hygiene scoring, and heat index calculations.

Scan data is stored in Forge SQL (MySQL-compatible hosted database).

### Scope Options

Admins can configure scan scope:
- **Full instance** - all projects
- **Specific projects** - selected projects only
- **JQL scope** - custom JQL query (when enabled)

### Auto-Pilot

Scans can run automatically on a schedule (daily or weekly). The scheduler heartbeat runs every 5 minutes; the actual scan frequency is enforced in code.

### Progress & Cancellation

- Scans show **live progress** with percentage and current project
- You can **cancel** a running scan - it stops at safe checkpoints
- Cancelled scans retain partial data (no data loss)

### Two-Phase Scanning

Large instances use a two-phase approach:
1. **Phase 1:** Collect issue metadata via JQL pagination
2. **Phase 2:** Fetch attachment details per issue

This ensures reliable scanning even for instances with millions of issues.

---

## 4. Attachment Explorer (Global Page)

### What It Is

Attachment Explorer is a **live, real-time** attachment search tool available to **all Jira users** (not just admins).

Access: **Apps menu → Attachment Explorer**

### Basic vs Advanced (Raw JQL)

Explorer has two search modes:

| Mode | How It Works |
|---|---|
| **Basic** | Visual filter dropdowns - Project, Status, Issue Assignee, Type, Created date. Text search for issue text. Filename filter. File Type and Size filters. |
| **Advanced (JQL)** | Raw JQL input field. Full JQL syntax support. Direct query editing. |

Switch between modes with the **Basic / JQL** toggle in the toolbar.

### Live Explorer Safety Limits

To prevent accidental "scan the universe" queries:
- Explorer enforces a **50,000 issue safety limit**
- If a query would exceed this limit, a warning is shown
- There is a **manual override flow** (explicit user confirmation required)
- Results are fetched in real-time via paginated Jira REST API calls

### Selection (Ctrl/Cmd + Click, Shift + Click)

Selection works like a desktop file manager:

| Action | Behavior |
|---|---|
| **Click** | Select one row (clears previous selection) |
| **Ctrl/Cmd + Click** | Toggle individual file (add/remove) |
| **Shift + Click** | Select contiguous range from last anchor |
| **Select All checkbox** | Toggle all visible files |

Selection survives sorting and filtering by tracking file IDs.

### Folders (Personal Collections)

Folders are **personal collections** - bookmarks for attachments you want to track.

| Action | How |
|---|---|
| Create folder | Folder selector → "+" button |
| Rename folder | Click folder name → edit inline |
| Delete folder | Folder menu → delete (does NOT delete files from Jira) |
| Add files | Select files → floating action bar → "Add to Folder" |
| Remove files | Open folder → select files → "Remove from Folder" |
| View folder | Click folder name in the folder selector |

**Limits:**
- Max **20 folders** per user
- Max **500 files** per folder
- Folders are scoped to your Jira account (not shared)

### Bulk Actions

When files are selected, a **floating action bar** appears at the bottom:

| Action | Description |
|---|---|
| **Download** | Single file: direct download. Multiple files: opens download options modal (ZIP packaging). |
| **Add to Folder** | Opens folder selection modal. Create new folder or add to existing. |
| **Delete** | Opens delete confirmation modal. Two-step safety flow. Requires Jira delete permission. |
| **Clear Selection** | Deselect all files |

**Delete limit from Issue Panel:** Max 100 files per batch. Use Attachment Explorer for larger cleanups.

---

## 5. Issue View Modules

### Attachments Issue Panel

A **compact attachment viewer** embedded in the Jira issue sidebar.

**Features:**
- Lists all attachments for the current issue
- Compact toolbar with filename filter, file type filter, size filter
- Click to preview any supported file type
- Select multiple files for bulk actions
- Folder chips showing which folders contain each file
- "Expand" button opens full Attachment Explorer filtered to this issue
- "Refresh" button reloads attachment list
- Folder navigation - click a folder chip to open that folder in Explorer

**Empty state:** Shows "0 attachments found. This issue is suspiciously clean." with a button to open Global Explorer.

### Attachment Activity (Issue Context)

A **conditional** context panel that appears on issues with attachment activity.

**Display conditions:**
- Issue must have the `attachmentArchitect-hasActivity` entity property set to `true`
- The `aa_showActivityPanel` app property must be enabled

This panel is designed for **deletion transparency** - showing what happened to attachments on this issue.

---

## 6. File Preview

Attachment Architect includes **14 specialized file viewers** that render files entirely in the browser. No file content is sent to external servers.

### Preview Matrix (14 Viewer Types)

| # | Viewer | File Types | Max Size | Key Features |
|---|--------|-----------|----------|-------------|
| 1 | **Image Gallery** | jpg, jpeg, png, gif, bmp, svg, webp, ico | 15 MB | Lightbox, zoom, pan, gallery navigation, OCR |
| 2 | **Video Player** | mp4, webm | 100 MB | HTML5 player, gallery navigation |
| 3 | **PDF Viewer** | pdf | 15 MB | Page-by-page rendering, zoom, page navigation |
| 4 | **Word Viewer** | docx | 15 MB | Full document rendering with styles |
| 5 | **Excel Viewer** | xlsx, xls, ods | 15 MB | Sheet tabs, column/row headers, search |
| 6 | **PowerPoint Viewer** | pptx, ppsx | 50 MB | Slide-by-slide rendering |
| 7 | **CSV Grid Viewer** | csv, tsv | 15 MB | Spreadsheet grid, column sorting |
| 8 | **Code Viewer** | 80+ extensions | 10 MB (code) / 20 MB (logs) | Syntax highlighting, line numbers, search, word wrap, copy |
| 9 | **Audio Player** | mp3, wav, ogg, m4a, aac, flac, opus | 100 MB | Waveform, ID3 tags, lyrics display |
| 10 | **Email Viewer** | eml | 15 MB | Headers, body, attachment list |
| 11 | **Certificate Viewer** | pem, crt, cer, der, p7b, p7c, key | 1 MB | Certificate metadata, validity, issuer chain |
| 12 | **Markdown Viewer** | md, markdown | 5 MB | Rendered HTML preview with syntax highlighting |
| 13 | **Map / Geo Viewer** | kml, kmz, geojson, gpx | 5 MB | Interactive SVG map, feature table, Google Maps links |
| 14 | **Archive Inspector** | zip, tar, gz, tgz | 500 MB | Virtual file browser, nested preview, byte-range fetching |

### Preview Access Paths

Files can be previewed from **four paths:**

1. **Explorer** → click attachment → preview modal
2. **Issue Panel** → click attachment → preview modal (via Forge Modal API)
3. **Explorer** → ZIP → nested file → preview modal
4. **Issue Panel** → ZIP → nested file → preview modal

### Image & Video Gallery

Uses `yet-another-react-lightbox` for a full-screen gallery experience:
- **Arrow keys** or swipe to navigate between images/videos
- **Zoom** with mouse wheel or pinch
- **Download** button in toolbar
- **Selection checkbox** - select/deselect files while previewing
- Images and videos from the same context are grouped into a single gallery

### PDF Viewer

Powered by `pdf.js` (Mozilla):
- Page-by-page lazy rendering
- Zoom controls
- Page number navigation
- Download button

### Word Document Viewer (.docx)

Powered by `docx-preview`:
- Full document rendering with styles, tables, images
- Scroll through entire document
- Download button

**Note:** Legacy `.doc` format is NOT supported (only `.docx`).

### Excel / Spreadsheet Viewer (.xlsx, .xls, .ods)

Powered by `SheetJS`:
- Multiple sheet tabs
- Column and row headers
- Search within sheet
- Supports `.xlsx`, `.xls`, and `.ods` (OpenDocument Spreadsheet)

### PowerPoint Viewer (.pptx, .ppsx)

- Slide-by-slide rendering
- Navigation between slides
- Supports `.pptx` and `.ppsx` (auto-play presentations)

### CSV / TSV Grid Viewer

- Spreadsheet-style grid display
- Column sorting
- Handles large files with virtualization

### Code & Text Viewer (80+ languages)

Powered by Prism.js with virtualized rendering:
- **Syntax highlighting** for 80+ languages (JavaScript, Python, Java, Go, Rust, SQL, YAML, Terraform, Solidity, and many more)
- **Line numbers** with click-to-select
- **Search** (Ctrl/Cmd+F) with match highlighting and navigation
- **Word wrap** toggle
- **Copy to clipboard**
- **Log file mode** - regex-based highlighting for `.log`, `.txt`, `.out`, `.err` files (20 MB limit)
- Special filename detection: `Dockerfile`, `Makefile`, `Jenkinsfile`, `.env`, `.gitignore`

### Audio Player

Custom HTML5 audio player:
- **Waveform visualization**
- **ID3 tag extraction** (artist, album, title, year)
- **Lyrics display** (from ID3 USLT tag)
- **Playback controls** - play/pause, seek, volume
- Supported formats: MP3, WAV, OGG, M4A, AAC, FLAC, OPUS

**Browser compatibility notes:**
- OGG: may not play in Safari
- WebM audio: may not play in Safari

### Email Viewer (.eml)

- Parses RFC 2822 email format
- Displays headers (From, To, Subject, Date)
- Renders email body (HTML or plain text)
- Lists email attachments

### Certificate Viewer (.pem, .crt, .cer)

Compact metadata viewer for X.509 certificates:
- Subject and Issuer details
- Validity period (Not Before / Not After)
- Serial number
- Signature algorithm
- Key usage

### Markdown Viewer (.md)

- Renders Markdown to styled HTML
- Code block syntax highlighting
- Tables, lists, headings, links
- Download original file

### Map / Geo Viewer (.kml, .kmz, .geojson, .gpx)

Interactive geographic data viewer - **100% offline**, no external map tile requests:

- **Bundled basemap** - Natural Earth 50m world map (country borders + coastlines)
- **SVG rendering** via d3-geo projections
- **Zoom/pan** - mouse wheel + drag, zoom buttons with Atlaskit icons
- **Feature table** - lists all geographic features with:
  - Type icon (📍 placemark, 📏 route, 📐 area)
  - Feature name
  - Measurement (coordinates for points, distance for lines, area for polygons)
  - "Maps" link - opens Google Maps via Forge router (with user confirmation prompt)
- **Feature interaction** - click/hover on map highlights table row and vice versa
- **KML style support** - renders stroke/fill colors from KML `<Style>` elements
- **KMZ support** - extracts KML from ZIP container (with decompression bomb protection)
- **Dynamic layout** - map/table split adjusts based on feature count (70/30 for ≤3 features, 60/40 for ≤6, 50/50 for more)
- **Graticule** - subtle latitude/longitude grid overlay
- **Security:** XML sanitization, CSS color validation, coordinate validation, depth limiting, prototype pollution guard

**Supported formats:**
| Format | Extension | Description |
|---|---|---|
| KML | `.kml` | Keyhole Markup Language (Google Earth) |
| KMZ | `.kmz` | Compressed KML (ZIP container) |
| GeoJSON | `.geojson` | Standard geographic JSON format |
| GPX | `.gpx` | GPS Exchange Format (tracks, routes, waypoints) |

### Archive Inspector (.zip, .tar, .gz)

Virtual file system browser for archives:

- **Surgical byte-range fetching** - only downloads the Central Directory (~64 KB), not the entire archive
- **Virtual folder navigation** - browse archive contents like a file manager
- **Nested preview** - click any supported file inside the archive to preview it
- **File metadata** - size, compressed size, modification date
- **Extract on demand** - individual files extracted only when opened
- Supports `.zip`, `.tar`, `.gz`, `.tgz`

### Preview Size Limits

| File Type | Max Preview Size |
|---|---|
| Images, PDF, Word, Excel, CSV, Email | 15 MB |
| Code files | 10 MB |
| Log files (.log, .txt, .out, .err) | 20 MB |
| PowerPoint | 50 MB |
| Video, Audio | 100 MB |
| Archives (browsing) | 500 MB |
| Markdown | 5 MB |
| Geo files | 5 MB |
| Certificates | 1 MB |

Files exceeding these limits show a "ghost state" (50% opacity) with a tooltip explaining the limit.

---

## 7. OCR (Live Text Recognition)

### How OCR Works

OCR is available for **image files** (jpg, png, gif, bmp, webp):

- Runs **entirely in the browser** using Tesseract.js (WebAssembly)
- Uses **offline language data** bundled with the app (no external network requests)
- **Does not store** OCR text in app storage
- Results are cached in the browser session for performance
- Automatic **language detection** based on script analysis

**To use OCR:**
1. Open an image in the preview gallery
2. Click the "OCR" / text icon button in the toolbar
3. The OCR panel slides in from the right
4. Text is extracted and displayed
5. Copy text to clipboard with one click

### Make Searchable (OCR → Comment)

If enabled by admins in Settings, users can **publish OCR text** into the Jira issue as a structured comment:

- Creates or updates a **single comment per attachment** (no spam - idempotent)
- Comment is formatted with metadata (filename, extraction date)
- Published text becomes **searchable via JQL** (`text ~ "search term"`)
- **Rate limited** per user to prevent abuse
- **Text length capped** for safety

**Requirements:**
- Admin must enable OCR publishing in Settings
- User must have comment permission on the issue
- Active license (trial or paid)

---

## 8. Licensing

Attachment Architect uses Atlassian Marketplace licensing.

| License State | Access Level | Details |
|---|---|---|
| **Trial** | **Full access** | All features available. Time-limited only - no feature restrictions during trial. |
| **Active** | **Full access** | All features available. |
| **Inactive** | **Read-only** | Browsing and viewing allowed. Destructive actions (delete, scan, settings changes) are blocked. Shows "Who turned out the lights?" message. |

**License check behavior:**
- License is checked on every page load
- Retries up to 3 times on network failure
- Falls back to "inactive" if all retries fail (safe default)
- Same license check applies to Admin Console, Explorer, and Issue Panel

---

## 9. Troubleshooting

### "No data" in Admin Console

- Run a scan first and wait for completion
- Check the Scans page for scan status and errors
- If scan failed, check the error message and retry

### "Permission denied" on delete

- Deletions run as the **current user** - Jira issue permissions apply
- You must have "Delete Attachments" permission in the project
- License must be active (trial or paid) - inactive license blocks all destructive actions

### Scan stuck or slow

- Large instances (100k+ issues) can take 10-30 minutes
- Check scan progress on the Scans page
- If stuck, use **Cancel** and retry
- **Factory Reset** in Settings → Danger Zone can clear all scan data for a fresh start

### Preview not loading

- Check file size against the [preview size limits](#preview-size-limits)
- Unsupported formats show 50% opacity with a tooltip
- For video: only MP4 and WebM are supported (MOV, AVI, MKV are not)
- For Word: only `.docx` is supported (legacy `.doc` is not)
- For archives: only ZIP, TAR, GZ are supported (RAR, 7z are not yet)

### Explorer returns no results

- Ensure you have at least one filter active (project, status, assignee, etc.)
- Check that your JQL is valid in Advanced mode
- The 50,000 issue safety limit may be blocking large queries - use the override option

### OCR not working

- OCR only works on image files (jpg, png, gif, bmp, webp)
- The image must be under 15 MB
- OCR runs in the browser - it may be slow on large images or low-powered devices
- WebAssembly must be enabled in your browser

---

## 10. Support

**Support portal:** [https://drinkits.atlassian.net/servicedesk/customer/portal/34](https://drinkits.atlassian.net/servicedesk/customer/portal/34)

**Quick links from the app:**
- Admin Console sidebar → **Help & Support** → Documentation / Report a Bug / Suggest a Feature

**When contacting support, include:**
- Jira site URL
- Which page you were on (Mission Control / Explorer / Issue Panel)
- What you clicked
- The exact error message (screenshot if possible)
- Approximate time and timezone
- Browser and OS version

---

## File Category Reference

Attachment Architect categorizes files into **20 categories** for filtering and analytics:

| Category | Icon | Example Extensions |
|---|---|---|
| Images | 🖼️ | jpg, png, gif, webp, svg, heic, raw, cr2 |
| Documents | 📄 | pdf, doc, docx, rtf, odt, txt, epub |
| Spreadsheets | 📊 | xls, xlsx, csv, tsv, ods, numbers |
| Presentations | 📽️ | ppt, pptx, pps, ppsx, odp, key |
| Code | 💻 | js, ts, py, java, go, rs, swift, kt, vue, svelte |
| Config | ⚙️ | json, yaml, yml, xml, toml, ini, env, dockerfile |
| Logs | 📝 | log, trace, out, err, debug |
| Data | 🗄️ | sql, dump, parquet, avro, sqlite, ipynb, har |
| Archives | 📦 | zip, rar, 7z, tar, gz, iso, jar, whl, apk |
| Video | 🎬 | mp4, avi, mov, mkv, webm, wmv |
| Audio | 🎵 | mp3, wav, ogg, m4a, flac, aac, opus |
| Design | 🎨 | fig, sketch, psd, ai, xd, blend |
| Sensitive | 🔐 | pem, key, p12, pfx, crt, gpg, kdbx, vault |
| Email | 📧 | eml, msg, mbox, ics, vcf |
| Diagrams | 📐 | drawio, vsd, vsdx, bpmn, puml, mermaid |
| Maps/Geo | 🗺️ | kml, kmz, geojson, gpx, shp |
| 3D Models | 🧊 | stl, obj, fbx, gltf, glb, dwg, dxf |
| Notebooks | 📓 | ipynb, rmd, qmd |
| Fonts | 🔤 | ttf, otf, woff, woff2 |
| Other | 📎 | Everything else |

---

**Last updated:** 2026-02
