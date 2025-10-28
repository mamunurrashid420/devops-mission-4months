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

