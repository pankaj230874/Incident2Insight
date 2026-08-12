# Incident2Insight Ecosystem

> Documented baseline for the **I2I Content Engine → Facebook Approval → Facebook Publisher** automation.

## Current Status

**Status: VALIDATED / WORKING**

The end-to-end Facebook content publishing flow has been successfully tested with content ID `I2I-001`.

Validated path:

```text
I2I Content Engine
        ↓
Google Sheets – Read Pending Row
        ↓
AI – Improve Caption
        ↓
Generate Branded Image
        ↓
Prepare Approval Data
        ↓
Google Sheets – Update Row
        ↓
Send Approval Email
        ↓
Human Approval
        ↓
Status = Approved
        ↓
Facebook Publisher
        ↓
Upload Photo + Caption
        ↓
Google Sheets – Update Row
        ↓
Status = Published
        ↓
Facebook Page
```

## Repository Structure

```text
I2I Content Engine/
├── README.md
├── docs/
│   ├── architecture.md
│   ├── 01-content-engine.md
│   ├── 02-approval-flow.md
│   ├── 03-facebook-publisher.md
│   ├── backup-checklist.md
│   ├── test-evidence.md
│   └── change-log.md
├── images/
│   ├── github-repo-current.png
│   └── README.md
└── workflows/
    └── README.md
```

## Key Design Principle

The Google Sheet is the workflow state store.

Typical lifecycle:

`GENERATED → Waiting Approval → Approved → Published`

The content ID (for example `I2I-001`) is the record key used across the workflow.

## Important

This repository documents the working configuration and provides a place for workflow exports and screenshots.

**Do not store API keys, access tokens, passwords, OAuth secrets, or other credentials in GitHub.**

The actual n8n workflow JSON exports should be added under `workflows/` after exporting them from n8n.
