<h2> Persistent Volume</h2>
<p> Kubernetes persistent volume and persistent volume clain are important concepted used for storage management in kubernetes. with their help you can create use and manage dynamic or static storage for containers</p>

**Table of contents**


## What is the persistent volume(PV)
Persistent volume is part  of the cluster that is used for long term storage. It is not directly associated     with pods but rather storage is provided to pods when needed. PV are created and used cluster-wide.

**Key point about PV:**
- `Cluster-wide`: PV are cluster-wide resource that pods can provided access to.
- `Lifecycle`: PV have lifecycle independent of my pods. PV remains as persistent storage and is independent of the pods lifecycle.
- `Typs of Volume`: There can be various type of PVs, such as AWS EBS,GCE Persistent disk , NFS,iSCSI, etc.