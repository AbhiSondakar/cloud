# Simple Flask Web Application Deployment on Azure VM

This project demonstrates how to deploy a simple Flask web application on an Azure Ubuntu Virtual Machine using Python virtual environments.

---

# Prerequisites

* Azure Virtual Machine (Ubuntu)
* Public IP address attached to the VM
* SSH access enabled
* Port `8080` allowed in Azure Network Security Group (NSG)

---

# Step 1: Connect to Azure VM

SSH into the VM using:

```bash
ssh username@<Public-IP>
```

Example:

```bash
ssh azureuser@20.219.66.132
```

---

# Step 2: Update System Packages

```bash
sudo apt update && sudo apt upgrade -y
```

---

# Step 3: Install Required Packages

Install Python virtual environment and pip:

```bash
sudo apt install python3.12-venv -y
sudo apt install python3-pip -y
sudo apt install python3-venv -y
```

---

# Step 4: Create Python Virtual Environment

Create virtual environment:

```bash
python3 -m venv venv
```

Activate virtual environment:

```bash
source venv/bin/activate
```

You should now see:

```bash
(venv)
```

---

# Step 5: Upgrade pip

```bash
pip install --upgrade pip
```

---

# Step 6: Clone GitHub Repository

```bash
git clone https://github.com/mmumshad/simple-webapp-flask.git
```

Move into project directory:

```bash
cd simple-webapp-flask
```

---

# Step 7: Install Project Dependencies

```bash
pip install -r requirements.txt
```

---

# Step 8: Run Flask Application

Start the Flask server:

```bash
python app.py
```

Expected output:

```bash
* Running on all addresses (0.0.0.0)
* Running on http://127.0.0.1:8080
* Running on http://10.0.0.5:8080
```

---

# Step 9: Configure Azure NSG Rule

Open port `8080` in Azure Portal.

Go to:

Azure Portal → Virtual Machine → Networking

Add inbound rule:

| Setting          | Value |
| ---------------- | ----- |
| Source           | Any   |
| Source Port      | *     |
| Destination      | Any   |
| Destination Port | 8080  |
| Protocol         | TCP   |
| Action           | Allow |
| Priority         | 1000  |

Save the rule.

---

# Step 10: Access the Application

Open browser:

```text
http://<Public-IP>:8080
```

Example:

```text
http://20.219.66.132:8080
```

---

# Verify Application

If deployment is successful, the browser displays:

```text
Welcome!
```

---

# Useful Commands

Check if application is listening on port 8080:

```bash
ss -tulnp | grep 8080
```

Check firewall status:

```bash
sudo ufw status
```

Deactivate virtual environment:

```bash
deactivate
```

---

# Project Structure

```text
simple-webapp-flask/
│
├── app.py
├── requirements.txt
├── Dockerfile
├── README.md
└── LICENSE
```

---

# Technologies Used

* Python 3
* Flask
* Azure Virtual Machine
* Ubuntu Linux
* GitHub

---

# Author

Deployment and setup completed using Azure Ubuntu VM and Flask.
