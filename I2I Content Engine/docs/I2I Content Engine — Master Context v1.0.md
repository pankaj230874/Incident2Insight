# Incident2Insight — I2I Content Engine
## Master Context v1.0

**Date:** 14 Aug 2026  
**Purpose:** Durable project handoff and working context for the I2I Content Engine automation.

---

## 1. Project Vision

Incident2Insight (I2I) is being developed as a reusable AI-powered content generation, approval, scheduling, and multi-platform publishing system.

Immediate POC platforms:
1. Facebook Page — Incident2Insight
2. LinkedIn — personal profile publishing is technically proven; LinkedIn Page publishing is next.

Long-term objective: a client-demonstrable platform using Lovable + Supabase as the configuration/front-end layer while n8n handles automation/orchestration.

The product should ultimately be positioned as an:

> **AI-powered Content Operations Engine**

rather than simply an n8n workflow that posts to social platforms.

---

## 2. Target Architecture

```text
Research / Content Ideas
        ↓
I2I Content Engine
        ↓
Content Generation
        ↓
Human Approval
        ↓
Content Queue / Scheduling
        ↓
Platform-specific Publisher
   ↙              ↘
Facebook        LinkedIn
   ↓              ↓
Published       Published
```

Future multi-platform architecture:

```text
                 ┌── Facebook Publisher
                 │
I2I Content ─────┼── LinkedIn Publisher
Engine            │
                 ├── Future Platform
                 │
                 └── Future Platform
```

Keep the Content Engine and publishing channels logically separate.

---

## 3. Current Lovable Frontend

Existing Lovable landing page:

`https://pankajp-automation-hq.lovable.app/`

Current functionality:
- LinkedIn icon is interactive.
- AI / "Talk to My AI" is interactive and connected to a Vapi agent.
- Sections include AI Services, AI Systems, Automation, Leadership, Certifications, and Connect.
- Existing showcased solutions include ContractPulse, KYC Screener, AI workflows/intelligent automation, finance systems modernization, and operational intelligence.

The landing page is not yet a fully developed production website and there is no registered custom domain at this stage.

Long-term concept:

```text
Lovable Frontend
      ↓
Configuration / Admin UI
      ↓
Supabase
      ↓
n8n Automation Layer
      ↓
Platform APIs
```

Potential configuration areas:
- Platforms
- Content
- Scheduling
- Approval
- Credentials
- Analytics

Do not migrate the current POC to Supabase prematurely. First stabilize the existing workflows.

---

## 4. Facebook POC — Current State

Facebook publishing is working end-to-end.

Current flow:

```text
Generated Content
      ↓
Google Sheet
      ↓
Approval Email
      ↓
Human changes status
      ↓
Approved
      ↓
Publisher workflow
      ↓
Facebook Page
```

The approval email contains Topic, AI-generated caption, Image, and Status.

A Facebook test post successfully appeared on the Incident2Insight Page.

Facebook workflows have been backed up/documented in GitHub.

---

## 5. Google Sheets Architecture

The current system depends on **two Google Sheets/sheet structures**.

Important decision:

> Both sheets must remain separately managed and simultaneously associated using `Content_ID`.

Do not casually merge the two sheets.

Human approval is dependent on Google Sheet status changes.

The Google Sheet is the current operational queue until a future Supabase layer is implemented.

---

## 6. Current n8n Workflow Structure

There are three relevant workflows in the overall content automation setup.

All three workflows are currently on **manual trigger** for the POC.

The intended future behavior is scheduled/automated execution.

### Working constraint

> **DO NOT suggest node changes unnecessarily. Continue with the existing workflow and fix/configure it incrementally.**

Working style:
- Work node-by-node.
- Ask for a screenshot when exact n8n configuration needs inspection.
- Give exact expressions/mappings.
- Test one node before moving to the next.
- Preserve working logic.
- Avoid multiple simultaneous changes.
- Distinguish current POC from future architecture.

---

## 7. GitHub Repository

GitHub repository:

`Incident2Insight`

Relevant structure:

