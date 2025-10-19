<h2>Deployment</h2>

 **Table of Contents**
- [ What is a Deployment](#what-is-a-deployment)  
- [Key Purposes of a Deployment](#key-purposes-of-a-deployment)  
- [Creating a Deployment](#creating-a-deployment)  
- [Creating deployment file in imperative way](#Creating-deployment-file-in-imperative-way)  
- [Update nginx deployment file](#update-nginx-deployment-file)  
- [Rolling Back a Deployment](#rollback-to-the-previous-version)

    


### What is a Deployment
A Deployment in Kubernetes is a resource that manages a set of identical Pods and ensures that the desired number of Pod replicas are running at any given time. It is one of the most fundamental and powerful controllers in Kubernetes, allowing you to manage the lifecycle, scaling, and updates of your applications

### Key Purposes of a Deployment
1. `Scalability`:
    A Deployment helps you scale your application by adjusting the number of Pod replicas. You can easily scale up (increase replicas) or scale down (decrease replicas) based on traffic or load.
2. `Rollbacks`:
    Deployments allow you to roll back to a previous version of the application in case the new version causes issues. Kubernetes stores the history of changes, so you can quickly revert to an earlier, stable version.
3. `Self-Healing`:
    If a Pod managed by a Deployment fails or is deleted, Kubernetes automatically creates a new one to maintain the desired number of replicas, ensuring high availability.
4. `Declarative Updates`:
    With Deployments, you can declaratively update your application. Kubernetes will automatically handle the rolling update process, replacing old Pods with new ones in a controlled manner, ensuring that there is no downtime.

## Creating a Deployment
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-container
        image: nginx:1.14.2
```
## Creating deployment file in imperative way
```bash
kubectl create deployment nginx-deployment --image=nginx:1.4.2 --replicas=3 --dry-run=client -o yaml > nginx-deployment.yaml
```
## Update nginx  deployment file
- Update  nginx pods to use the nginx:1.16.1 image instead of nginx:1.4.2
```bash
kubectl set image deployment/nginx-deployment nginx=nginx:1.16.1
```
- Alternative you can edit in deployment file
```bash
kubectl edit deployment/nginx-deployment
```
- If you want to see the rollout status,
```bash
kubectl rollout status deployment/nginx-deployment
```
### Rollback a deployment
- suppose that you  made a type while updating the deployment by putting the image name as nginx:1.161 instead of nginx:1.16.1
```
kubectl set image deployment/nginx-deployment nginx=nginx:1.161
```
- The rollout get stuck . you can verify it by checking the rollout status 
```bash
kubectl rollout status deployment/nginx-deployment
```
- Describe the deployment to see the error
```bash
kubectl describe deployment/nginx-deployment
```
## rollback to the previous version
- Now you have decided to undo the current rollback to rollback to  the previous version
```bash
kubectl rollout undo deployment/nginx-deployment
```
- Alternative you can rollback to a specific version
```bash 
kubectl rollout undo deployment/nginx-deployment --to-revision=2
```
- check the rollback was successful
```bash
kubectl get deployment

```
### Delete a deployment
```bash
kubectl delete deployment/nginx-deployment
```

### Scaling a Deployment
- You can scale a Deployment by using following   command
```bash
kubectl scale deployment/nginx-deployment --replicas=5
```
- You can also scale a Deployment by editing the deployment file
```bash
kubectl edit deployment/nginx-deployment
```
- You can also scale a Deployment by using the following command
```bash
kubectl scale deployment/nginx-deployment --replicas=5
```
- Assuming horizontal pod autoscaling is enabled in your cluster
```bash
kubectl autoscale deployment/nginx-deployment --min=10 --max=15 --cpu-percent=80
```

### Deployment Strategy
A deployment strategy in kubernetes defines `how updates or new versions of an application rolled out`- specifically, how old pods are replaced  with new pods during an update. 
It determines whether the applications will experience downtime   and how fast or safely the new version will be deployed 
## Many types of kubernetes Deployment strategies

#### Recreate strategy
- All existing Pods are killed before new ones are created .
```bash 
strategy:
  type: Recreate
```
- `Uses case`: When old and new versions cannot run together (e.g., database migration)
## Rolling Update Deployment
- The default strategy in kubernetes . Old pods are gradually replaced with new pods.
  -  `Zero downtime` - users experience no interruption 
  - Old and new versions run side by side for a short time.
```bash

strategy:
  type: RollingUpdate 
  rollingUpdate: 
    maxUnavailable: 1
    maxSurge: 1
```
- `maxUnavailable:1`- At most 1 pod can be unavailable during the update.
- `maxSurge:1 ` - At most 1 extra pod can be created above the desired count.
## `Uses case`:
 `Best for production environments` - ideal when update is critical (e.g., web applications)

## Rolling Update Strategy YAML
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-deployment
spec:
  replicas: 3
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxUnavailable: 1
      maxSurge: 1
    template:
      metadata: 
        labels: 
          app: myapp
      spec:
        containers:
        - name: myapp-container
          image: myapp:v2
          ports:
          - containerPort: 8080

```
A Deployment Strategy defines how Kubernetes replaces old Pods with new ones.
Choosing the right strategy ensures smooth updates, zero downtime, and safe rollbacks for your applications.

##  Blue-Green Deployment
You run two environments — one current (Blue) and one new (Green).
Once the new version (Green) is ready and tested, you switch traffic from Blue to Green.

### Process:

- Blue environment is live (old version).

- Green environment is deployed with the new version.

- Test the Green environment.

- Switch traffic from Blue → Green.

- Delete the old Blue environment after validation.
### Canary Deployment
Roll out the new version gradually to a small subset of users first. If everything looks good, extend it to all users.
`Use Case:`
  - When testing new features or changes with minimal risk.