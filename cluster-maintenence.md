#Cluster maintenece

##OS Upgrades

Useful commands

* Recreate pods in other nodes and mark node as none scheduleable
```bash
kubectl drain <node01>
```
* Mark node as schedulable
```bash
kubectl cordon <node01>
```
* Mark node as unschedulable
```bash
kubectl uncordon <node01>
```

##K8s upgrade

Kubeadm tool

Show plan of an upgrade:

```bash
kubeadm upgrade plan
```