```text
I2I Content Engine/
│
├── docs/
│   ├── 01-content-engine.md
│   ├── 02-approval-flow.md
│   ├── 03-facebook-publisher.md
│   ├── architecture.md
│   ├── backup-checklist.md
│   ├── change-log.md
│   └── test-evidence.md
│
├── images/
│   ├── README.md
│   └── github-repo-current.png
│
├── workflows/
│   ├── 1-Facebook_Content_Approval_V2.json
│   ├── 2-Facebook_Content_Publisher.json
│   └── README.md
│
└── README.md
```

This repository should be the durable system-of-record for architecture, workflow backups, documentation, test evidence, screenshots, and change history.

Back up workflow JSON whenever a meaningful working version is reached.

---

## 8. LinkedIn Developer App

Existing LinkedIn Developer application:

**I2I**

It is a standalone app.

Current OAuth redirect URLs:

```text
https://www.linkedin.com/developers/tools/oauth/redirect
https://n8n.coachshwetagupta.com/rest/oauth2-credential/callback
```

Current OAuth scopes visible:

```text
openid
profile
w_member_social
email
```

`w_member_social` supports publishing on behalf of the authenticated member.

Never commit LinkedIn Client Secret or other credentials to GitHub.

---

## 9. LinkedIn Organization/Page Access

Long-term requirement: publish to the Incident2Insight LinkedIn Page.

The LinkedIn Developer portal shows **Community Management API**.

Access had already been requested approximately 3–4 months before this work.

LinkedIn currently prevents requesting additional products because there are already provisioned/pending products associated with the application.

The portal displayed a message indicating that some API products require the product to be the only product on an application for legal/security reasons. Similar disabled/request behavior appeared when hovering over several requested products.

A new LinkedIn app was considered but paused.

Current decision:

> Continue reviewing the existing LinkedIn application and its existing/pending privileges before creating another application.

Do not create another LinkedIn app merely as a workaround without reviewing the current state.

---

## 10. LinkedIn Personal Profile POC

LinkedIn personal-profile publishing is technically proven.

An older LinkedIn workflow successfully published to the personal profile.

One initial test published without content because the `Create a post` node was not mapped correctly. After mapping the content field correctly, content was successfully published.

The test post was then deleted because it was not intended to remain visible.

Therefore:

> **LinkedIn personal-profile publishing is proven.**

The current objective is to connect the I2I Content Engine properly to this capability.

---

## 11. Current LinkedIn Content Publisher Workflow

A duplicate of the existing Workflow B was created for LinkedIn.

Current workflow name:

**Linked_Content_Publisher**

Current flow:

```text
Schedule Trigger
      ↓
Get row(s) in sheet
      ↓
If
      ↓
Sort
      ↓
Limit
      ↓
AI Agent1
      ↓
Update row in sheet
      ↓
Create a post
```

AI model:

**OpenRouter Chat Model**

The workflow is being converted into:

> **I2I → LinkedIn Content Publisher**

rather than remaining a generic copy of Workflow B.

---

## 12. Current LinkedIn Google Sheet Columns

The LinkedIn publishing sheet contains columns similar to:

```text
Content_ID
Topic
Context
Key_Facts
Angle
Audience
Format
Status
LinkedIn_Post
Hashtags
Infographic_Title
Infographic_Prompt
Infographic_Image
Created_Date
Error
LinkedIn_Status
LinkedIn_Scheduled_Date
LinkedIn_Publish...
LinkedIn_Published_Date
```

Current example:

```text
Content_ID = I2I-001
Topic = Finance report automation
Status = GENERATED
LinkedIn_Status = READY
LinkedIn_Scheduled_Date = 13/08/2026
```

---

## 13. Current LinkedIn Node Naming Standard

Recommended names:

```text
LinkedIn — Schedule Trigger

I2I — Get LinkedIn Queue

I2I — Content Eligible?

I2I — Sort by Scheduled Date

I2I — Select Next Post

I2I — LinkedIn Content Optimizer

I2I — Update LinkedIn Status

LinkedIn — Publish Post

I2I — Content Model
```

Intended flow:

