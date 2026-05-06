ssh username@<Public-IP>
sudo apt update && sudo apt upgrade -y
sudo apt install python3.12-venv
sudo apt install python3-pip
sudo apt install python3-venv
python3 -m venv venv
pip install --upgrade pip
source venv/bin/activate
git clone https://github.com/mmumshad/simple-webapp-flask.git
cd simple-webapp-flask
pip install -r requirements.txt
python app.py
use public ip and port to connect the vm
<img width="993" height="621" alt="image" src="https://github.com/user-attachments/assets/e5ff8531-81bf-4e99-be21-f02e4fcae1f9" />
