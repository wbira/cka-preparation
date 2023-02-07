# Services

## Service types
1. ClusterIP: Exposes the Service on a cluster-internal IP. Choosing this value makes the Service only reachable from within the cluster. This is the default that is used if you don't explicitly specify a type for a Service. You can expose the service to the public with an Ingress or the Gateway API.
2. NodePort: Exposes the Service on each Node's IP at a static port (the NodePort). To make the node port available, Kubernetes sets up a cluster IP address, the same as if you had requested a Service of type: ClusterIP.
3. LoadBalancer: Exposes the Service externally using a cloud provider's load balancer.

### Node port

```yaml
apiVersion: v1
kind: Service
metadata:
    name: my-service
spec:
    type: NodePort
    ports:
    - targetPort: 80
        port: 80
        nodePort: 30008
    selector:
        app: my-app
```