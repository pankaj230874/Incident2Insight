# I2I Content Engine

## Purpose

The Content Engine prepares content for Facebook publication and routes it through human approval.

## Tested Workflow

```text
Manual Trigger
    ↓
Google Sheets – Read Pending Row
    ↓
If – Pending Row Found
    ↓
Set – Prepare Content Data
    ↓
AI – Improve Caption
    ↓
Set – Extract Final Caption
    ↓
Generate Branded Image
    ↓
Image readiness / polling logic
    ↓
Set – Prepare Approval Data
    ↓
Google Sheets – Update Row
    ↓
Send Approval
```

## AI Transformation

The AI step uses two chat messages:

### System

The model is instructed to act as a professional social media copywriter for the Incident2Insight Facebook Page and transform the supplied LinkedIn post into a polished Facebook post.

Important constraints include:

- preserve the original message and key insight
- preserve factual meaning
- preserve Incident2Insight professional voice
- make the opening engaging for Facebook
- use shorter paragraphs
- make the language natural and conversational
- do not invent facts, statistics, achievements or claims
- do not mention LinkedIn
- return only the final Facebook post text

### User

The user message supplies:

```text
Topic: {{ $json.Topic }}

Content to transform:

{{ $json.LinkedIn_Post }}
```

## Output

The AI output is passed to `Set – Extract Final Caption` and stored as `finalCaption`.

The final caption is then carried into the approval record as `Caption`.

## Image Generation

The branded image is generated from the infographic/content information associated with the content record.

The resulting image URL is normalized before it is used in the approval email.

## Approval

The approval email contains:

- Topic
- AI Generated Caption
- Image
- Status
- Approval instruction

The human approval action is intentionally simple:

```text
Waiting Approval → Approved
```

The publisher workflow then detects the approved row.
