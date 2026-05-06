# Azure App Service CI/CD Deployment using GitHub

This project demonstrates how to deploy a Python Flask application to Azure App Service using GitHub CI/CD integration.

---

# Prerequisites

Before starting, ensure you have:

- Azure Account
- GitHub Account
- Flask Application Code in GitHub Repository
- Azure Subscription

---

# Step 1 — Login to Azure Portal

Open:

```text
https://portal.azure.com
```

Login with your Azure account.

---

# Step 2 — Create Resource Group

1. Search for:
   ```text
   Resource Groups
   ```

2. Click:
   ```text
   Create
   ```

3. Enter:
   - Resource Group Name:
     ```text
     lab3
     ```
   - Region:
     Choose nearby region

4. Click:
   ```text
   Review + Create
   ```

5. Click:
   ```text
   Create
   ```

---

# Step 3 — Create Azure App Service

1. Search:
   ```text
   App Services
   ```

2. Click:
   ```text
   Create
   ```

3. Fill the details:

| Option | Value |
|---|---|
| Resource Group | lab3 |
| Name | Any unique name |
| Publish | Code |
| Runtime Stack | Python 3.9 |
| Region | North Europe |

4. Click:
   ```text
   Review + Create
   ```

5. Click:
   ```text
   Create
   ```

6. Wait for deployment to complete.

---

# Step 4 — Open App Service

After deployment:

1. Click:
   ```text
   Go to Resource
   ```

---

# Step 5 — Open Deployment Center

1. In the left-side menu:
   ```text
   Deployment → Deployment Center
   ```

2. Click:
   ```text
   Deployment Center
   ```

---

# Step 6 — Configure GitHub Deployment

Inside Deployment Center:

1. Select:
   ```text
   Source → GitHub
   ```

2. Click:
   ```text
   Authorize
   ```

3. Login to GitHub.

4. Grant permissions.

---

# Step 7 — Select GitHub Repository

Choose:

| Option | Value |
|---|---|
| Organization | Your GitHub username |
| Repository | lab3app |
| Branch | main |

---

# Step 8 — Configure Workflow

1. Workflow option:
   ```text
   Add Workflow
   ```

2. Authentication Type:
   ```text
   User-assigned identity
   ```

---

# Step 9 — Create Managed Identity

If identity dropdown shows:
```text
No results
```

Follow these steps:

## Create Identity

1. Search:
   ```text
   Managed Identities
   ```

2. Click:
   ```text
   Create
   ```

3. Fill details:

| Field | Value |
|---|---|
| Subscription | Azure subscription |
| Resource Group | lab3 |
| Region | Same as App Service |
| Name | github-identity |

4. Click:
   ```text
   Review + Create
   ```

5. Click:
   ```text
   Create
   ```

6. Wait for deployment.

---

# Step 10 — Select Managed Identity

1. Return to:
   ```text
   App Service → Deployment Center
   ```

2. Refresh identity dropdown.

3. Select:
   ```text
   github-identity
   ```

---

# Step 11 — Save Configuration

Click:
```text
Save
```

Azure will now:
- Connect GitHub repository
- Create GitHub Actions workflow
- Start automatic deployment

---

# Step 12 — Monitor Deployment Logs

Go to:
```text
Deployment Center → Logs
```

Check:
- Build status
- Deployment progress
- Errors if any

---

# Step 13 — Open Web Application

1. Go to:
   ```text
   Overview
   ```

2. Click:
   ```text
   Default Domain URL
   ```

Example:
```text
https://yourapp.azurewebsites.net
```

Your Flask app should now run successfully.

---

# Step 14 — Modify Application

Edit:
```html
home.html
```

Example:

```html
<h1>Hello from Azure CI/CD</h1>
```

---

# Step 15 — Commit and Push Changes

Open terminal inside project folder.

Run:

```bash
git add .
```

Then:

```bash
git commit -m "Updated homepage"
```

Then:

```bash
git push origin main
```

---

# Step 16 — Automatic Deployment

After pushing:
- GitHub Actions workflow starts
- Azure redeploys app automatically
- Updated application becomes live

---

# Step 17 — Verify Updated Website

Refresh your Azure website.

You should now see updated content.

---

# CI/CD Workflow Summary

```text
Write Code
    ↓
Push to GitHub
    ↓
GitHub Actions Triggered
    ↓
Azure Builds Application
    ↓
Azure Deploys Application
    ↓
Live Website Updated
```

---
ask application to Azure App Service with automated CI/CD deployment using GitHub.
