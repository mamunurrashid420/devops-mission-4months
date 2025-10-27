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
For example Mysql database

```
apiVersion: apps/v1
kind:StatefullSet
metadata:
  name: mysql 
spec:
 serviceName: "mysql"
 replicas: 2
 selector:
    matchLabels:
        app:
    template:
        metadata:
            labels:
                app: mysql
        spec:
            containers:
            - name: mysql
              image: mysql:5.7
              ports:
              - containerPort: 3306
              env:
              - name: MYSQL_ROOT_PASSWORD
                value: "password"
              - name: MYSQL_DATABASE
                value: "mydatabase"
              volumeMounts:
              - name: mysql-persistent-storage
                mountPath: /var/lib/mysql
    volumeClaimTemplates:
    - metadata:
        name: mysql-persistent-storage
      spec:
        accessModes: [ "ReadWriteOnce" ]
        resources:
          requests:
            storage: 1Gi
```

## Stateless
A Stateless application is an application that does not store any data or state . It does not depend on any privious state.
- Stateless app means   memory less app
- Easy scalable in pods 
- If any pods are died kubernetes will easy create new pods- there is no data loss here 
- light weight and fast