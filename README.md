# Attachment Architect - User Guide (Jira Cloud)

This guide documents the **current, implemented** Attachment Architect functionality.

---

## Table of Contents

1. [Where to Find Attachment Architect](#1-where-to-find-attachment-architect)
2. [Admin Console (Mission Control + Command Deck)](#2-admin-console-mission-control--command-deck)
3. [Scanning (Index Build)](#3-scanning-index-build)
4. [Action Center](#4-action-center)
   - [Security Risks](#security-risks)
   - [Duplicates](#duplicates)
   - [Storage Hygiene](#storage-hygiene)
   - [Frozen Dinosaurs (Heat Index)](#frozen-dinosaurs-heat-index)
5. [Deep Analytics](#5-deep-analytics)
6. [Operations](#6-operations)
   - [Scans (History, Export)](#scans-history-export)
   - [Audit Log](#audit-log)
   - [Settings](#settings)
7. [Attachment Explorer (Public Global Page)](#7-attachment-explorer-public-global-page)
   - [Basic vs Advanced (Raw JQL)](#basic-vs-advanced-raw-jql)
   - [Live Explorer Safety Limits](#live-explorer-safety-limits)
   - [Selection (Ctrl/Cmd + Click, Shift + Click)](#selection-ctrlcmd--click-shift--click)
   - [Folders (Personal Collections)](#folders-personal-collections)
8. [Issue View Modules](#8-issue-view-modules)
   - [Attachments Issue Panel](#attachments-issue-panel)
   - [Attachment Activity (Issue Context)](#attachment-activity-issue-context)
9. [Preview & OCR](#9-preview--ocr)
   - [Preview Matrix](#preview-matrix)
   - [OCR (Live Text)](#ocr-live-text)
   - [Make Searchable (OCR → Comment)](#make-searchable-ocr--comment)
10. [Licensing](#10-licensing)
11. [Troubleshooting](#11-troubleshooting)
12. [Support](#12-support)

---

## 1. Where to Find Attachment Architect

### Admin Console (for Jira Admins)

Go to: **Jira settings → Apps → Attachment Architect**

This is the control room:
- Mission Control (KPIs + health)
- Scans + Scan History
- Action Center (Security / Duplicates / Hygiene / Heat Index)
- Deep Analytics
- Audit Log
- Settings

### Attachment Explorer (for all users)

Go to: **Apps → Attachment Explorer**

This is the user-facing explorer:
- Search attachments across Jira (Live mode)
- Filter and sort
- Preview files
- Manage personal folders
- Bulk actions (download / delete, if permitted)

### Issue View modules

Attachment Architect adds two issue-level modules:
- **Attachments** issue panel (a compact attachment viewer)
- **Attachment Activity** issue context panel (conditional)

---

## 2. Admin Console (Mission Control + Command Deck)

When you open Attachment Architect Admin Console, it opens on **Mission Control**.

Layout is a high-density “command deck”:
- Left sidebar for navigation
- Primary content with compact tables and charts
- Empty states and errors explain what went wrong in plain language

---

## 3. Scanning (Index Build)

### What a scan does

A scan builds an **attachment index** (metadata only) that powers:
- dashboards
- duplicates
- hygiene
- heat index
- analytics

### Scope

Admins can configure scope:
- **Full instance**
- **Specific projects**
- **JQL scope** (when enabled in the UI)

### Progress and cancellation

- Scans show live progress.
- You can cancel a scan; it stops at safe checkpoints.

---

## 4. Action Center

### Security Risks

Shows detected risks based on:
- filename patterns
- (optional) on-demand content scanning for supported files

You can:
- filter by severity
- open the issue containing the file
- scan file content when available

### Duplicates

Duplicates are grouped by **content hash**.

You can:
- view groups sorted by impact
- inspect where copies live
- delete selected duplicates (canonical/original copy is protected)

### Storage Hygiene

Detects “trash” attachments (low-value files), based on filename/type heuristics.

Deletion uses a safety flow:
1. **Backup strategy** step
2. **Delete** step (confirmation required)

### Frozen Dinosaurs (Heat Index)

Surfaces large files on stale issues (high cleanup priority).

---

## 5. Deep Analytics

Deep Analytics pages show storage trends and breakdowns, including:
- storage velocity (growth)
- usage by project
- usage by user
- usage by file type
- age distribution
- zombie projects (archive candidates)

---

## 6. Operations

### Scans (History, Export)

The Scans section includes:
- scan history list
- scan-to-scan comparison
- export of scan data (CSV)

### Audit Log

Audit Log records major actions, including:
- scans (started/completed/cancelled/failed)
- deletions
- settings changes

### Settings

Settings include implemented controls such as:
- enabling/disabling features
- scanning/security toggles
- OCR publishing settings (if enabled)
- “danger zone” reset (factory reset)

---

## 7. Attachment Explorer (Public Global Page)

### What it is

Attachment Explorer is a **live-only** explorer for all users.

It supports:
- searching and filtering attachments
- previewing
- bulk download
- deletion (subject to user permissions and licensing)
- personal folders

### Basic vs Advanced (Raw JQL)

Explorer has two modes:

- **Basic mode**: visual filters
- **Advanced mode**: raw JQL input

### Live Explorer safety limits

To prevent accidental “scan the universe” queries:
- Explorer enforces a **50,000 issue safety limit**
- There is a manual override flow (explicit user confirmation)

### Selection (Ctrl/Cmd + Click, Shift + Click)

Selection works like a normal desktop file manager:
- Click: select one row
- Ctrl/Cmd + click: toggle
- Shift + click: select a contiguous range

Selection survives sorting/filtering by tracking file IDs.

### Folders (Personal Collections)

Folders are personal collections for attachments.

You can:
- create / rename / delete folders
- add selected attachments to a folder
- remove attachments from a folder
- open a folder to view its contents

Limits (implemented):
- **Max folders per user:** 20
- **Max files per folder:** 500

Notes:
- Deleting a folder does **not** delete attachments from Jira issues.
- Folders are scoped to your Jira account.

---

## 8. Issue View Modules

### Attachments Issue Panel

A compact attachment viewer inside an issue.

You can:
- preview attachments
- select multiple
- bulk download
- add to folder
- delete (if permitted)

### Attachment Activity (Issue Context)

A contextual panel that shows attachment activity (for issues that qualify under display conditions). It is designed for deletion transparency.

---

## 9. Preview & OCR

### Preview Matrix

Supported previews depend on file type. Implemented preview types include:
- images
- videos (browser-supported formats)
- PDF
- DOCX
- spreadsheets (XLSX/XLS)
- code/text
- ZIP browsing with nested preview

### OCR (Live Text)

OCR is available for images:
- runs **entirely in the browser**
- uses offline assets
- does not store OCR text in app storage

### Make Searchable (OCR → Comment)

If enabled by admins, users can publish OCR text into the issue as a Jira comment so it becomes searchable via JQL.

Behavior:
- creates or updates a single structured comment per attachment (no spam)
- rate limited per user
- text length is capped

---

## 10. Licensing

Licensing affects destructive actions.

Implemented states:
- **Trial**: limited lifetime deletions
- **Active**: full access
- **Inactive**: read-only / restricted actions

---

## 11. Troubleshooting

### “No data” in Admin Console

- Run a scan and wait for completion.

### “Permission denied” on delete

- Deletions run as the current user; Jira permissions apply.
- Trial limits and license status can block deletion.

### Scan stuck or slow

- Large instances can take time.
- If a scan is stuck, use cancel and retry.
- Factory reset exists for recovery.

---

## 12. Support

Support portal: https://drinkits.atlassian.net/servicedesk/customer/portal/34

When contacting support, include:
- Jira site URL
- what page you were on (Mission Control / Explorer / Issue Panel)
- what you clicked
- the exact error message
- approximate time and timezone

---

**Last updated:** 2026-02
