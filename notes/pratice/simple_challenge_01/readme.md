# Kubernetes Practice Challenges

This document contains hands-on exercises for practicing core Kubernetes concepts.

Concepts covered:

* Namespaces
* Pods
* ReplicaSets
* Deployments

Try to solve each challenge using `kubectl` commands or YAML manifests.

---

# Namespace Challenges

### Challenge 1

Create a namespace called `team-a`.

### Challenge 2

Create another namespace called `team-b`.

### Challenge 3

Run an `nginx` pod inside the `team-a` namespace.

### Challenge 4

Run a `redis` pod inside the `team-b` namespace.

### Challenge 5

List all pods running in the `team-a` namespace.

### Challenge 6

List pods across **all namespaces**.

### Challenge 7

Delete the `team-b` namespace.

---

# Pod Challenges

### Challenge 8

Create a pod named `nginx-test` using the `nginx` image.

### Challenge 9

Check the logs of the `nginx-test` pod.

### Challenge 10

Describe the pod and find the following:

* container image
* pod IP address
* node where the pod is running

### Challenge 11

Execute a shell inside the running pod.

### Challenge 12

Delete the `nginx-test` pod.

### Challenge 13

Create a pod from YAML called `alpine-test` using the `alpine` image that runs a command to sleep for `3600` seconds.

---

# ReplicaSet Challenges

### Challenge 14

Create a ReplicaSet that runs **3 nginx pods**.

### Challenge 15

Verify that the ReplicaSet created exactly **3 pods**.

### Challenge 16

Delete one of the pods manually.

Observe what happens.

### Challenge 17

Scale the ReplicaSet to **5 pods**.

### Challenge 18

Scale the ReplicaSet back to **2 pods**.

---

# Deployment Challenges

### Challenge 19

Create a Deployment called `web-app` running **3 nginx pods**.

### Challenge 20

Verify that the Deployment created:

* a ReplicaSet
* multiple Pods

### Challenge 21

Scale the deployment to **6 replicas**.

### Challenge 22

Update the nginx image version in the deployment.

### Challenge 23

Watch the rollout progress of the deployment.

### Challenge 24

Roll back the deployment to the previous version.

---

# Mixed Scenario Challenges

### Challenge 25

Create a namespace called `staging`.

Inside that namespace deploy:

Deployment name: `api-server`
Image: `nginx`
Replicas: `4`

---

### Challenge 26

Delete **one pod** from the deployment.

Observe what happens.

---

### Challenge 27

Scale the deployment to **8 pods**.

---

### Challenge 28

Delete the deployment.

Check whether the pods still exist.

---

# Controller Behavior Challenges

### Challenge 29

Create a pod manually with the label:

app=nginx

Then create a ReplicaSet with the selector:

app=nginx

and set replicas = 3.

Question:

How many pods will Kubernetes create?

---

### Challenge 30

Create a deployment with **3 replicas**.

Then manually delete the ReplicaSet.

Question:

What happens next?

---

# Learning Goal

By completing these exercises you will understand the Kubernetes controller hierarchy:

Deployment
→ ReplicaSet
→ Pods

Controllers continuously watch the cluster state and ensure that the desired state is maintained.

This behavior forms the foundation of many cloud-native systems and ML platforms that run on Kubernetes.


Note: This practice list was initially generated with the help of ChatGPT
and then adapted as part of my personal Kubernetes learning exercises.