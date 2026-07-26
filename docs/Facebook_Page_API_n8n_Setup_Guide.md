# Facebook Page API + n8n Setup Guide

## (Incident2Insight Working Reference)

## Step 1 - Create a Meta App

1.  Go to https://developers.facebook.com/
2.  Click **My Apps**
3.  Click **Create App**
4.  Choose **Manage everything on your Page**
5.  Name the app **Incident2Insight Marketing**
6.  Create the app.

------------------------------------------------------------------------

## Step 2 - Add Required Permissions

Add only these permissions:

-   `pages_show_list`
-   `pages_read_engagement`
-   `pages_manage_posts`

------------------------------------------------------------------------

## Step 3 - Connect Facebook Account

Open:

`Tools → Graph API Explorer`

Choose the Meta App:

`Incident2Insight Marketing`

Click **Generate Access Token** and approve all permission prompts.

------------------------------------------------------------------------

## Step 4 - Select the Page

Under **User or Page**, select:

`Incident2Insight`

Do **not** select your personal profile.

------------------------------------------------------------------------

## Step 5 - Verify Permissions

Run:

``` http
GET /me/permissions
```

Expected:

-   `pages_show_list` → granted
-   `pages_read_engagement` → granted
-   `pages_manage_posts` → granted

------------------------------------------------------------------------

## Step 6 - Verify Page Access Token

Run:

``` http
GET /me?fields=id,name,access_token
```

Expected:

``` json
{
  "id": "1081348701733494",
  "name": "Incident2Insight",
  "access_token": "EAAPD..."
}
```

Copy the **Page Access Token**.

------------------------------------------------------------------------

## Step 7 - Verify the Page

Run:

``` http
GET /me
```

Expected:

``` json
{
  "id": "1081348701733494",
  "name": "Incident2Insight"
}
```

------------------------------------------------------------------------

## Step 8 - Test Posting in Graph API Explorer

**Method**

``` text
POST
```

**Endpoint**

``` text
/1081348701733494/feed
```

**Body Parameter**

  Name      Value
  --------- ---------------------------------
  message   Testing from Graph API Explorer

Expected response:

``` json
{
  "id": "1081348701733494_xxxxxxxxx"
}
```

If you receive an ID, posting is working.

------------------------------------------------------------------------

## Step 9 - Configure n8n

Use an **HTTP Request** node.

**Do not use the Facebook Graph API Credential for publishing.**

### Method

`POST`

### URL

``` text
https://graph.facebook.com/v25.0/1081348701733494/feed
```

### Authentication

`None`

### Send Body

`ON`

### Body Content Type

`Form URL Encoded`

### Body Fields

  Name           Value
  -------------- ----------------
  message        Hello from n8n
  access_token   EAAPD...

Expected response:

``` json
{
  "id": "1081348701733494_xxxxxxxxx"
}
```

------------------------------------------------------------------------

## Step 10 - Verify the Post

Refresh your Facebook Page. The new post should appear immediately.

------------------------------------------------------------------------

# Common Errors

### Session expired

**Cause:** User token expired.

**Solution:** Generate a new token.

------------------------------------------------------------------------

### `pages_read_engagement` required

**Cause:** Invalid or incorrect token (typically a user token instead of
a Page token).

**Solution:** Generate a fresh **Page Access Token** from Graph API
Explorer.

------------------------------------------------------------------------

### Forbidden (#200)

**Cause:** Incorrect authentication method or missing Page token.

**Solution:**

-   Authentication = None
-   Body Content Type = Form URL Encoded
-   Include `access_token` in the request body.

------------------------------------------------------------------------

### Invalid OAuth access token

**Cause:** Token copied incorrectly or expired.

**Solution:** Generate a new token and copy it completely.

------------------------------------------------------------------------

# Useful API Endpoints

## Check permissions

``` http
GET /me/permissions
```

## Get Page information

``` http
GET /me
```

## Get Page Access Token

``` http
GET /me?fields=id,name,access_token
```

## Publish a text post

``` http
POST /1081348701733494/feed
```

Parameters:

-   `message`
-   `access_token`

## Upload a photo

``` http
POST /1081348701733494/photos
```

Parameters:

-   `url`
-   `caption`
-   `access_token`

------------------------------------------------------------------------

# Recommended Production Workflow

``` text
AI (Claude/OpenAI/Gemini)
        │
        ▼
Generate Content
        │
        ▼
Human Approval (Optional)
        │
        ▼
Retrieve Page Access Token
        │
        ▼
POST /{page-id}/feed
        │
        ▼
Log Post ID
        │
        ├── Google Sheets
        ├── Supabase
        ├── LinkedIn
        ├── Instagram
        └── X
```

------------------------------------------------------------------------

# Key Lessons Learned

-   Create a Meta App using **Manage everything on your Page**.
-   Use a **Page Access Token**, not just a user token.
-   Confirm all three required permissions are granted.
-   Verify posting works in Graph API Explorer before configuring n8n.
-   In n8n, use:
    -   Authentication: **None**
    -   Body Content Type: **Form URL Encoded**
    -   Body fields: `message` and `access_token`
-   Keep the Graph API version consistent (e.g., `v25.0`) across Graph
    API Explorer and n8n.
