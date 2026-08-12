# Test Evidence

## End-to-End Validation

### Test ID

`I2I-001`

### Content

`Finance report automation`

### Expected Flow

```text
Generated
→ Waiting Approval
→ Approved
→ Facebook Published
```

### Results

| Check | Result |
|---|---|
| Pending content read | PASS |
| AI Facebook transformation | PASS |
| Final caption extraction | PASS |
| Branded image generation | PASS |
| Approval email sent | PASS |
| Image visible in approval email | PASS |
| Human approval | PASS |
| Approved row detected by publisher | PASS |
| Facebook photo upload | PASS |
| Facebook post visible | PASS |
| Facebook URL returned | PASS |
| Facebook Post ID captured | PASS |
| Published status written to sheet | PASS |

## Evidence Screenshot

`images/github-repo-current.png` documents the repository state at the time of this documentation update.

Additional execution screenshots should be added to `images/` as the workflow evolves.

## Current Baseline

The validated baseline is the configuration that successfully published `I2I-001`.

Any future change should be tested against the same acceptance criteria.
