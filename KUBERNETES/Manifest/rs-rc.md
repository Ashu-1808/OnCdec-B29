## Diff between rc and rs 
**ReplicationController:**
- support only equality based selector

**ReplicaSet:**
- support equality based as well as set based selector

### ReplicationController

````
vim rc.yaml
````
````
apiVersion: v1 
kind: ReplicationController 
metadata: 
  name: rc-yoga 

spec: 
  replicas: 3 #3identical pods
  selector: 
    app: yoga 

  template: 
   metadata: 
     name: tmp-1
     labels: 
       app: yoga
   spec: 
    containers:
     - name: c1 
       image: abhipraydh96/yoga 
       ports:
       - containerPort: 80

--- 

apiVersion: v1 
kind: Service 
metadata: 
  name: svc-yoga
spec: 
 selector: 
   app: yoga
 ports:
   - protocol: "TCP"
     port: 80 
     targetPort: 80 
 type: NodePort   
````
````
kubectl apply -f rc.yaml
````
````
kubect get rc
kubectl get pods
````
````
kubectl delete pod <pod-name>
````
---
### ReplicaSet

````
vim rs.yaml
````
````
apiVersion: apps/v1 
kind: ReplicaSet
metadata: 
  name: rs-coffee

spec: 
  replicas: 2 
  selector: 
   matchLabels:
     app: coffee

  template: 
    metadata:
      name: tmp-coffee 
      labels:
        app: coffee
    spec: 
     containers:
      - name: c2 
        image: abhipraydh96/coffee 
        ports:
        - containerPort: 80
---
apiVersion: v1 
kind: Service 
metadata:
  name: svc-cofee
spec:
  selector:
    app: coffee
  ports:
   - protocol: "TCP"
     port: 80
     targetPort: 80
  type: NodePort
````
````
kubectl apply -f rs.yaml
````
````
kubect get rs
kubectl get pods
````
````
kubectl delete pod <pod-name>
````
