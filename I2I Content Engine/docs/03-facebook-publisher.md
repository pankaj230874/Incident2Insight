# Facebook Publisher

## Purpose

Publish approved content from the I2I Google Sheet to the Incident2Insight Facebook Page.

## Tested Workflow

```text
Manual Trigger
    ↓
Google Sheets – Read Approved Row
    ↓
If – Approved Row Found
    ↓
If – Caption Not Empty
    ↓
If – Image URL Exists
    ├── TRUE → Facebook – Upload Photo
    │              ↓
    │       Set – Prepare Update Data
    │              ↓
    │       Google Sheets – Update Row
    │
    └── FALSE → Facebook – Post Text Only
```

Failure paths are captured separately.

## Image Path

The validated production-like test used the image path:

```text
Approved Row
    ↓
Image URL Exists = TRUE
    ↓
Facebook – Upload Photo
    ↓
Published
```

## Successful Test

Content ID:

`I2I-001`

Topic:

`Finance report automation`

Result:

- Facebook post created successfully
- Branded infographic displayed
- AI-generated Facebook caption displayed
- Facebook URL written back to Google Sheet
- Published date written back
- Facebook Post ID written back
- Status changed to `Published`

## Sheet Result

The tested row now contains publication tracking information.

This is the final confirmation that the publisher and tracking logic are connected correctly.

## Keep Stable

The following working branches should not be changed casually:

1. Approved row detection
2. Caption validation
3. Image URL existence check
4. Photo upload route
5. Text-only fallback route
6. Google Sheets publication update
