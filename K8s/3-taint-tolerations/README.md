<h2>Kubernetes Taints and Tolerations </h2>
Taint and tolerations are very important scheduling concepts in kubernetes, which determines which pods will or will not run on which nodes.

**Table of contents:**

    - [What is the taints](#what-is-the-taints)

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
Toleration =  permissionn not a guarantee
- It lets the pod be eligible for that tainted node but it won't force placement there. if you want to actually land there, and labels  + nodeAffinity 






## Why use them?
1. `Dedicated Nodes:` Keep certain nodes for specific workloads—like monitoring, databases, or GPUs. Example: only AI/ML Pods run on GPU nodes
2. `Sensitive Resource Protection:`Use taints to protect critical nodes so regular workloads can’t land there by mistake
3. `Node Isolation:` In mixed environments (prod/dev/test), taints prevent dev/test Pods from scheduling onto production nodes
4. `High-Priority Scheduling:` Ensure only select, important Pods can run on specific nodes by combining node taints with Pod tolerations
## Dicision tree
- `Taint + Toleration`: Normal pods won't be go to this node, only specific ones.
- `Node affinity and anti-affinity`:` Its better to go to that node but its okay if you don't.