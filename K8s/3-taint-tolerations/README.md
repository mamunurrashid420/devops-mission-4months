<h2>Kubernetes Taints and Tolerations </h2>
Taint and tolerations are very important scheduling concepts in kubernetes, which determines which pods will or will not run on which nodes.

**Table of contents:**

    - [What is the taints](#what-is-the-taints)

## What is the taints
A tiant is a kind of `constraint` or `restriction` that we place on a Node. 
Meaning- we say that only certain pods will run on this node and not others.
`Purpose:`
- To prevent the pods from accidentally moving to sensitive or dedicated nodes.

### Taint effects

    - NoSchedule: New non-tolerant Pods won’t schedule.
    - PreferNoSchedule: Soft avoid.
    - NoExecute: Blocks new Pods and evicts existing non-tolerant Pods.