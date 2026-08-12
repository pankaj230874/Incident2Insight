# Backup & Recovery Checklist

## Before Any Major Workflow Change

- [ ] Export the current n8n workflow as JSON.
- [ ] Save the export under `workflows/`.
- [ ] Record the export date.
- [ ] Take a screenshot of the complete workflow canvas.
- [ ] Take screenshots of critical nodes.
- [ ] Record credentials by **name only**; never store secrets.
- [ ] Commit the backup to GitHub.

## Critical Nodes to Screenshot

### Content Engine

- Google Sheets – Read Pending Row
- If – Pending Row Found
- Set – Prepare Content Data
- AI – Improve Caption
- Set – Extract Final Caption
- Generate Branded Image
- Image polling/status nodes
- Set – Prepare Approval Data
- Google Sheets – Update Row
- Send Approval

### Publisher

- Google Sheets – Read Approved Row
- If – Approved Row Found
- If – Caption Not Empty
- If – Image URL Exists
- Facebook – Upload Photo
- Facebook – Post Text Only
- Set – Prepare Update Data
- Google Sheets – Update Row
- Set – Capture Publish Failure

## Recovery Principle

The safest recovery artifact is the **n8n JSON export**.

Screenshots document configuration visually, but they are not a restorable workflow.

Therefore:

```text
n8n JSON export = primary backup
screenshots       = visual evidence
README/docs       = operational documentation
GitHub            = version history
```

## Security

Never commit:

- Facebook access tokens
- API keys
- Google OAuth credentials
- Bannerbear API keys
- n8n credential exports containing secrets
- passwords
- personal authentication data

Use n8n credentials and environment/secret management instead.
