# wsl2-dev-config
Project to instruct to install and configure the first step of wsl2 using ubuntu

- Installing zsh: 

sudo apt install zsh

- Installing zsh themes:

sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"


- install docker:

sudo apt update
sudo apt install apt-transport-https ca-certificates curl software-properties-common
sudo apt install build-essential
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt update
sudo apt install docker-ce
sudo service docker start
sudo docker run hello-world

- If using zsh export variable to .zshrc
export DOCKER_HOST=unix:///var/run/docker.sock


- Install docker compose 

sudo curl -L "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version

