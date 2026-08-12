# n8n Workflow Backups

This folder is reserved for **exported n8n workflow JSON files**.

Recommended files:

```text
I2I_Content_Engine_Approval.json
I2I_Facebook_Content_Publisher.json
```

## Export Procedure

In n8n:

1. Open the workflow.
2. Use the workflow menu.
3. Export/download the workflow as JSON.
4. Save the file here.
5. Do not include credential secrets in the repository.
6. Commit the JSON to GitHub.

## Versioning

Use Git commits to preserve known-good versions.

Example:

```text
backup: validated I2I Facebook publishing flow
```

Before editing a working workflow, create a backup commit.
