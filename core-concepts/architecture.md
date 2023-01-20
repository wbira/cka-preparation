CLUSTER ARCHITERCUTE (COMPONENTS):


0. ETCD:
storage for all data in a cluster. Stores info about
(nodes, PODs, configs, secrets, accounts, roles, bidings and other)
Lives in kube-system namespace (with kubeadm setup)


Access ectd:

kubectl exec etcd-master -n kube-system ecrdctl get / --prefix -keys-only
 
1. Kube-API server:
Primary managment component in k8s. Responsible for:
- Auth User
- Validate Request
- Retrieve data
- Update information in ETCD storage
- Interact with scheduler and kublet when providing new resources in a cluster

2. Kube controller manager:
Process that continously monitor state of various components in a system and try to keep whole system in a desired state.
Example:

Node controller:
Monitor nodes in a cluster in 5s period. When node is down for 40s, node controller move podes to different nodes to keep HA

3. Kube scheduler:

Main responsibility is deciding where pods should be located. So it's filter nodes that satisfy POD requirements and then ranks them.

4. Kubelet:
Is placed on the node. Main tasks:
- Register node in master
- Create PODs and containers
- Monitor Node & PODs
- Report about current status of Node/PODs 

5. Kube Proxy
Internal virual network that gives connectivity between all PODs in a cluster. 
Kube proxy is a process that lives in each node in a cluster. It's looking for a new services, 
and creates appropiate rules on each node  to forward traffic to those services using e.g IP Tables rules on each node

