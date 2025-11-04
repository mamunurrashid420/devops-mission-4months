<h2 align="center">Kubernetes Auto Scale</h2>
Autoscaling in Kubernetes refers to the automatic adjustment of resources in response to changes in workload demand. Kubernetes provides several mechanisms for autoscaling:

- Including Horizontal Pod Autoscaling (HPA)
- Vertical Pod Autoscaler (VPA)
- Cluster Autoscaler

## Horizontal Pod Autoscaling (HPA)

we will work through following steps by steps 
1. create a k8s cluster
2. Install the metrics server
3. Deploy a sample application
4. Apply Horizantal Pod Autoscaling (HPA)
5. Increase Load to the Application
6. Monitor Events

Steps 1. Create a k8s cluster
If you don;t already have a kubernetes cluster please follow the instructions provided in the Reference to setup one efficiency.

Steps 2. Install the metrics server
```
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml

```
First, get the name of the Metric Server pod.
`kubectl get pods -n kube-system | grep metrics-server`

If you want to see the top pods based on CPU.
`kubectl top pods --sort-by cpu -A`
And to see the top pods based on memory usage.
`kubectl top pods --sort-by memory`

## Deploy a sample application
```yaml 
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx
        resources:
          limits:
            cpu: "200m" # Set CPU resource limit
          requests:
            cpu: "100m" # Set CPU resource request
```
Create the kubernetes service for nginx 
```yaml 
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: LoadBalancer
  ```
## apply HPA 
```
apiVersion: autoscaling/v1
kind: HorizontalPodAutoscaler
metadata:
  name: nginx-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: nginx-deployment
  minReplicas: 2
  maxReplicas: 10
  targetCPUUtilizationPercentage: 30
  ```

  If you want to configure imperative 
  ```
  kubectl autoscale deployment nginx-deployment --cpu-percent=30 --min=2 --max=10
  ```
  ## Increase Load to the Application
  ```
  kubectl run -i --tty load-generator --image=busybox /bin/sh
  ```
  ```
  while true; do wget -q -O- http://nginx-service; done
  ```
  ## Monitor Events
  ```


    

