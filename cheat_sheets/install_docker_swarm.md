# Cheat sheet for installing Docker Swarm on Master, Node1 and Node2
### On all three nodes
```
sudo apt-get update
sudo apt-get -y install apt-transport-https ca-certificates curl gnupg-agent software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
sudo apt-get update
sudo apt-get install -y docker-ce=5:18.09.5~3-0~ubuntu-bionic docker-ce-cli=5:18.09.5~3-0~ubuntu-bionic containerd.io
```
#### add user to docker group
```
sudo usermod -a -G docker cloud_user
```
#### relog and verify
```
docker version
```
### on master
```
docker swarm init --advertise-addr <swarm manager private IP>
```
### check command for joining:
```
docker swarm join-token worker
```
### on Nodes
```
docker swarm join --token <some_token> <swarm manager private IP>:2377
```
### on Master verify nodes
```
docker node ls
```
### search for an <image>, e.g., "ubuntu"
```
docker search ubuntu
```
