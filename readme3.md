# Docker Flask Application Deployment

This project demonstrates how to deploy a Flask web application using Docker on a cloud virtual machine.

## Project Overview

The application is containerized using Docker and deployed on an Ubuntu virtual machine hosted in the cloud.

The Flask application contains:

* Home route (`/`)
* Custom route (`/how-are-you`)

The application runs inside a Docker container and is exposed through port mapping.

---

# Technologies Used

* Ubuntu 22.04
* Docker
* Python
* Flask
* Azure/OpenStack VM

---

# Step 1 — Create Virtual Machine

Create an Ubuntu 22.04 virtual machine in Azure/OpenStack.

Open inbound ports:

* 22 (SSH)
* 80 (HTTP)

Connect to VM using SSH:

```bash
ssh username@VM_PUBLIC_IP
```

---

# Step 2 — Install Docker

Update packages:

```bash
sudo apt-get update
```

Install required packages:

```bash
sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common
```

Add Docker GPG key:

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

Add Docker repository:

```bash
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```

Install Docker:

```bash
sudo apt-get update
sudo apt-get install docker-ce -y
```

Verify installation:

```bash
docker --version
```

---

# Step 3 — Pull Ubuntu Docker Image

```bash
docker pull ubuntu
```

Check images:

```bash
docker images
```

---

# Step 4 — Run Ubuntu Container

```bash
docker run -dit -p 80:80 --name username ubuntu
```

Check running containers:

```bash
docker ps
```

---

# Step 5 — Install Apache Inside Container

Enter container:

```bash
docker exec -it username sh
```

Update packages:

```bash
apt-get update
```

Install Apache:

```bash
apt-get install apache2 -y
```

Start Apache:

```bash
service apache2 start
```

Check Apache status:

```bash
service apache2 status
```

Exit container:

```bash
exit
```

Open browser:

```text
http://VM_PUBLIC_IP
```

---

# Step 6 — Create Docker Image

Create custom image from container:

```bash
docker commit -m "added apache2 web server" -a "yourname" username apacheimage
```

Verify image:

```bash
docker images
```

---

# Step 7 — Clone Flask Application

```bash
git clone https://github.com/airowireNetworks/devops-web-app-2.git simple-webapp-flask
```

Move into project folder:

```bash
cd simple-webapp-flask
```

---

# Step 8 — Flask Application Code

Example Flask application:

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def main():
    return "Welcome!"

@app.route('/how-are-you')
def hello():
    return 'I am good, how about you?'

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=8080)
```

---

# Step 9 — Create Dockerfile

Create Dockerfile:

```bash
nano Dockerfile
```

Dockerfile content:

```dockerfile
FROM python:3.9-slim

WORKDIR /opt

COPY . .

RUN pip install flask

EXPOSE 8080

CMD ["python", "app.py"]
```

---

# Step 10 — Build Docker Image

```bash
docker build -t myimage .
```

Verify image:

```bash
docker images
```

---

# Step 11 — Run Flask Container

Remove old containers if necessary:

```bash
docker rm -f flaskapp
```

Run Flask container:

```bash
docker run -d -p 80:8080 --name flaskapp myimage
```

Check running containers:

```bash
docker ps
```

Check logs:

```bash
docker logs flaskapp
```

---

# Step 12 — Configure Azure Firewall

Open inbound TCP port 80 in Azure/OpenStack networking settings.

---

# Step 13 — Access Application

Homepage:

```text
http://20.219.124.9
```

Second route:

```text
http://20.219.124.9/how-are-you
```

---

# Docker Port Mapping

Container runs Flask on port:

```text
8080
```

Docker mapping:

```text
80:8080
```

Meaning:

| Host VM Port | Container Port |
| ------------ | -------------- |
| 80           | 8080           |

---

# Useful Docker Commands

Check containers:

```bash
docker ps
```

Check images:

```bash
docker images
```

View logs:

```bash
docker logs flaskapp
```

Stop container:

```bash
docker stop flaskapp
```

Remove container:

```bash
docker rm flaskapp
```

Remove image:

```bash
docker rmi myimage
```

---

# Project Outcome

This project demonstrates:

* Docker installation
* Docker image creation
* Container deployment
* Flask application deployment
* Docker networking
* Azure VM deployment
* Cloud-based container hosting

---

# Author

Your Name
