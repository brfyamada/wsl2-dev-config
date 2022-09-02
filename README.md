# wsl2-dev-config
Project to instruct to install and configure the first step of wsl2 using ubuntu

- Installing zsh: 
```bash
sudo apt install zsh
```

- Installing zsh themes oh my sh:
```bash
sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
```

- Install Zinit to be able to install zsh plugins 
```bash
bash -c "$(curl --fail --show-error --silent --location https://raw.githubusercontent.com/zdharma-
continuum/zinit/HEAD/scripts/install.sh)"
```

- Paste in the end of .zshrc the next plugins
```bash
zinit light zdharma/fast-syntax-highlighting
zinit light zsh-users/zsh-autosuggestions
zinit light zsh-users/zsh-completions
```
- close and open terminal 

Docker Instalation

- install docker:
```bash
sudo apt update
sudo apt install apt-transport-https ca-certificates curl software-properties-common
sudo apt install build-essential
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt update
sudo apt install docker-ce
```

-If you are using Ubuntu 22.04 LTS, when you install Docker in WSL2 with the latest Ubuntu 22.04 LTS, you will notice that Docker will not start after running sudo service docker start. You will receive errors when starting a container, and sudo service docker status will tell you Docker is not running.

```bash
sudo update-alternatives --config iptables
Enter 1 to select iptables-legacy
``` 
- Start and execute
```bash
sudo usermod -aG docker $USER
sudo service docker start
sudo docker run hello-world
```

- Install docker compose 
```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version
```

Install K3D
- Run commands:
```bash
$ sudo wget https://github.com/rancher/k3d/releases/download/v3.0.0/k3d-linux-amd64 -O /usr/local/bin/k3d
$ sudo chmod +x /usr/local/bin/k3d
```

