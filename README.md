# Docker
How to get start with Docker


## Uninstall old versions
Older versions of Docker were called docker, docker.io, or docker-engine. If these are installed, uninstall them:
 ```sh
sudo apt-get remove docker docker-engine docker.io containerd runc
```

## Set up the repository
1- Update the apt package index and install packages to allow apt to use a repository over HTTPS:

```sh
sudo apt-get update
```
```sh
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```
    
2- Add Docker’s official GPG key:

```sh
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```
 3- Use the following command to set up the stable repository. To add the nightly or test repository, add the word nightly or test (or both) after the word stable in the commands below. Learn about nightly and test channels.

```sh
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

## Install Docker Engine
Update the apt package index, and install the latest version of Docker Engine and containerd, or go to the next step to install a specific version:
```sh
sudo apt-get update
```
```sh
sudo apt-get install docker-ce docker-ce-cli containerd.io
 ```
 ## Set permissions
 ```sh
 sudo usermod -a -G docker "user"   // change "user" to your user
 ```
 ```sh
 sudo reboot
 ```
 ## Test
 ```sh
 docker images
 ```
 
 ## Create an application
Create a example Flask File with this content, and save as app.py in your workdir:

app.py
```sh
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello_world():
    return "<p>Hello, World!</p>"
```


## Create a Virtual Env
```sh
python3 -m venv .venv
```
```sh
source .venv/bin/activate
```

## Install and run Flask
```sh
pip install flask
```
```sh
flask run
```

## Download Python Image
```sh
python3 --version
```
```sh
docker pull python:3.8.12-bullseye
```

## Create Requirements File
```sh
pip freeze > requirements.txt
```

## Create Docker File
Create a Docker File with this content, and save as Dockerfile in your workdir:

Dockerfile
```sh
FROM python:3.8.12-bullseye

WORKDIR /app

COPY requirements.txt .

RUN pip install -r requirements.txt

EXPOSE 5000

ENV FLASK_ENV development

COPY app.py .

CMD ["flask", "run", "--host", "0.0.0.0"]
```

## Docker Build Image
```sh
docker build -t flask-app:dev-0.0.1 .
```

# Test
```sh
docker images |grep flask-app
```

## Create Container
```sh
docker run -d -P flask-app:dev-0.0.1
```

## Test
```sh
docker ps
```

Open in a web browser:
localhost:PORT

## Execute a command in a container
```sh
docker exec "HASH" ls //change "HASH" to your container hash
```

## Enter in a container
```sh
docker exec -it "HASH" bash //change "HASH" to your container hash
```
