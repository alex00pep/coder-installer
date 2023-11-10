# coder-installer
Repo to streamline/automate the installation of Coder

## Step1: Make sure you have Docker and Docker Compose Installed on a Linux-based machine.

## Step 2: Use below commands to automate the installation 
```bash
git clone https://github.com/coder/coder-installer.git
cd coder-installer
export CODER_DATA=$HOME/.config/coderv2-docker
export DOCKER_GROUP=$(getent group docker | cut -d: -f3)
mkdir -p $CODER_DATA
export CODER_ACCESS_URL=http://<linuxmachine_ip>:7080
export CODER_WILDCARD_ACCESS_URL=="*.coder.example.com"

docker compose down --rmi all --remove-orphans --volumes
docker compose up -d

```

## Step 3: Configure user login via remote Coder instance 
Visit the web ui via the configured url http://<linuxmachine_ip>:7080/. You can add /login to the base url to create the first user via the ui.

## Step 4: Create your first workspace template and run an example application
Follow the on-screen instructions to log in and create your first template and workspace. As example: please follow this repository [https://github.com/alex00pep/python-devcontainer](https://github.com/alex00pep/python-devcontainer)
You can open the remote workspace using the browser. Open the embedded terminal and run the app with:
```bash
cd python-devcontainer
flask run --host 0.0.0.0 --port 9000  --reload
```


## Step 5: Forward app ports to your local Windows machine using PowerShell
This way you can access the app from your local machine.

```powerShell
# Powershell
# Install Coder CLI
curl -fsSL https://coder.com/install.sh | sh

# Login to remote Coder instance using Coder CLI and your credentials
coder login http://<linuxmachine_ip>:7080/
coder port-forward <yourworkspace> --tcp 9000:9000
```

You should see the app in your browser:

http://localhost:9000/ping


## Find more information here: [Coder](https://coder.com/)