<h2>Pods in Kubernetes</h2>


- [Pods in Kubernetes](#pods-in-kubernetes)
  - [What is a Pod?](#what-is-a-pod)
  - [Key Points about Pods](#key-points-about-pods)
  - [Creating a Pod](#creating-a-pod)
  - [Accessing a Pod](#accessing-a-pod)
  - [Deleting a Pod](#deleting-a-pod)
  - [Pods and Services](#pods-and-services)

## What is a Pod?
In Kubernetes, a Pod is the smallest and simplest deployable unit. It represents a single instance of a running process in your cluster. A Pod can contain one or more tightly coupled containers that share the same network, storage, and namespace. Pods are ephemeral resources — they can be terminated and recreated on other nodes as needed.
## Key Points about Pods
**Atomic Unit:** A Pod encapsulates one or more application containers, storage resources, a unique network IP, and configuration options. It's the basic building block of Kubernetes applications.

**Containers:** Pods can contain one or more containers, which are managed as a single entity within the Pod. These containers share the same network namespace, allowing them to communicate with each other using localhost.

**Networking:** Each Pod in Kubernetes is assigned a unique IP address, which allows communication between Pods and external clients or other Pods within the same cluster.

**Storage**: Pods can define volumes that are mounted into their containers, allowing them to share data between containers or persist data beyond the lifetime of the Pod.

**Lifecycle**: Pods have a lifecycle managed by the Kubernetes control plane. They can be created, updated, and terminated based on deployment configurations, scaling requirements, or failures.

**Atomicity and Scalability**: Pods are atomic units that can be replicated and scaled horizontally. You can create multiple replicas of a Pod to handle increased load or ensure high availability.

<p align="center">
<img src="./image/pod.png" alt="Pods in Kubernetes" width="500" height="300" /> 
<br/>
Pic: Pods in Kubernetes
</p>
