<h2 align="center">Statefull & Stateless</h2>

## What is statefull ?
A statefull set is a kubernetes controler used to manage statefull applications
- Each Pod has its own identity, data (storage), and order.
Statefull-set
- Each pod is created with a unique name
- Each pod has its own Persistent Volume
- Pods are created and deleted in a specific order
## Why we use it?
**Need to stable storage**
Each pod in a statefull set get its own persistent  volume claim. so even if a pod is deleted its data remains safe.
- database lossing data is not acceptable
