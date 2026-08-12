# I2I Automation Architecture

## 1. Purpose

The Incident2Insight ecosystem automates the journey from an approved content idea to a published Facebook post while retaining human approval before publication.

## 2. Core Components

| Component | Role |
|---|---|
| Google Sheets | Content queue and publishing state |
| n8n | Workflow orchestration |
| Google Gemini Chat Model | Facebook caption transformation |
| Bannerbear | Branded image generation |
| Gmail | Human approval notification |
| Facebook Graph API | Facebook publishing |
| GitHub | Documentation, workflow backup and version history |

## 3. State Model

```text
GENERATED
   │
   ▼
Waiting Approval
   │
   ├── Approved ──► Publisher ──► Published
   │
   └── Not approved / unchanged
```

## 4. Content Record

The tested record is:

- ID: `I2I-001`
- Topic: `Finance report automation`
- Source context: `Manual report generation and email distribution`
- Key facts: `Python, automated report + email`
- Angle: `Mindset over technology`

The Facebook caption is generated from the source LinkedIn content rather than manually rewritten in the sheet.

## 5. Image Handling

The workflow originally received a Google Drive file URL.

For reliable rendering in the approval email, the workflow converts the Drive file URL into a browser-accessible thumbnail/view URL.

The working approach was to extract the Drive file ID and construct a direct image URL.

The exact expression currently used in the workflow should be preserved in the n8n export and documented in the workflow notes.

## 6. Failure Boundaries

The Facebook Publisher includes separate logic for:

- caption missing
- image URL present
- image URL absent
- photo upload failure
- text-only fallback

This allows the publisher to use an image-post route when an image is available and a text-post route otherwise.
