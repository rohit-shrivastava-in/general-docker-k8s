
# Kubernetes Cluster Management Guide

## Check Node Status

To check the status of the nodes:
```bash
kubectl get nodes
```

For more detailed information about the nodes:
```bash
kubectl get nodes -o wide
```

---

## Master Machine Components

View all the master machine components:
```bash
kubectl get pod -A
```

Check the status of the kubelet service:
```bash
systemctl status kubelet
```

---

## Check Running Containers (Using CRI-O)

Docker is not used, so to check the running containers, use CRI-O:
```bash
crictl ps
```

To list all available images:
```bash
crictl images
```

---

## Generate Join Command for Worker Node

On the master machine, generate the join command:
```bash
kubeadm token create --print-join-command
```

Take the output of the above command and paste it into the worker node terminal.

---

## Verify Node Status Again

After adding the worker node, verify the nodes:
```bash
kubectl get nodes
kubectl get nodes -o wide
```

---

## Master Node Authentication Configuration

Check the authentication configuration for the master node:
```bash
cd /root/.kube/
ls
cat config
```

This guide helps in managing Kubernetes clusters, checking node statuses, managing containers using CRI-O, and setting up worker nodes.
