```bash
kubectl describe pod nginx-test
```

# Kubernetes Pod Networking — Quick Guide

This guide explains how networking works for Pods in Kubernetes and how Pod IPs are assigned and used inside a cluster.

---

# 1. Pod Networking Basics

In Kubernetes, **each Pod receives its own IP address**.
Containers inside the same Pod share the **same network namespace**, meaning they share:

* the same IP address
* the same network interface
* the same port space

Example:

Pod
├── Container A
└── Container B

Both containers communicate using **localhost** because they share the same network stack.

---

# 2. Pod IP Address

When a Pod is created, Kubernetes assigns it an IP address from the **cluster network range**.

Example output:

kubectl get pods -o wide

Result:

NAME           READY   STATUS    IP           NODE
nginx-team-a   1/1     Running   10.244.0.7   worker-node

Here:

* `10.244.0.7` → Pod IP address
* `worker-node` → Node where the Pod is running

The Pod IP can also be found using:

kubectl describe pod <pod-name>

or

kubectl get pod <pod-name> -o yaml

Look for:

status:
podIP: 10.244.0.7

---

# 3. How Pod IPs Are Assigned

Pod IPs are assigned by the **Container Network Interface (CNI) plugin**.

Common CNI plugins include:

* Flannel
* Calico
* Cilium
* Weave

Process:

Pod scheduled to node
→ kubelet requests network setup
→ CNI plugin allocates an IP address
→ virtual network interface is created
→ Pod receives its IP

---

# 4. Pod-to-Pod Communication

One of Kubernetes’ key networking rules:

**Every Pod can communicate with every other Pod using its IP address.**

Example:

Pod A → curl 10.244.0.7 → Pod B

This works **across nodes**, meaning Pods do not need NAT or port forwarding to communicate inside the cluster.

Example cluster layout:

Cluster
│
├── Node1
│   ├── Pod A (10.244.0.5)
│   └── Pod B (10.244.0.7)
│
└── Node2
└── Pod C (10.244.1.3)

All Pods can communicate directly.

---

# 5. Pod IPs Are Temporary

Pod IP addresses are **ephemeral**.

If a Pod is deleted or restarted:

Old Pod → destroyed
New Pod → created
New IP → assigned

Example:

Old Pod → 10.244.0.7
New Pod → 10.244.1.2

Because of this, applications should **not depend on Pod IP addresses directly**.

---

# 6. Services Provide Stable Access

To solve the changing Pod IP problem, Kubernetes uses **Services**.

A Service provides:

* a stable virtual IP
* load balancing across Pods
* stable DNS name

Example flow:

Client → Service → Pod A / Pod B / Pod C

This allows applications to reach Pods reliably even when Pods restart.

---

# 7. Useful Commands for Inspecting Pod Networking

View Pod IP addresses:

kubectl get pods -o wide

Describe a Pod:

kubectl describe pod <pod-name>

View full Pod networking details:

kubectl get pod <pod-name> -o yaml

Test communication between Pods:

kubectl exec -it <pod-name> -- curl <pod-ip>

---

# 8. Key Networking Concepts

Pod networking in Kubernetes follows three important rules:

1. Every Pod has its own IP address.
2. Pods can communicate directly with other Pods across nodes.
3. Pod IPs are temporary; Services provide stable networking.

---

# 9. Why Pod Networking Matters

Pod networking is essential for distributed applications running in Kubernetes.

Examples include:

* microservices communication
* service meshes
* machine learning training clusters
* inference services
* distributed systems such as Ray or Spark

Understanding Pod networking helps diagnose communication issues and design scalable applications in Kubernetes.
