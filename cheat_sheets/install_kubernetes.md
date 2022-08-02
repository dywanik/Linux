# Cheat sheet for installing Kubernetes on Ubuntu (after Docker is installed)
### Add repository and install newest versions (sometimes you might want to specify a version)

```
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -

cat << EOF | sudo tee /etc/apt/sources.list.d/kubernetes.list
deb https://apt.kubernetes.io/ kubernetes-xenial main
EOF

sudo apt-get update
sudo apt-get install -y kubeadm kubelet kubectl kubernetes-cni
```

### Verify
```
kubeadm version
```

### Bootstrapping 
#### On master
```
sudo kubeadm init --pod-network-cidr=10.244.0.0/16

mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

### Verify
```
kubectl version
```

#### On nodes
```
sudo kubeadm join [someIP] --token [someToken] --discovery-token-ca-cert-hash sha256:[someHash]
```

### Network configuration (using Flannel)
#### On all nodes
```
echo "net.bridge.bridge-nf-call-iptables=1" | sudo tee -a /etc/sysctl.conf 
sudo sysctl -p
```

#### On master Install flannel
```
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
```

### Verify (all machines should be Ready)
```
kubectl get nodes
```

#### For legacy versions use these URLs (+RBAC)
```
https://raw.githubusercontent.com/coreos/flannel/master/Documentation/k8s-manifests/kube-flannel-legacy.yml
https://raw.githubusercontent.com/coreos/flannel/master/Documentation/k8s-manifests/kube-flannel-rbac.yml
```