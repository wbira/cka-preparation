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

###High level process
1. Upgrade control plane nodes
  * Upgrade kubeadm tool
    * Verify if version kubeadm is correct
    * Get upgrade plan
  * Drain control plane node
  * Upgrade kubelet on control plane node
  * Uncordone control plane node
2. Upgrade worker nodes
  * Upgrade kubeadm tool
  * Drain the node
  * Upgrade kubelet
  * Uncordon the node

	
Kubeadm tool

Show plan of an upgrade:

```bash
kubeadm upgrade plan
```

```bash
kubeadm upgrade apply
```
##ETCD backup

1. Creating backup:
```bash
etcdctl --endpoints=https://[127.0.0.1]:2379 --cacert=/etc/kubernetes/pki/etcd/ca.crt --cert=/etc/kubernetes/pki/etcd/server.crt --key=/etc/kubernetes/pki/etcd/server.key snapshot save /opt/snapshot-pre-boot.db
```
To get those values run describe pod on etcd in kube-system namespace.

2. Restore backup:
```bash
etcdctl --data-dir /var/lib/etcd-from-backup  snapshot restore /opt/snapshot-pre-boot.db
```

3. Modify /etc/kubernetes/manifests/etcd.yaml

Use new target location:
```bash
--data-dir=/var/lib/etcd-from-backup
```
and update volumes and volumes mounts
