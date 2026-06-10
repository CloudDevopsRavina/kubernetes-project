Deployment and Service communicate indirectly through labels and selectors. The Deployment creates Pods and assigns labels such as app=my-app. The Service uses a selector with the same label to discover those Pods. Kubernetes automatically creates endpoints for the matching Pods. When traffic reaches the Service, kube-proxy forwards it to one of the Pod endpoints. The Deployment controller continuously ensures the desired number of Pods are running, while the Service automatically updates its endpoint list whenever Pods are added or removed. This provides self-healing and load balancing without manual intervention.

what is kube rpoxy here
What is kube-proxy?

kube-proxy is a Kubernetes networking component that runs on every worker node.

Its main job is to route traffic from a Service to the correct Pod(s).

Why Do We Need kube-proxy?

Suppose you have:

Service (my-app-svc)
       │
       ▼
Pod-1   Pod-2   Pod-3

A Service has a virtual IP (ClusterIP), but Services are not actual processes that receive traffic.

When a request comes to the Service IP:

10.96.0.10:80

something must decide:

Which Pod should receive the request?
How should the packet be forwarded?

That's the job of kube-proxy.

Traffic Flow
Client Pod
    │
    ▼
Service (ClusterIP)
    │
    ▼
kube-proxy
    │
    ▼
Pod-1 / Pod-2 / Pod-3

Example:

Request 1 → Pod-1
Request 2 → Pod-2
Request 3 → Pod-3

This provides load balancing across Pods.

Where Does kube-proxy Run?
Worker Node 1
 ├── kubelet
 ├── kube-proxy
 └── Pods

Worker Node 2
 ├── kubelet
 ├── kube-proxy
 └── Pods

Every worker node has its own kube-proxy.

How Does It Work?

kube-proxy watches the Kubernetes API Server.

When a Service is created:

kind: Service
metadata:
  name: my-app-svc

kube-proxy learns:

Service IP
Service port
Backend Pod IPs

Then it configures Linux networking rules (typically iptables or IPVS) so traffic to the Service is forwarded to the Pods.

Example

Service:

ClusterIP = 10.96.0.10

Pods:

10.244.1.10
10.244.1.11
10.244.1.12

Request:

curl http://10.96.0.10

kube-proxy forwards it to one of:

10.244.1.10
10.244.1.11
10.244.1.12
Interview Answer

kube-proxy is a networking component that runs on every Kubernetes worker node. It watches Services and Endpoints through the API Server and configures networking rules using iptables or IPVS. When traffic reaches a Service, kube-proxy forwards the request to one of the backend Pods and provides load balancing. It enables communication between Services and Pods inside the Kubernetes cluster.
