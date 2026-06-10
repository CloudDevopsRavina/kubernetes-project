Replica Set YAML:::---

This YAML creates a ReplicaSet named web-rs. The ReplicaSet ensures that 3 Pod replicas are always running. It uses the label selector app=webapp to identify and manage Pods. The Pod template defines the labels and container configuration. Each Pod runs an Apache HTTP Server container using the httpd image. If any Pod fails or is deleted, the ReplicaSet automatically creates a new Pod to maintain the desired count of 3 replicas. This provides self-healing and high availability for applications.

Deployment YAML::::-

This Deployment YAML creates a Deployment named nginx-deployment. It maintains one replica of a Pod running the Apache HTTP Server (httpd) container. The Deployment uses the label app=nginx to identify and manage Pods. Internally, the Deployment creates a ReplicaSet, which ensures the desired number of Pods are always running. If a Pod fails, Kubernetes automatically creates a replacement. Deployments also provide advanced features such as rolling updates and rollbacks, making them the preferred way to manage applications in Kubernetes.
