Reference document- https://github.com/kubernetes/dashboard/blob/master/docs/user/access-control/creating-sample-user.md

**i) Creating a Service Account**
Create and apply a “AdminUser.yaml” file with the following contents.
```
apiVersion: v1
kind: ServiceAccount
metadata:
  name: admin-user
  namespace: kubernetes-dashboard
```
**ii) Creating a ClusterRoleBinding**
Create and apply a “ClusterRoleBinding.yaml” file with the following contents.
```
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: admin-user
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
- kind: ServiceAccount
  name: admin-user
  namespace: kubernetes-dashboard
```
**iii) Getting a Bearer Token**
```
kubectl -n kubernetes-dashboard create token admin-user
```
Now copy the token and paste it into the Enter token field on the login screen.
![image](https://user-images.githubusercontent.com/120251092/206851816-9cedccd7-19df-4e04-b107-2e4afe66222b.png)
 
Click the Sign in button. You are now logged in as an admin.

![image](https://user-images.githubusercontent.com/120251092/206851821-5a0974e4-0af6-474d-8020-aa75354e050d.png)
 
Run command **iii** to create new tokens whenever session expires.
