# Useful commands

## Create pod:
```bash
kubectl run nginx --image=nginx
```
## Generate pod template:
```bash
kubectl run nginx --image=nginx  --dry-run=client -o yaml
```

## Create Deployment:
```bash
kubectl create deployment --image=nginx nginx --replicas=n
```

## Generate deployment template:
```bash
kubectl create deployment --image=nginx nginx --dry-run -o yaml  > nginx-deployment.yaml
```

## Service commands:
```bash
kubectl expose pod redis --port=6379 --name redis-service --dry-run=client -o yaml

kubectl create service clusterip redis --tcp=6379:6379 --dry-run=client -o yaml
```


