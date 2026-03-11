KubeMastery Labs ☸️

Hands-on Kubernetes practice repository — workloads, networking, storage, scaling, and configuration management implemented from scratch.


What This Is
A personal lab for building real familiarity with Kubernetes. Each directory targets a specific concept — not just reading docs, but writing manifests, applying them to a live cluster, and debugging until things actually work.
Built and tested on Minikube and Docker Desktop.

Concepts Covered
AreaWhat's ImplementedWorkloadsDeployments, Pods, ReplicaSets with liveness/readiness health checksNetworkingClusterIP, NodePort, LoadBalancer services — internal and external traffic routingIngressIngress controller setup with separate routing rules for frontend and backendConfigurationConfigMaps and Secrets to decouple config from container imagesStoragePersistentVolumes (PV) and PersistentVolumeClaims (PVC) for stateful workloadsAutoscalingHorizontal Pod Autoscaler (HPA) based on CPU utilization with resource limitsInit ContainersDatabase initialization via init containers before main app starts

Repository Structure
.
├── deployments/       # Application workload manifests (Deployments, Pods)
├── services/          # Networking configs — ClusterIP, NodePort, LoadBalancer, Ingress
├── config-maps/       # ConfigMaps and Secrets for environment config
├── storage/           # PV and PVC manifests for persistent storage
├── scaling/           # HPA configs and resource limit definitions
├── scripts/           # Helper scripts for minikube/kubectl setup
└── README.md

Getting Started
Prerequisites: A running local cluster — Minikube, Docker Desktop, or K3s.
bash# Clone the repo
git clone https://github.com/heyrohhh/KubeMastery-Labs.git
cd KubeMastery-Labs

# Apply workloads
kubectl apply -f deployments/
kubectl apply -f services/

# Verify everything is running
kubectl get all
For HPA to work, ensure the metrics-server is enabled:
bash# Minikube
minikube addons enable metrics-server

Key Learnings
Networking — Understanding the difference between ClusterIP (internal only), NodePort (external via node IP), and LoadBalancer (cloud-provisioned) took real debugging to internalize. Ingress on top of that adds another layer of routing logic worth understanding separately.
Stateful vs Stateless — Stateless Deployments are straightforward. Stateful workloads need PV/PVC correctly bound, and init containers for setup ordering. Getting the init container sequence right was a useful exercise.
HPA behaviour — HPA doesn't scale instantly. There's a stabilisation window. Testing this properly meant generating actual CPU load and watching kubectl get hpa update in real time.
Secrets management — Kubernetes Secrets are base64 encoded, not encrypted. In production they'd be backed by something like AWS Secrets Manager or Vault. This repo uses them for local practice only.

Related Projects
If you want to see these concepts applied at scale in a cloud environment:
→ microservices_demo — 18-service microservices platform migrated from GCP Kubernetes to AWS ECS Fargate, with Terraform infrastructure, GitHub Actions CI/CD, and Prometheus/Grafana monitoring.

Author
Rohit Neel Mishra — LinkedIn
Aspiring DevOps / Cloud / SRE Engineer
