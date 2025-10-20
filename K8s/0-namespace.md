<h2>Namespace</h2>

**Table of Contents**

- [Namespace](#namespace)
  - [What is Namespace?](#what-is-namespace)
  - [Why we need Namespace?](#why-we-need-namespace)
  - [Namespaces organize resources logically](#namespaces-organize-resources-logically)
  - [Benefits of Namespaces in Kubernetes:](#benefits-of-namespaces-in-kubernetes)
  - [How to create Namespace?](#how-to-create-namespace)
  - [How to list Namespace?](#how-to-list-namespace)
  - [How to delete Namespace?](#how-to-delete-namespace)

## What is Namespace?

Namespaces are a way to organize clusters into virtual sub-clusters — they can be helpful when different teams or projects share a Kubernetes cluster. Any number of namespaces are supported within a cluster, each logically separated from others but with the ability to communicate with each other. Namespaces cannot be nested within each other.
Names of resources need to be unique within a namespace, but not across namespaces. Namespace isolate different workloads or environments within the same physical cluster.

## Why we need Namespace?

Kubernetes namespaces solve organizational, security, and resource management problems in multi-user or complex environments.

## Namespaces organize resources logically
```
dev/frontend
prod/frontend
dev/backend
prod/backend
```
### Benefits of Namespaces in Kubernetes:
- **Resource Isolation**: keeps workloads separated to avoid interference
- **Access Control**: Uses RBAC to manage who can access what within each namespace.
- **Resource Quotas**: Can limit CPU, memory, storage, etc. per namespace to ensure fair usage.
- **Simplified Management**: Separate  dev,staging, and production environment for safer, organized deployments.

## How to create Namespace?
```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
  name: team-a-quota
  namespace: dev
spec:
  hard:
    pods: "10"
    requests.cpu: "1"
    requests.memory: 1Gi
    limits.cpu: "2"
    limits.memory: 2Gi
```
## Namespace and Network
- by default, pods in different namespaces can communicate with each other within the same Kubernetes cluster, unless you explicitly block it using a NetworkPolicy.

```bash
kubectl create namespace <namespace-name>
```
**Or**
```yaml
apiVersion:v1
kind: namespace
metadata:
  name: <namespace-name>
```

## How to list Namespace?

```bash
kubectl get namespaces
```

## How to delete Namespace?

```bash
kubectl delete namespace <namespace-name>
```
How many pods exits in dev-ns?
```bash
kubectl get pods -n dev-ns
```
How to switch namespace?
```bash
kubectl config set-context --current --namespace=dev-ns
```
Create Deployment with dev-ns
```bash
kubectl create deployment nginx --image=nginx -n dev-ns
```
List all pods in all namespaces
```bash
kubectl get pods --all-namespaces
```