##Deployment types
Two deployment startegy
*Recreate => downtime
*RollingUpdate => default stratedy, replacement happens one by one

kubectl rollout status <deploy>
obatain status of particular rollout

How to perform rollback?

```bash
kubectl rollout undo <name-of-deployment>
```

##Config Map Notes:

```bash
kubectl create configmap generic db-secret --from-literal=DB_Host=sql01 --from-literal=DB_User=root --from-literal=DB_Password=password123
```
Referencing in a Pod:

```yaml
env:
- configMapRef:
    name: config-map-name
```

##Secrets:

```bash
kubectl create secret generic db-secret --from-literal=DB_Host=sql01 --from-literal=DB_User=root --from-literal=DB_Password=password123
```
Referencing in a Pod:

```yaml
envFrom:
- secretRef:
    name: config-map-name
```

##Init contaieners
init containers: specialized containers that run before app containers in a Pod. Init containers can contain utilities or setup scripts not present in an app image.

Init containers are exactly like regular containers, except:

- Init containers always run to completion.
- Each init container must complete successfully before the next one starts

todo
review commands and arguments.
