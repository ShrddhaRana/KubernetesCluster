We will be hosting a simple ‘nginx’ service to check if the cluster created is working properly or not.
Reference document- https://kubernetes.io/docs/tasks/run-application/run-stateless-application-deployment/ 

i) Create a Deployment based on the YAML file
 kubectl apply -f https://k8s.io/examples/application/deployment.yaml

ii) Display information about the Deployment:
 kubectl describe deployment nginx-deployment

iii) Expose the deployment to be accessed from browser.
 kubectl expose deployment nginx-deployment --type=NodePort --port=80
 

iv) View the port where nginx is hosted
 kubectl get svc
 
v) To access the service use the IP address of master with the port
  10.164.76.36:32151
 
vi) Delete deployment
  kubectl delete deployment nginx-deployment
