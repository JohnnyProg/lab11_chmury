```markdown
# Task

This repository contains Kubernetes manifests for deploying a MySQL database using a StatefulSet. The example includes scaling up and down.

## Files

- `mysql-service.yaml`: Definition of the **mysql-headless** service for DNS addressing of Pods.
- `mysql-statefulset.yaml`: StatefulSet configuration for MySQL with persistent data storage.
- `mysql-secret.yaml`: Encoded MySQL credentials.

## Prerequisites

1. Kubernetes cluster (Minikube or a cloud-based cluster).
2. `kubectl` tool installed and configured.

## Deployment Steps

1. **Apply manifests:**

   ```bash
   kubectl apply -f mysql-service.yaml
   kubectl apply -f mysql-secret.yaml
   kubectl apply -f mysql-statefulset.yaml
   ```

2. **Verify StatefulSet and Pods:**

   ```bash
   kubectl get statefulset
   kubectl get pods
   ```

   ![alt text](image-2.png)

3. **Check Persistent Volumes:**

   ```bash
   kubectl get pvc
   ```

   ![alt text](image-1.png)

## Scaling the StatefulSet

### Scaling Up

Increase the number of replicas:

```bash
kubectl scale statefulset mysql --replicas=5
```

Verify the new Pods:

```bash
kubectl get pods
```

![alt text](image-3.png)

Check data replication and the initialization order of the Pods.  New pods will be initialized sequentially, with increasing ordinal indexes.

### Scaling Down

Decrease the number of replicas:

```bash
kubectl scale statefulset mysql --replicas=2
```

```bash
kubectl get pods
```

![alt text](image-4.png)

Ensure that Pods are terminated in reverse order (highest index first).  This is important for data consistency and to avoid potential data loss.
```

This revised version provides a single, copyable Markdown block and clarifies some aspects of the scaling process.  It also explicitly shows how to apply the YAML files separately, which is generally best practice.