```text
LinkedIn — Schedule Trigger
        ↓
I2I — Get LinkedIn Queue
        ↓
I2I — Content Eligible?
        ↓
I2I — Sort by Scheduled Date
        ↓
I2I — Select Next Post
        ↓
I2I — LinkedIn Content Optimizer
        ↓
I2I — Update LinkedIn Status
        ↓
LinkedIn — Publish Post
```

---

## 14. Current LinkedIn Eligibility Node

Current node:

**I2I — Content Eligible?**

Condition 1:

```javascript
{{ $json["LinkedIn_Status"] }}
```

equals:

```text
READY
```

Condition 2 parses the Google Sheet date, which is stored as `DD/MM/YYYY`.

Working left expression:

```javascript
{{ DateTime.fromFormat($json["LinkedIn_Scheduled_Date"], "dd/MM/yyyy", { zone: "Asia/Kolkata" }).startOf('day').toMillis() }}
```

Operator:

```text
is smaller than or equal to
```

Working right expression:

```javascript
{{ DateTime.now().setZone("Asia/Kolkata").startOf('day').toMillis() }}
```

This was tested successfully.

Result:

```text
True Branch — 1 item
```

Therefore:

> **I2I — Content Eligible? is WORKING.**

Do not modify this node unless a new issue appears.

---

## 15. Timezone Decision

The n8n Schedule Trigger had been displaying:

```text
America/New_York
```

while Google Sheet timestamps used:

```text
+05:30
```

The system is being operated from India.

Therefore business scheduling/date comparison should use:

```text
Asia/Kolkata
```

The current eligibility logic explicitly uses `Asia/Kolkata`.

A future hardening task should review workflow-level timezone configuration so trigger execution aligns consistently with India time.

---

## 16. Immediate Next Step

The current working node is:

**I2I — Content Eligible?**

The next node to inspect is:

### `I2I — Sort by Scheduled Date`

Objective:

> If multiple LinkedIn records are eligible, select the correct next post based on scheduled date.

Then:

```text
Sort
 ↓
Select Next Post
 ↓
AI Content Optimizer
 ↓
Update Sheet
 ↓
LinkedIn Publish
```

Do not redesign the workflow.

Continue node-by-node.

---

## 17. Future Posting Schedule

Target behavior:

> Approximately one post every third day, or configurable scheduling.

Future configuration should support:
- Every 3 days
- Specific days such as Mon/Thu/Sat
- Custom schedule

---

## 18. Future Content Intelligence / Research Agent

A major future evolution is a research-driven content idea engine.

Desired architecture:

```text
Research Agent
      ↓
Identify relevant industry topics/trends
      ↓
Generate content ideas
      ↓
Score / select ideas
      ↓
I2I Content Engine
      ↓
Generate post
      ↓
Human Approval
      ↓
Schedule
      ↓
Publish
```

A separate AI research agent is desired.

Research should support professional positioning around:
- Finance systems
- Finance operations
- Process transformation
- Operational excellence
- AI automation
- AI agents
- Workflow automation
- Low-code/no-code
- Business + technology integration
- Intelligent systems
- Incident2Insight philosophy

Objectives:
- regular visibility
- professional positioning
- brand building
- Incident2Insight awareness
- useful industry insights
- marketing
- thought leadership

---

## 19. Two Content Input Modes

### Mode A — Human-specified content

A Google Sheet entry remains available for specific content.

Example:

```text
Topic:
Finance Report Automation

Context:
Manual report generation and email distribution

Angle:
Mindset over technology
```

The system generates/optimizes the post around that input.

### Mode B — Autonomous research-driven content

The Research Agent automatically researches and generates ideas based on:
- industry relevance
- current trends
- I2I positioning
- posting schedule
- previous content
- audience
- content gaps

Then the idea enters the same content pipeline.

Conceptually:

```text
Human Idea
     ↘
       I2I Content Engine
     ↗
Research Agent
```

---

## 20. Human Approval

Human approval remains part of the system.

Current mechanism:

```text
AI Generated Content
        ↓
Google Sheet
        ↓
Approval Email
        ↓
Human changes status
        ↓
Publisher
```

Do not remove human approval prematurely.

