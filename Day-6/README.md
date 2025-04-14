
# Day 6 - Kubernetes : Namespaces, ReplicaSets, Deployments, Services, and Monitoring

## Namespace

Dividing cluster into isolated environments

### Basic Commands

```bash
sudo su
kubectl get nodes
kubectl get namespace
kubectl get all -n kube-system
```

### Default Namespaces

- **default**: Created automatically by Kubernetes for user-defined resources.
- **kube-node-lease**: Used by Kubernetes master node to check the health of nodes using lease objects.
- **kube-public**: Resources in this namespace can be accessed by anyone.
- **kube-system**: Contains default services/resources like metrics-server, CNI, CoreDNS created at cluster setup time.

> ❗ When deploying a production application on the server, **never deploy in the default namespace**.

### Creating and Using a Custom Namespace

```bash
kubectl create ns ranjana-ns
kubectl get ns
kubectl get pods
kubectl run test-pod --image=nginx --port=80 -n ranjana-ns
kubectl get pods -n ranjana-ns
kubectl delete pods test-pod -n ranjana-ns
```

## Pod Failure Scenarios and Solutions

| Problem                                  | Solution                                |
|------------------------------------------|------------------------------------------|
| Application downtime                     | Attach **controllers** to pod            |
| Changing IP on pod restart               | Use **Kubernetes services** for static URLs |
| Data loss on pod termination             | Use **Volumes** in Kubernetes            |

---

## ReplicaSet

- A Kubernetes object that ensures a specified number of pod replicas are running at all times.
- Maintains: **Desired State = Actual State**.

### Commands

```bash
kubectl apply -f rs.yaml
kubectl get pods -n ranjana-ns
kubectl get ns -n ranjana-ns
kubectl get pods -n ranjana-ns
kubectl get nodes
```

### Limitations of ReplicaSet

- Cannot perform **rolling updates** or **rollbacks**.
- Not suitable for production usage.

---

## Deployment

- Used for deploying applications in Kubernetes.
- Deployment → manages ReplicaSet → manages Pods.

```bash
kubectl apply -f deployment.yaml
kubectl get rs -n ranjana-ns
```

---

## Services in Kubernetes

To expose your applications, Kubernetes provides 3 main types of services:

| Service Type     | Description                              |
|------------------|------------------------------------------|
| ClusterIP        | Internal access within the cluster       |
| NodePort         | Exposes service on a static port         |
| LoadBalancer     | Exposes service externally (cloud-native)|

> We commonly implement **LoadBalancer** service in real-world applications.

---

## Monitoring in Kubernetes

### Why Monitoring?

- Gain insights into application internals
- Detect issues in pods, nodes, and cluster health
- Identify CPU/memory consumption

### Tools Used

| Tool        | Role                                                                 |
|-------------|----------------------------------------------------------------------|
| Prometheus  | Time-series database (TSDB); collects metrics                        |
| Grafana     | Visualization tool; shows metrics via dashboards, pie charts, graphs |

> Prometheus sends collected data to Grafana for visualization.

### Install Helm

```bash
snap install helm --classic
```

---
