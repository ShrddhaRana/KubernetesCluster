Using k3s- https://k3s.io/

**i) Assumptions**
```
      Role	  Machine Name	      IP
      Master	  k8s-master1	      10.164.76.36
      Worker	  k8s-worker3	      10.164.76.38
```

1)Install k3s on both master and worker
```
curl -sfL https://get.k3s.io | sh -
```

2) Add worker to our cluster:
```
curl -sfL https://get.k3s.io | K3S_NODE_NAME=k8s-worker3 K3S_URL=https://<IP>:6443 K3S_TOKEN=<TOKEN> sh -
```
K3S_NODE_NAME= will be the worker node name
K3S_URL=https://<IP>:6443 <IP of the master node>
K3S_TOKEN = token from master
