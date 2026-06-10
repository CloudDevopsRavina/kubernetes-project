Replica Set YAML:::---

This YAML creates a ReplicaSet named web-rs. The ReplicaSet ensures that 3 Pod replicas are always running. It uses the label selector app=webapp to identify and manage Pods. The Pod template defines the labels and container configuration. Each Pod runs an Apache HTTP Server container using the httpd image. If any Pod fails or is deleted, the ReplicaSet automatically creates a new Pod to maintain the desired count of 3 replicas. This provides self-healing and high availability for applications.
