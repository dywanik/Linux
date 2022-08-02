# Cheat sheet for k8s flawless usage

### get all nodes in cluster
```kubectl get nodes```

### describe node and look for errors, constant "starting" and/or check flags
```kubectl describe node [name]```

### show all pods on the machine
```
kubectl get pods --all-namespaces
kubectl get pods -A
```

### show all info on a pod
```kubectl describe pod [name] -n kube-system```

### show logs for a pod
```kubectl logs [name] -n kube-system```

### "restart" a pod - there is NO "kubectl pod restart" - we need to scale it up and then terminate malfunctioning pods
```
kubectl scale deployment [name] --replicas=4 -n kube-system
kubectl scale deployment [name] --replicas=2 -n kube-system
```

### node information
```kubectl get nodes -o wide```

### kubernetes configuration file
```kubectl -n kube-system get cm kubeadm-config -oyaml```

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
```sudo kubeadm reset```

### entering into pod
```kubectl exec -it [podName] -- /bin/bash```

### create pod from yaml
```kubectl apply -f pods01.yaml```

### delete pod
```kubectl delete -f pods01.yaml```