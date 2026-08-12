# Facebook Approval Flow

## Objective

Provide a human checkpoint before Facebook publication.

## Google Sheet

The approval workflow updates the content record with:

| Field | Value |
|---|---|
| ID | Content ID |
| Topic | Content topic |
| Draft Caption | AI-generated Facebook caption |
| Image URL | Normalized image URL |
| Status | `Waiting Approval` |

## Approval Email

The email subject follows the pattern:

```text
Facebook Approval Required - <Topic>
```

The body displays the generated caption and the branded image.

The current working email confirms that the image renders correctly.

## Approval Action

The current implementation intentionally uses the Google Sheet as the approval control.

Human action:

```text
Waiting Approval → Approved
```

No approval button/webhook is required at this stage.

## Important

Do not change the working image URL conversion logic without testing the approval email again.

The image rendering problem was caused by the original Google Drive URL not being directly renderable by the email client. The normalized URL solved the issue.
