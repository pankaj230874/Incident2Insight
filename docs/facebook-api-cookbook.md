# Facebook Graph API Cookbook (n8n)

## Publish Text Post

POST

``` text
https://graph.facebook.com/v25.0/{page-id}/feed
```

Fields

-   message
-   access_token

------------------------------------------------------------------------

## Publish Photo

POST

``` text
https://graph.facebook.com/v25.0/{page-id}/photos
```

Fields

-   url
-   caption
-   access_token

------------------------------------------------------------------------

## Delete a Post

DELETE

``` text
https://graph.facebook.com/v25.0/{post-id}
```

Field

-   access_token

------------------------------------------------------------------------

## Read Page Details

GET

``` text
https://graph.facebook.com/v25.0/{page-id}
```

------------------------------------------------------------------------

## Read Feed

GET

``` text
https://graph.facebook.com/v25.0/{page-id}/feed
```

------------------------------------------------------------------------

## Read Comments

GET

``` text
https://graph.facebook.com/v25.0/{post-id}/comments
```

------------------------------------------------------------------------

## Reply to Comment

POST

``` text
https://graph.facebook.com/v25.0/{comment-id}/comments
```

Fields

-   message
-   access_token

------------------------------------------------------------------------

## Page Insights

GET

``` text
https://graph.facebook.com/v25.0/{page-id}/insights
```

------------------------------------------------------------------------

## Suggested n8n Flow

Trigger → AI generates content → Human approval → HTTP Request (POST
/feed) → Store post ID → Notify Slack/Email

------------------------------------------------------------------------

## Reusable HTTP Request Template

Method: POST

Authentication: None

Body: Form URL Encoded

Fields:

message={{\$json.message}}

access_token={{\$env.FACEBOOK_PAGE_TOKEN}}

------------------------------------------------------------------------

## Production Recommendations

-   Store tokens in n8n Credentials or environment variables.
-   Refresh long-lived tokens periodically.
-   Log Graph API response IDs.
-   Retry transient failures.
-   Maintain one HTTP Request node template for all Page operations.
