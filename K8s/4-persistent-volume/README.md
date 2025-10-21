<h2> Persistent Volume</h2>
<p> Kubernetes persistent volume and persistent volume clain are important concepted used for storage management in kubernetes. with their help you can create use and manage dynamic or static storage for containers</p>

**Table of contents**


## What is the persistent volume(PV)
Persistent volume is part  of the cluster that is used for long term storage. It is not directly associated     with pods but rather storage is provided to pods when needed. PV are created and used cluster-wide.

**Key point about PV:**
- `Cluster-wide`: PV are cluster-wide resource that pods can provided access to.
- `Lifecycle`: PV have lifecycle independent of my pods. PV remains as persistent storage and is independent of the pods lifecycle.
- `Typs of Volume`: There can be various type of PVs, such as AWS EBS,GCE Persistent disk , NFS,iSCSI, etc.

## Persistent volume claim(PVC)
<p> A persistent volume claim is a request that comes from pods or workloads, specifying the required storage capacity and other requirements. PVC is binding request that gets asscoiated with a persistent volume (pv)</p>

Key point of PVC:
- `User Request`: A PVC is a storage request from the user (or Pod). It essentially says, "I need some storage that meets these conditions."

- `Binding`: Kubernetes finds an available PV for a PVC and binds them together. Once bound, the PVC and PV stay associated with each other until the PVC is fulfilled.


## PV and PVC Relationship
- Persistent volume is a actual storage in the cluster
- Persistent volume claim is a request sent by the pod to use that storage.