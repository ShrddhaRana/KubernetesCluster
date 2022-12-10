We will be hosting a simple ‘nginx’ service to check if the cluster created is working properly or not.
Reference document- https://kubernetes.io/docs/tasks/run-application/run-stateless-application-deployment/ 

i) Create a Deployment based on the YAML file
 kubectl apply -f https://k8s.io/examples/application/deployment.yaml

ii) Display information about the Deployment:
 kubectl describe deployment nginx-deployment

iii) Expose the deployment to be accessed from browser.
 kubectl expose deployment nginx-deployment --type=NodePort --port=80
 ![image](https://user-images.githubusercontent.com/120251092/206851225-dbef73ef-d783-4e2a-9e47-4842f32d7fb9.png)


iv) View the port where nginx is hosted
 kubectl get svc
 ![image](https://user-images.githubusercontent.com/120251092/206851235-a9a44f99-0bac-4d9b-aa85-03d85f218d90.png)

 
v) To access the service use the IP address of master with the port
  10.164.76.36:32151
  ![image](https://user-images.githubusercontent.com/120251092/206851245-1471c58f-1b19-46b1-ac3c-9f18990fdf73.png)

 
vi) Delete deployment
  kubectl delete deployment nginx-deployment
