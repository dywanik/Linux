# Cheat sheet for Docker on Ubuntu
### Add repository and install (ce = community edition). Sometimes it is good to use particular version (especially if using legacy code)
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get update
sudo apt-get install -y docker-ce=18.06.1~ce~3-0~ubuntu
sudo apt-mark hold docker-ce
```
### verify
```
sudo docker version
```
### info about docker, i.e., storage driver
```
docker info
```
### daemon config file
```
/etc/docker/daemon.json
```
### run container in detached mode (does not use prompt)
```
docker run -d image_name
```
### print containers (stopped -a)
```
docker ps
```
### start/stop container image_id
```
docker container start/stop image_id
```
### remove container
```
docker container rm id
```
### run container with particular name
```
docker run -d --name nginx image_name
```
### decide when restart container (no [default]/on-failure/unless-stopped/always)
```
docker run --restart always
```
### expose port over the network (publish)
```
docker run -p <host_port>:<container_port>
```
### remove container aftaer it exits
```
docker run -rm container_id
```
### override logging driver to write to system log
```
docker run --log-driver syslog nginx
```
### initialise swarm cluster under particular address (private IP)
```
docker swarm init --advertise-addr
```
### list nodes connected to the cluster
```
docker node ls
```
### backuping swarm - stop docker, backup all files from
```
/var/lib/docker/swarm
```