Future Lovable/Supabase version could provide:

```text
Lovable Dashboard
       ↓
Approve / Reject / Edit
```

while retaining the same backend orchestration concept.

---

## 21. Platform Configuration Concept

Eventually the client-facing Lovable interface could expose:

```text
Platform Configuration
  ├── Facebook
  ├── LinkedIn
  └── Other platforms

Content Configuration
  ├── Content source
  ├── Brand voice
  ├── Topics
  └── Formats

Scheduling
  ├── Frequency
  ├── Days
  └── Time

Approval
  ├── Human approval
  └── Approval rules

Credentials
  ├── OAuth
  └── API configuration

Analytics
  ├── Published
  ├── Failed
  └── Engagement
```

This should eventually allow a potential client to configure the platform without rebuilding n8n workflows.

---

## 22. Current Priority Roadmap

### PHASE 1 — LinkedIn POC

1. Fix/validate eligibility — **DONE**
2. Sort correct scheduled content — **NEXT**
3. Select one post
4. AI content optimization
5. Update LinkedIn status
6. Correct LinkedIn Create Post mapping
7. Test publishing
8. Verify post
9. Record test evidence
10. Back up workflow JSON

### PHASE 2 — LinkedIn Page

1. Review existing LinkedIn app
2. Review Community Management API request
3. Determine current organization/page access
4. Verify organization publishing permissions/scopes
5. Test publishing to Incident2Insight LinkedIn Page

### PHASE 3 — Content Intelligence

1. Research agent
2. Idea generation
3. Topic scoring
4. Content calendar
5. Automated scheduling

### PHASE 4 — Platform Hardening

1. Error handling
2. Duplicate prevention
3. Retry handling
4. Publishing status
5. Logging
6. Audit trail
7. Monitoring

### PHASE 5 — Lovable + Supabase

1. Configuration UI
2. Platform mappings
3. Content queue
4. Approval dashboard
5. Scheduling
6. Credential status
7. Analytics
8. Client demo mode

---

## 23. Current Status Summary

| Component | Status |
|---|---|
| Facebook Page publishing | Working POC |
| Facebook approval flow | Working |
| Google Sheet queue | Working |
| Human approval | Working |
| LinkedIn personal profile publishing | Proven |
| LinkedIn API OAuth | Working for current personal-profile test |
| LinkedIn Page publishing | Pending access/configuration |
| LinkedIn Content Eligible node | Working |
| LinkedIn Sort | Next |
| LinkedIn publisher workflow | Being hardened |
| Research Agent | Future |
| Scheduled 3-day cadence | Future |
| Lovable landing page | Existing |
| Lovable + Supabase platform | Future |
| GitHub documentation | Started |

---

## 24. Key Design Principle

The end product should communicate:

```text
Research
   ↓
Intelligence
   ↓
Content
   ↓
Approval
   ↓
Scheduling
   ↓
Multi-platform Publishing
   ↓
Analytics
```

The n8n workflows are the automation/orchestration layer underneath this system.

The client-facing concept is the **Incident2Insight Content Engine**.

---

## 25. Immediate Continuation Instruction

When continuing this project in a new ChatGPT conversation:

> **Continue from `I2I — Sort by Scheduled Date`. Do not redesign the workflow. Inspect the current node configuration and guide me step-by-step.**

The user prefers exact, incremental troubleshooting/configuration rather than wholesale workflow redesign.

---

## 26. Security Reminder

Never place the following into GitHub:
- LinkedIn Client Secret
- OAuth access tokens
- Google credentials
- n8n credential secrets
- OpenRouter API keys
- Supabase service-role keys
- Vapi private keys
- Facebook access tokens

Workflow JSON backups should be checked for credential leakage before committing.

Use placeholders where necessary, for example:

```text
YOUR_LINKEDIN_CLIENT_ID
YOUR_LINKEDIN_CLIENT_SECRET
YOUR_N8N_CREDENTIAL
YOUR_OPENROUTER_API_KEY
```

---

**Document status:** Master project handoff  
**Version:** v1.0  
**Last updated:** 14 Aug 2026
