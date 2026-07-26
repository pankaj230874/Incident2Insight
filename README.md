# Incident2Insight

![n8n](https://img.shields.io/badge/n8n-Automation-orange)

![Facebook](https://img.shields.io/badge/Facebook-Graph_API-blue)

![Status](https://img.shields.io/badge/Status-Production_Ready-brightgreen)

Automation knowledge base and reusable workflows.

---

## Facebook Automation

### Architecture
                           FACEBOOK PAGE                                                
                                  │
                                  │
                         Graph API Explorer
                                  │
                                  ▼
                      Facebook Graph API v23+
                                  │
                    Page Access Token (OAuth)
                                  │
                                  ▼
                      n8n HTTP Request Node
                                  │
          ┌───────────────────────┼───────────────────────┐
          │                       │                       │
          ▼                       ▼                       ▼
      Create Post            Upload Image          Read Comments
          │                       │                       │
          └───────────────────────┼───────────────────────┘
                                  │
                                  ▼
                           Facebook Page

🏗️ Architecture

```mermaid
flowchart TD

A[Facebook Page] --> B[Graph API Explorer]
B --> C[Facebook Graph API v23+]
C --> D[Page Access Token]

D --> E[n8n HTTP Request]

E --> F[Create Text Post]
E --> G[Upload Image]
E --> H[Read Comments]

F --> I[Facebook Page]
G --> I
H --> I
```
### Documentation
- [Facebook Page API n8n Setup Guide](docs/facebook-page-api-n8n-setup-guide.md)
- [Facebook API Cookbook](docs/facebook-api-cookbook.md)
- [Facebook Troubleshooting](docs/facebook-troubleshooting.md)

### n8n Examples
- [Post Text](examples/Post_Text.json)
- [Upload Image](examples/Upload_Image.json)
- [Read Comments](examples/Read_Comments.json)
- [Get Insights](examples/Get_Insights.json)

### Images
Screenshots used in the documentation.

### Workflows
Reusable n8n workflows ready to import.
