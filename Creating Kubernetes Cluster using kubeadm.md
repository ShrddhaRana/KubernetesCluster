We will be setting up a cluster with one master node and one worker node. We are using Ubuntu 20.04 as the operating system.

**i) Assumptions**
```
      Role	  Machine Name	      IP
      Master	  k8s-master1	      10.164.76.36
      Worker	  k8s-worker3	      10.164.76.38
```
      
**ii) On both master and worker**

1. Login as root user
```
sudo su –
```

**2. Disable Firewall**
```
ufw disable
```

**3. Disable swap**
```
swapoff -a; sed -i '/swap/d' /etc/fstab
```

**4. Update sysctl settings for Kubernetes networking**
```
cat >>/etc/sysctl.d/kubernetes.conf<<EOF
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF
sysctl --system
```

**5. Install docker engine- Here we are using a known compatible docker version**
```
{
  apt install -y apt-transport-https ca-certificates curl gnupg-agent software-properties-common
  curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
  add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
  apt-get update
  apt install docker.io=20.10.12-0ubuntu2~20.04.1
}
```

**iii) Kubernetes Setup**
                                         
**1. Add Apt repository**
```
{
  curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
  echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" > /etc/apt/sources.list.d/kubernetes.list
}
```
      
**2. Install Kubernetes components- Here also a known compatible version**
```
apt update && apt install -y kubeadm=1.24.4-00 kubelet=1.24.4-00 kubectl=1.24.4-00
```
      
**iv) On master**
      
1. Update the below command with the ip address of master
```
kubeadm init --apiserver-advertise-address=10.164.76.36 --pod-network-cidr=192.168.0.0/16  --ignore-preflight-errors=all
```

2. Deploy Calico network- A compatible version is used here
```
kubectl --kubeconfig=/etc/kubernetes/admin.conf create -f https://docs.projectcalico.org/manifests/calico.yaml
```

3. If you want to be able to run kubectl commands as non-root user, then as a non-root user perform these
```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

**v) On worker**
      
1. Join the cluster
Use the output from kubeadm token create command in previous step from the master server and run here.

**vi) Verifying the cluster (On master)**
      
1. Get Nodes status
```
kubectl get nodes
```

2. Get component status
```
kubectl get cs
```
![image](https://user-images.githubusercontent.com/120251092/206851287-77d6ec91-867b-42dc-9c59-7460de415212.png)


