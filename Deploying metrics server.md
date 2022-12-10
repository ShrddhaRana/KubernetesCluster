Reference document- https://github.com/kubernetes-sigs/metrics-server

Metrics Server is a scalable, efficient source of container resource metrics for Kubernetes built-in autoscaling pipelines.
You can use Metrics Server for:
•	CPU/Memory based horizontal autoscaling
•	Automatically adjusting/suggesting resources needed by containers

i) Download the Metrics Server release from the components.yaml manifest on master
```
wget https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```
ii) Edit the yaml by inserting
```
        - --kubelet-insecure-tls
``` 
![image](https://user-images.githubusercontent.com/120251092/206851878-35d49932-b6dd-4569-9ea0-53a074528a75.png)

iii) Apply the yaml
```
kubectl apply -f components.yaml
```

You will be able to view the CPU and memory usage in the dashboard.
![image](https://user-images.githubusercontent.com/120251092/206851882-16272bc5-6b70-422f-be11-afad9cb4db0b.png)


Run kubectl top pods to get similar status through ssh
![image](https://user-images.githubusercontent.com/120251092/206851888-1b236b32-07a5-464b-b3ac-04e26abea25e.png)

	
