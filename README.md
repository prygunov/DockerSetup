# DockerSetup
Install docker:

sudo apt-get update

sudo apt-get install \
      ca-certificates \
      curl \
      gnupg \
      lsb-release
    
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io

sudo docker run hello-world


Postinstall steps

sudo groupadd docker
 
sudo usermod -aG docker $USER
 
newgrp docker 
 
docker run hello-world
 
sudo systemctl enable docker.service

sudo systemctl enable containerd.service
 
Enable remote api:

sudo systemctl edit docker.service

[Service]
ExecStart=
ExecStart=/usr/bin/dockerd -H fd:// -H tcp://0.0.0.0:2375

sudo systemctl daemon-reload

sudo systemctl restart docker.service

apt install net-tools 
sudo netstat -lntp | grep dockerd

curl http://localhost:2375/images/json must be with response

OPEN PORT:

sudo iptables -I INPUT -p tcp -s 0.0.0.0/0 --dport 2375 -j ACCEPT - open port 2375

.\pscp.exe -r ubuntu@158.101.202.201:/home c:\temp\
