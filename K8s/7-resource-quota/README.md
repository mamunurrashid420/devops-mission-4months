<h2>Resource Quota</h2>
Resource quota is a namespace level limit system in kubernetes that defines. How much cpu,memory, storage,or how many objects(like Pods, Services, PVCs) a particular namespace can use.

**summary**
ResourceQuota is used to make sure that a single team or application doesn’t consume all the resources of the entire cluster.

## Resource Quota Object

**To control resource sharing:**
When multiple teams or projects share the same cluster, quotas help allocate a specific amount of resources to each one.