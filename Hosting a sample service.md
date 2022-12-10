We will be hosting a simple ‘nginx’ service to check if the cluster created is working properly or not.
Reference document- https://kubernetes.io/docs/tasks/run-application/run-stateless-application-deployment/ 

i) Create a Deployment based on the YAML file
```
kubectl apply -f https://k8s.io/examples/application/deployment.yaml
```

ii) Display information about the Deployment:
``` 
kubectl describe deployment nginx-deployment
```

iii) Expose the deployment to be accessed from browser.
```
kubectl expose deployment nginx-deployment --type=NodePort --port=80
``` 
![image](https://user-images.githubusercontent.com/120251092/206851616-72d79eb8-f3d4-4f6b-a21f-ec47784c3fd9.png)


iv) View the port where nginx is hosted
``` 
kubectl get svc
``` 
![image](https://user-images.githubusercontent.com/120251092/206851607-fb6fd892-7253-4b1c-a572-9736a15de450.png)


v) To access the service use the IP address of master with the port
```
10.164.76.36:32151
``` 
![image](https://user-images.githubusercontent.com/120251092/206851600-1786455f-8eac-4c33-ad90-f5b55b88280b.png)


vi) Delete deployment
```
kubectl delete deployment nginx-deployment
```
