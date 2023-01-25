# Replicaset

Main purpose is to make sure that we're running desired number of pods

### Example definition
```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: nginx-rc
  labels:
    app: myapp
spec:
  replicas: 2
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      name: nginx
      labels:
        app: myapp
    spec:
      containers:
      - image: nginx
        name: nginx
```


### Commands

Scale
```
kubectl scale -replicase=3 -f <file>
```