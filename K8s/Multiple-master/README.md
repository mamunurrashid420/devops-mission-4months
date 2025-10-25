<h2> Kubernetes Multiple Master Node</h2>
In kubernetes cluster the `master node` is the `brain` of the entire cluster

Node components:
- kube-apiserver
- etcd
- kube-scheduler
- kube-controller-manager
- cloud-controller-manager (optional)
- coredns (optional)

## If One master node 
- when its goes down kubectl the schedule and the controller-manager    all stop working
- worker node will keep existing pods but no new pods can be scheduled.
## If three master nodes 
- etcd (Kubernetes’ internal database) maintains quorum.
- If one master node goes down, the remaining two stay active and keep the cluster running.
- This provides fault tolerance — meaning your cluster can survive even if one master node fails.

`When you make a change using kubectl that change gets replicated through the etcd database to all the nodes in the cluster.`

### Why 3 master - not 2 or 5 
Because etcd follows the `quorum` rule.
- quorum = (n/2)+1
- n = number of master nodes
**Meaning**
- 1 master -> quorum =1 -> no fault tolerance
- 2 master -> quorum = 2 -> If one fails quorum is breaks 
- 3 master -> quorum = 2 -> cluster fails works even if one fails 
