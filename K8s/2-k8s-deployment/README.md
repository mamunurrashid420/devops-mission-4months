<h2>Deployment</h2>

**Table of Contents**
    - [What is a Deployment](# what-is-a-deployment)
    - [Key Purposes of a Deployment](#key-purposes-of-a-deployment)
    - [Creating a Deployment](#creating-a-deployment)
    - [Updating a Deployment](#updating-a-deployment)
    - [Scaling a Deployment](#scaling-a-deployment)
    - [Rolling Back a Deployment](#rolling-back-a-deployment)
    - [Deleting a Deployment](#deleting-a-deployment)


### What is a Deployment
A Deployment in Kubernetes is a resource that manages a set of identical Pods and ensures that the desired number of Pod replicas are running at any given time. It is one of the most fundamental and powerful controllers in Kubernetes, allowing you to manage the lifecycle, scaling, and updates of your applications

### Key Purposes of a Deployment
1. `Scalability`:
    A Deployment helps you scale your application by adjusting the number of Pod replicas. You can easily scale up (increase replicas) or scale down (decrease replicas) based on traffic or load.
2. Rollbacks:
    Deployments allow you to roll back to a previous version of the application in case the new version causes issues. Kubernetes stores the history of changes, so you can quickly revert to an earlier, stable version.
3. Self-Healing:
    If a Pod managed by a Deployment fails or is deleted, Kubernetes automatically creates a new one to maintain the desired number of replicas, ensuring high availability.
4. Declarative Updates:
    With Deployments, you can declaratively update your application. Kubernetes will automatically handle the rolling update process, replacing old Pods with new ones in a controlled manner, ensuring that there is no downtime.

### Creating a Deployment
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
## Update nginx  deployment file\
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
- To rollback to the previous version
```bash
kubectl rollout undo deployment/nginx-deployment
```
### Delete a deployment
```bash
kubectl delete deployment/nginx-deployment
```