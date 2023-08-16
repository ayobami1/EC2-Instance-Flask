# EC2-Instance-Flask
Easy Step by Step to Setup Flask on EC2 AWS

## Table of Contents
- [Step 1](#step-1)
- [Step 2](#step-2)
- [Step 3](#step-3)
- [Run Terminal Commands](#run-terminal-commands)
- [app.py](#app-py)
- [Run Gunicorn](#run-gunicorn)
- [Create systemd Service](#create-systemd-service)
- [Run Nginx](#run-nginx)
- [Edit Nginx Configuration](#edit-nginx-configuration)
- [Restart Nginx](#restart-nginx)

## Step 1
```bash
# Launch a new instance on your EC2 AWS.
```

## Step 2 
Choose your preferred on-demand instance type (e.g., t3.micro).

## Step 3
```bash
# Set up your Security Group:
# - SSH (Port Range: 22)
# - HTTP (Port Range: 80)
# - HTTPS (Port Range: 442)
# - Custom (Port Range: 8080)
```


## Run Terminal Commands


# Run the following commands in your EC2 instance terminal:

```bash
sudo apt-get update
sudo apt-get install python3-venv
mkdir helloworld
cd helloworld
python3 -m venv venv
source venv/bin/activate
pip install flask

```


## app.py

```python
# Paste the following code into `app.py` (you can put this in a separate code file):

from flask import Flask
app = Flask(__name__)

@app.route("/display", methods=["GET"])
def display():
    return "Code Successfully Run. 😎"

@app.route('/')
def hello_world():
    return "Hello Ayocrypt 😎"

if __name__ == "__main__":
    app.run()
```

## Run Gunicorn
### Run the following commands:

```bash
pip install gunicorn
gunicorn -b 0.0.0.0:8000 app:app
```

## Create systemd Service

```bash

# Create and edit a systemd service:

sudo nano /etc/systemd/system/helloworld.service

```
```bash

# Add the following content:

[Unit]
Description=Gunicorn instance to serve helloworld
After=network.target

[Service]
User=ubuntu
Group=www-data
WorkingDirectory=/home/ubuntu/helloworld
ExecStart=/home/ubuntu/helloworld/venv/bin/gunicorn -b localhost:8000 app:app
Restart=always

[Install]
WantedBy=multi-user.target
```


```bash
# Run the following commands:

sudo systemctl daemon-reload
sudo systemctl start helloworld
sudo systemctl enable helloworld
```

## Run Nginx

```bash
# Run a test:

curl localhost:8000

```

```bash
# Install and configure Nginx:

sudo apt-get install nginx
sudo systemctl start nginx
sudo systemctl enable nginx

```

## Edit Nginx Configuration

```bash
# Edit the Nginx default configuration:

sudo nano /etc/nginx/sites-available/default
```

```bash

# Replace the default server configuration with:

upstream flaskhelloworld  {
    server    127.0.0.1:8000;
}

server {
    listen 80 default_server;
    listen [::]:80 default_server;

    root /var/www/html;
    index index.html index.htm index.nginx-debian.html;
    server_name _;

    location / {
        proxy_pass http://flaskhelloworld;
    }
}
```


## Restart Nginx

```bash

# Restart Nginx:

sudo systemctl restart nginx
```

###  Use your public address to access your Flask application.

