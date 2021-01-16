#Scheduling

Manual scheduling:

We could specify nodeName property in POD spec to manual schedule POD on specific node.
Example:
```
apiVersion: v1
kind: Pod
metadata:
	name: nginx
	labels:name: nginx
spec:
	containers:
	- name: nginx
	  image: nginx
	  ports:
    		-containerPort: 8080
	nodeName: node01
```
## Tains and tolerations vs Node Affinity
Node affinity, is a property of Pods that attracts them to a set of nodes (either as a preference or a hard requirement). Taints are the opposite -- they allow a node to repel a set of pods.
Tolerations are applied to pods, and allow (but do not require) the pods to schedule onto nodes with matching taints.
Taints and tolerations work together to ensure that pods are not scheduled onto inappropriate nodes. One or more taints are applied to a node;
this marks that the node should not accept any pods that do not tolerate the taints

Examples:

Setting taint:
```
kubectl taint nodes node1 key1=value1:NoSchedule
```
Remove taint:
```
kubectl taint nodes node1 key1=value1:NoSchedule-
```

Set tolaration (inside POD spec)
```
tolerations:
- key: "key1"
  operator: "Exists"
  effect: "NoSchedule"
```

###Tolerations effects:
NoSchedule => Pod won't be scheduled on node
PreferNoSchedule => soft version of NoSchedule, if there's not other matching node POD might be scheduled
NoExecute => POD will be eviceted from node (if already running) or not scheduled

###Tolerations operator:
Exists (in which case no value should be specified), or
Equal and the values are equal.

##Node Affinity:

todo more about affinity here

Example (part of POD spec)
```
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
          - key: kubernetes.io/e2e-az-name
            operator: In
            values:
            - e2e-az1
            - e2e-az2
      preferredDuringSchedulingIgnoredDuringExecution:
      - weight: 1
        preference:
          matchExpressions:
          - key: another-node-label-key
            operator: In
            values:
            - another-node-label-value
```

## Daemon sets:

Ensuring that specific POD is scheduled on every node in a cluster. 
Use cases:
- monitoring solutions
- log viewer
- networking solutions
Example: kube-proxy is sheduled internally by DaemonSet

It has similar template like ReplicaSet or Deployment

## Static Pods:
Static Pods are managed directly by the kubelet daemon on a specific node, without the API server observing them. Unlike Pods that are managed by the control plane (for example, a Deployment); instead, the kubelet watches each static Pod (and restarts it if it fails).

Static Pods are always bound to one Kubelet on a specific node.	
Usually you need to place POD definition on specific dir that kubelet monitor. Default is /etc/kubernetes/manifest

Here configuration:
https://kubernetes.io/docs/tasks/configure-pod-container/static-pod/

Useful things:

How to find staticPodPath
1. Grep for process kublet to find config file (ps -rf | grep kubelet)
2. Grep given file by static (grep -i static /pathToConfig

##Multiple scheduler:

How deploy aditional scheduler reusing kubeadm approach?
1. Find kube-scheduler manifest file (/etc/kubernetes/manifests/
2. --leader-elect param should be false
3. Run Pod

To schedule pod with custom scheduler we need set up schedulerName prop on POD spec

