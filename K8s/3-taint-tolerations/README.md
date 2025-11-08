<h2>Kubernetes Taints and Tolerations </h2>
Taint and tolerations are very important scheduling concepts in kubernetes, which determines which pods will or will not run on which nodes.

**Table of contents:**

  - [What is the taints](#what-is-the-taints)
  - [Tolerations](#tolerations)
  - [Why are using taints and tolerations?](#why-are-using-taints-and-tolerations)
- [Decision tree](#decision-tree)

## Why are using taints and tolerations?

## What is the taints
A tiant is a kind of `constraint` or `restriction` that we place on a Node. 
Meaning- we say that only certain pods will run on this node and not others.
`Purpose:`
- To prevent the pods from accidentally moving to sensitive or dedicated nodes.

### Taint effects

 - NoSchedule: New non-tolerant Pods won’t schedule.
- PreferNoSchedule: Soft avoid.
- NoExecute: Blocks new Pods and evicts existing non-tolerant Pods.

**For node**
```yaml
# taint add
kubectl taint nodes node1 key=value:NoSechedule

# taint remove
kubectl taint nodes node1 key=value:NoSechedule-
```
- `key=value` - taint label
- `NoSchedule` - taint effect 

**Pod yaml file for toleration**
```yaml 
apiVersion: v1
kind: Pod 
metadata:
    name: prod-api
spec: 
    tolerations:
    - key: "env"
      operator: "Equal"
      value: "prod"
      effect: "NoSchedule"
    containers:
    - name: prod-api
      image: nginx
```

## Tolerations
`Toleration` =  permissionn not a guarantee
- It lets the pod be eligible for that tainted node but it won't force placement there. if you want to actually land there, and labels  + nodeAffinity 






## Why use them?
1. `Dedicated Nodes:` Keep certain nodes for specific workloads—like monitoring, databases, or GPUs. Example: only AI/ML Pods run on GPU nodes
2. `Sensitive Resource Protection:`Use taints to protect critical nodes so regular workloads can’t land there by mistake
3. `Node Isolation:` In mixed environments (prod/dev/test), taints prevent dev/test Pods from scheduling onto production nodes
4. `High-Priority Scheduling:` Ensure only select, important Pods can run on specific nodes by combining node taints with Pod tolerations
## Dicision tree
- `Taint + Toleration`: Normal pods won't be go to this node, only specific ones.
- `Node affinity and anti-affinity`:` Its better to go to that node but its okay if you don't.

## Affinity and anti-affinity
Affinity and Anti-Affinity are Kubernetes scheduling rules that control where pods should (or should not) be placed based on node labels or other pods already running in the cluster.
## Node Selector
`kubectl get node k8-worker1 --show-labels `

`kubectl label nodes k8-worker1 environment=production`



### 1. Node Affinity
Node affinity defines which nodes a pod can be scheduled on based on labels assigned to nodes.
```yaml 

spec:
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
          - key: node-type
            operator: In
            values:
            - high-memory
```
- This pod will be only run on nodes labeld with `node-type: high-memory`

### 2. Pod affinity
Pod affinity defines the rules that allow a pod to be scheduled near another pod.same node or zone
```yaml 
spec:
  affinity:
    podAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
      - labelSelector:
          matchExpressions:
          - key: app
            operator: In
            values:
            - frontend
        topologyKey: "kubernetes.io/hostname"
```
### 3. Pod anti-affinity
Pod Anti-Affinity ensures Pods are not placed together on the same node
```yaml 
spec:
  affinity:
    podAntiAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
      - labelSelector:
          matchExpressions:
          - key: app
            operator: In
            values:
            - frontend
        topologyKey: "kubernetes.io/hostname"
```
- ensures no two Pods with `app=frontend` run on the same node.