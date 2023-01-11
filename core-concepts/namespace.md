## Namespace are multiple virtual cluster inside physical cluster.
1. Isolation of resources
2. Posibility of setting Resource quota. (number of pods, cpu, memory)

### Kubernetes starts with four initial namespaces:
1. default
	 The default namespace for objects with no other namespace
2. kube-system
	The namespace for objects created by the Kubernetes system
3. kube-public
	This namespace is created automatically and is readable by all users (including those not authenticated).
 	This namespace is mostly reserved for cluster usage, in case that some resources should be visible and readable publicly throughout the whole cluster. The public aspect of this namespace is only a convention, not a requirement.
4. kube-node-lease
	This namespace for the lease objects associated with each node which improves the performance of the node heartbeats as the cluster scales

## DNS

When you create a Service, it creates a corresponding DNS entry.
This entry is of the form 

**service-name**.**namespace-name**.svc.cluster.local,

which means that if a container just uses **service-name** it will resolve to the service which is local to a namespace.
There is also possible connectivity between namespaces by using full form of DNS entry

