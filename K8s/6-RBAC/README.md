<h2 align="center"> RBAC Authorization</h2>
Role based access control is a method of regulating access to computer or network on the roles of individual users within your organization.

- `who` (users, service, or team)
- `why` resource (pods, service, secrets, configmaps, etc)
- `how` works(read,write,delete,update)
- RBAC is a kubernets `permission system`  - it defines who can do what.

## why we use RBAC

- For security 
    - Instead of giving everyone full access to the entire cluster, you can grant limited permissions  based on specific tasks.
- For team-based control
    - When multiple teams work on the same cluster - like dev,Ops, and QA . Each team can have its own role with the right level of access.
- To prevent accident damange.
    - You can stop users from accidentally deleting production resource.

**Componets of RBAC**
- Role
- RoleBinding
- ClusterRole
- ClusterRoleBinding

`Create in Role`
```yaml 
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: pod-reader
  namespace: dev
rules:
- apiGroups: [""] # "" indicates the core API group
  resources: ["pods"]
  verbs: ["get", "watch", "list"]
```

**RoleBinding**
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: read-pods
  namespace: dev
subjects:
- kind: User
  name: mamun
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io
```
**ClusterRole**
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: pod-reader
rules:
- apiGroups: [""] # "" indicates the core API group
  resources: ["pods"]
  verbs: ["get", "watch", "list"]
```
**ClusterRoleBinding**
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: read-pods
subjects:
- kind: User
  name: mamun
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: ClusterRole
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io
```

### To create a Role and RoleBinding imperatively in Kubernetes


```bash
kubectl create role pod-reader --verb=get,list,watch --resource=pods --namespace=default
kubectl create rolebinding pod-reader-binding --role=pod-reader --user=bob --namespace=default
kubectl -n default get pod server --as bob
kubectl -n default delete pod server --as bob
```
## To create a ClusterRole and Cluster RoleBinding imperatively in Kubernetes
```bash
kubectl create clusterrole pod-reader --verb=get,list,watch --resource=pods
kubectl create clusterrolebinding bob-admin-binding --clusterrole=pod-reader --user=bob
kubectl run nginx --image nginx --as bob
```

```
kubectl create clusterrole dev-cluster-role --verb=get,list,watch,create --resource=pods
kubectl create clusterrolebinding dev-admin-binding --clusterrole=dev-cluster-role --user=mamun
kubectl run server --image nginx -n default --as mamun
kubectl -n default delete pod server --as mamun
```
