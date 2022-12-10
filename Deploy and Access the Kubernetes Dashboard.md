Reference document- https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/
Make the Web UI accessible to Internal NI by changing the services from Cluster to NodePort, reference materials:(1854) kubernetes dashboard - YouTube

Deploying the Dashboard UI

The Dashboard UI is not deployed by default. To deploy it, run the following commands:

i) On master
```
wget https://raw.githubusercontent.com/kubernetes/dashboard/v2.6.1/aio/deploy/recommended.yaml
```
Note: If the yaml is not available I have provided it in this repo, copy fromt there

ii) Edit the yaml file for making it accessible to NI internal

vi recommended.yaml

iii) Add following line
```
type: NodePort
``` 
![image](https://user-images.githubusercontent.com/120251092/206851674-0f858448-95ea-4bfa-93be-88956fc8546e.png)

iv) Apply the yaml
```
kubectl apply -f recommended.yaml
```
v) Access the WebUI through browser
Master IP with port, you will get the below view (10.164.76.36: 30910) To get the port run the following
```
kubectl -n kubernetes-dashboard describe service kubernetes-dashboard
```
![image](https://user-images.githubusercontent.com/120251092/206851668-95a070b6-5cc2-429f-b899-f45358fd253d.png)

