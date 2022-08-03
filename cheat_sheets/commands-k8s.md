# Cheat sheet for k8s flawless usage
### get all nodes in cluster
```
kubectl get nodes
```
### describe node and look for errors, constant "starting" and/or check flags
```
kubectl describe node [name]
```
### show all pods on the machine
```
kubectl get pods --all-namespaces
kubectl get pods -A
```
### show all info on a pod
```
kubectl describe pod [name] -n kube-system
```
### show logs for a pod
```
kubectl logs [name] -n kube-system
```
### "restart" a pod - there is NO "kubectl pod restart" - we need to scale it up and then terminate malfunctioning pods
```
kubectl scale deployment [name] --replicas=4 -n kube-system
kubectl scale deployment [name] --replicas=2 -n kube-system
```
### node information
```
kubectl get nodes -o wide
```
### kubernetes configuration file
```
kubectl -n kube-system get cm kubeadm-config -oyaml
```
### detected "cgroupfs" as the Docker cgroup driver. The recommended driver is "systemd".
```
sudo vim /etc/docker/daemon.json

{
  "exec-opts": ["native.cgroupdriver=systemd"]
}

sudo systemctl restart docker
```
### remove kubernetes
```
sudo kubeadm reset
sudo apt-get purge kubeadm kubectl kubelet kubernetes-cni kube*   
sudo apt-get autoremove  
sudo rm -rf ~/.kube
sudo reboot
```
### revert kubeadm init OR kubeadm join
```
sudo kubeadm reset
```
### entering into pod
```
kubectl exec -it [podName] -- /bin/bash
```
### create pod from yaml
```
kubectl apply -f pods01.yaml
```
### delete pod
```
kubectl delete -f pods01.yaml
```
### example of deployment
```
cat << EOF | kubectl apply -f -
apiVersion: apps/v1
kind: Deployment
metadata:
  name: store-products
  labels:
    app: store-products
spec:
  replicas: 4
  selector:
    matchLabels:
      app: store-products
  template:
    metadata:
      labels:
        app: store-products
    spec:
      containers:
      - name: store-products
        image: linuxacademycontent/store-products:1.0.0
        ports:
        - containerPort: 80
EOF
```
### get list of deployments
```
kubectl get deployments
```
### get detailed description of deployment
```
kubectl describe deployment nginx-deployment
```
### example service
```
cat << EOF | kubectl apply -f -
kind: Service
apiVersion: v1
metadata:
  name: store-products
spec:
  selector:
    app: store-products
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
EOF
```
### get list of all services or of particular ones
```
kubectl get svc
kubectl get services
kubectl get svc store-products
```
### create new namespace
```
kubectl create namespace new-namespace with auto-update (after change occurs)
```
### print all pods in new-namespace
```
kubectl get pods -n new-namespace -w
```
### scaling particular deployment (more pods needed)
```
kubectl edit deployment mongodb -n new-namespace
```
```
spec:
	replicas: n
```
exit
### get information on particular deployment in new-namespace
```
kubectl get deployment mongodb -n new-namespace
```
