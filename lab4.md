# Azure Flask Deployment Guide — Starting From Part 2 (Connect to VM)

This guide continues from Part 2 onward.
It assumes your Azure VM has already been created successfully.

---

# PART 2 — Connect to VM

## Step 8 — Open VM Resource

After deployment click:

```text
Go to Resource
```

---

## Step 9 — Copy Public IP Address

Find:

```text
Public IP Address
```

Example:

```text
20.55.xx.xx
```

---

## Step 10 — Connect Using SSH

Open PowerShell or terminal and run:

```bash
ssh azureuser@YOUR_PUBLIC_IP
```

Example:

```bash
ssh azureuser@20.55.xx.xx
```

Type:

```text
yes
```

Enter your password.

You should now see:

```text
azureuser@myvm:~$
```

---

# PART 3 — Install Docker

## Step 11 — Update Packages

```bash
sudo apt update
```

---

## Step 12 — Install Docker

```bash
sudo apt install docker.io -y
```

---

## Step 13 — Start Docker

```bash
sudo systemctl start docker
```

---

## Step 14 — Enable Docker

```bash
sudo systemctl enable docker
```

---

## Step 15 — Add User to Docker Group

```bash
sudo usermod -aG docker $USER
```

---

## Step 16 — Refresh Session

```bash
newgrp docker
```

---

## Step 17 — Verify Docker Installation

```bash
docker --version
```

You should see Docker version output.

---

# PART 4 — Run a Flask Docker Application

We will use a ready-made Flask Docker image.

---

## Step 18 — Pull Flask Docker Image

```bash
docker pull tiangolo/uwsgi-nginx-flask:python3.11
```

Wait for image download.

---

## Step 19 — Run Flask Container

```bash
docker run -d -p 80:80 tiangolo/uwsgi-nginx-flask:python3.11
```

Explanation:

* `-d` → Run container in background
* `80:80` → Map web traffic to container

---

## Step 20 — Check Running Containers

```bash
docker ps
```

You should see:

```text
STATUS = Up
```

This means the container is running.

---

# PART 5 — Open Flask Application

## Step 21 — Open Browser

Open:

```text
http://YOUR_VM_PUBLIC_IP
```

Example:

```text
http://20.55.xx.xx
```

You should now see the Flask application.

---

## Step 22 — If Website Does Not Open

Go to:

```text
Azure Portal → VM → Networking
```

Click:

```text
Add inbound port rule
```

Fill:

| Field    | Value |
| -------- | ----- |
| Port     | 80    |
| Protocol | TCP   |
| Action   | Allow |

Click:

```text
Add
```

Wait 1 minute and refresh the browser.

---

# PART 6 — Create Azure App Service

## Step 23 — Search App Services

In Azure search bar type:

```text
App Services
```

---

## Step 24 — Create Web App

Click:

```text
+ Create → Web App
```

---

# PART 7 — Configure Web App

## Step 25 — Configure Basics

Use:

| Field               | Value              |
| ------------------- | ------------------ |
| Subscription        | Azure for Students |
| Resource Group      | Create New         |
| Resource Group Name | flask-rg           |
| Name                | unique app name    |
| Publish             | Docker Container   |
| Operating System    | Linux              |
| Region              | North Europe       |

Example app name:

```text
my-flask-app-123
```

---

## Step 26 — Pricing Plan

Choose:

* Free F1
  OR
* cheapest available student plan

---

# PART 8 — Configure Docker Container

## Step 27 — Open Container Settings

Click:

```text
Next : Container
```

---

## Step 28 — Fill Docker Configuration

| Field               | Value                                              |
| ------------------- | -------------------------------------------------- |
| Image Source        | Other container registries                         |
| Access Type         | Public                                             |
| Registry Server URL | [https://index.docker.io](https://index.docker.io) |
| Image and Tag       | tiangolo/uwsgi-nginx-flask:python3.11              |
| Port                | 80                                                 |
| Startup Command     | Leave empty                                        |

---

# PART 9 — Deploy Application

## Step 29 — Review and Create

Click:

```text
Review + Create
```

Azure validates the settings.

---

## Step 30 — Create Deployment

Click:

```text
Create
```

Azure will:

* create App Service
* pull Docker image
* start Flask container

Wait 5–10 minutes.

---

# PART 10 — Open Azure Website

## Step 31 — Go to Resource

Click:

```text
Go to Resource
```

---

## Step 32 — Open Website URL

Find:

```text
Default Domain
```

Example:

```text
https://my-flask-app-123.azurewebsites.net
```

Open it in browser.

---

# RESULT

You should now see:

✅ Flask application running
✅ Docker container deployed successfully
✅ Azure App Service working
✅ Public website accessible

---

# HOW TO CHECK APPLICATION STATUS

## Check Running Docker Containers

Inside VM:

```bash
docker ps
```

If container is running:

```text
STATUS = Up
```

---

## Check Azure Website

Open:

```text
https://yourapp.azurewebsites.net
```

If website opens:

✅ Application is running successfully.

---

## Check Azure Logs

Go to:

```text
App Service → Monitoring → Log Stream
```

This shows:

* startup logs
* Docker logs
* Flask errors
* deployment status

---

# FINAL ARCHITECTURE

```text
Azure VM
   ↓
Docker Flask Container
   ↓
Azure App Service
   ↓
Public Website URL
```

---

# Common Errors and Fixes

| Problem                 | Fix                     |
| ----------------------- | ----------------------- |
| Website not opening     | Open inbound port 80    |
| Container stopped       | Check docker logs       |
| Azure Application Error | Check Log Stream        |
| Wrong image name        | Verify Docker image tag |
| Slow startup            | Wait 5–10 minutes       |

---

# Useful Commands

## Show Running Containers

```bash
docker ps
```

## Show All Containers

```bash
docker ps -a
```

## View Container Logs

```bash
docker logs CONTAINER_ID
```

## Restart Container

```bash
docker restart CONTAINER_ID
```

---
