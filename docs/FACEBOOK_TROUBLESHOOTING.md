# Facebook Graph API Troubleshooting Guide

## Purpose

Quick reference for diagnosing Facebook Graph API and n8n integration
issues.

## Error: (#10) pages_read_engagement required

**Symptoms** - Browser request fails - POST /{page-id}/feed returns
OAuthException

**Cause** - Wrong token (user token instead of Page token) - Missing
permission

**Fix** 1. Open Graph API Explorer. 2. Select the Page (not User). 3.
Generate a new token. 4. Ensure: - pages_show_list -
pages_read_engagement - pages_manage_posts 5. Verify:

``` http
GET /me/permissions
```

------------------------------------------------------------------------

## Error: (#200) Forbidden

### Cause

Authentication is incorrect.

### Verify

-   Authentication = None
-   POST request
-   Form URL Encoded body
-   access_token included in body

Correct endpoint:

``` text
https://graph.facebook.com/v25.0/{PAGE_ID}/feed
```

------------------------------------------------------------------------

## Invalid OAuth Access Token

### Cause

Expired or partially copied token.

### Fix

Generate a new Page token from Graph API Explorer.

------------------------------------------------------------------------

## Graph API Explorer works but n8n fails

Checklist:

-   Same API version?
-   Same Page ID?
-   Same access token?
-   POST not GET?
-   Authentication=None?
-   access_token sent in body?

------------------------------------------------------------------------

## Page token verification

``` http
GET /me?fields=id,name,access_token
```

------------------------------------------------------------------------

## Permission verification

``` http
GET /me/permissions
```

All required permissions must be granted.

------------------------------------------------------------------------

## Page lookup

``` http
GET /me
```

Should return the Page ID.

------------------------------------------------------------------------

## Test before n8n

Always test:

``` http
POST /{page-id}/feed
```

If Graph API Explorer cannot post, n8n will not post.

------------------------------------------------------------------------

## Common Mistakes

-   Using User token
-   Wrong Page ID
-   GET instead of POST
-   JSON instead of Form URL Encoded
-   Authentication set to Facebook Credential
-   Expired token

------------------------------------------------------------------------

## Final Working Configuration

Method: POST

Authentication: None

Content Type: Form URL Encoded

Fields:

-   message
-   access_token
