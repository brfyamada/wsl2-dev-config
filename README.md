# wsl2-dev-config
## Project to instruct to install and configure the first step of wsl2 using ubuntu

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
bash -c "$(curl --fail --show-error --silent --location https://raw.githubusercontent.com/zdharma-continuum/zinit/HEAD/scripts/install.sh)"
```

- Paste in the end of .zshrc the next plugins
```bash
zinit light zdharma/fast-syntax-highlighting
zinit light zsh-users/zsh-autosuggestions
zinit light zsh-users/zsh-completions
```
- close and open terminal 

## Docker Instalation

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

## Install Kubectl
- Download the latest release with the command:
```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```

- Download the kubectl checksum file
```bash
curl -LO "https://dl.k8s.io/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
```

- Validate the kubectl binary against the checksum file:

```bash
echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check
```

- Install kubectl:
```bash
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

- Test to ensure the version you installed is up-to-date:
```bash
kubectl version --client
```
## Install K3D
- Run commands:
```bash
wget -q -O - https://raw.githubusercontent.com/k3d-io/k3d/main/install.sh | bash
```

## Installing ArgoCD in a K3d cluster
```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

- check argo process:
```bash
kubectl get all -n argocd
```

- ArgoCD port forward:
```bash
kubectl port-forward svc/argocd-server -n argocd 8081:443
```

- Get ArgoCD password, the default user is admin:
```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
```
- Importing a local docker image to the k3d cluster:
```bash
k3d image import {imageName}:{version} -c {clusterName}
```

## configuring ssh key in linux that you can use it with github and outhers:
- generate the key
```bash
ssh-keygen -t ed25519 -C "some comment"
```

- to check the public key content
```bash
cat /home/{put here your user}/.ssh/id_ed25519.pub
```

- to check the private key content
```bash
/home/{put here your user}/.ssh/id_ed25519
```

## Installing Go language (change to the last version if necessary):
```bash
wget https://dl.google.com/go/go1.14.2.linux-amd64.tar.gz
sudo tar -xvf go1.14.2.linux-amd64.tar.gz
sudo mv go /usr/local
```

- Paste the next lines to the .bashrc or .zshrc if it's your case:
```bash
export GOROOT=/usr/local/go
export GOPATH=$HOME/go
export PATH=$GOPATH/bin:$GOROOT/bin:$PATH
```

- testing the go instalation, after close and open terminal, type:
```bash
go version
```


## Installing Java

- Download the JDK Binaries:
```bash
$ wget https://download.java.net/java/GA/jdk13.0.1/cec27d702aa74d5a8630c65ae61e4305/9/GPL/openjdk-13.0.1_linux-x64_bin.tar.gz
$ tar -xvf openjdk-13.0.1_linux-x64_bin.tar.gz
$ mv jdk-13.0.1 /opt/
```

-  Setting JAVA_HOME and Path Environment Variables (Open .profile file from the home directory and add the following lines to it.)
```bash
JAVA_HOME='/opt/jdk-13.0.1'
PATH="$JAVA_HOME/bin:$PATH"
export PATH
```

* You can relaunch the terminal or execute source .profile command to apply the configuration changes.

- Step 3: Verify the Java Installation
```bash
$ java -version
```

## Installing Maven (step above is needed)

- Download the JDK Binaries:
```bash
$ wget https://mirrors.estointernet.in/apache/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz
$ tar -xvf apache-maven-3.6.3-bin.tar.gz
$ mv apache-maven-3.6.3 /opt/
```

-  Setting JAVA_HOME and Path Environment Variables (Open .profile file from the home directory and add the following lines to it.)
```bash
M2_HOME='/opt/apache-maven-3.6.3'
PATH="$M2_HOME/bin:$PATH"
export PATH
```

* You can relaunch the terminal or execute source .profile command to apply the configuration changes.

- Step 3: Verify the Java Installation
```bash
$ mvn -version
```