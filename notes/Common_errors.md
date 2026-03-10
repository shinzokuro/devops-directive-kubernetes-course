# Kubernetes Practice Notes — Common Errors Encountered

While completing the Kubernetes practice challenges, the following errors occurred.
This document explains why they happened and how they were resolved.

---

# Error 1 — CreateContainerConfigError

## Symptom

Running:

kubectl get pods -n team-a

Result:

NAME           READY   STATUS                       RESTARTS   AGE
nginx-team-a   0/1     CreateContainerConfigError   0          27s

## Cause

The container was configured with:

securityContext:
runAsNonRoot: true

However, the nginx image runs as the **root user by default**.

When Kubernetes sees `runAsNonRoot: true`, it checks the container image user.
If the container tries to run as UID `0` (root), Kubernetes refuses to start the container.

This results in the Pod status:

CreateContainerConfigError

## How to Debug

kubectl describe pod nginx-team-a -n team-a

Look at the **Events** section. It typically shows a message similar to:

container has runAsNonRoot and image will run as root

## Solution

Option 1 — Remove the security context (simplest for learning)

Remove:

securityContext:
runAsNonRoot: true

Option 2 — Run the container with a non-root user

Example:

securityContext:
runAsUser: 101
runAsNonRoot: true

---

# Error 2 — Pod Spec Is Immutable

## Symptom

After modifying the YAML and applying again:

kubectl apply -f challenge3.yml

Error:

The Pod "nginx-team-a" is invalid: spec: Forbidden: pod updates may not change fields other than
spec.containers[*].image ...

## Cause

Pods are mostly **immutable after creation**.

Kubernetes allows only a small set of fields to be updated in an existing Pod, mainly:

* container image
* activeDeadlineSeconds
* some toleration additions

Fields such as:

* securityContext
* volumes
* container structure
* namespace

cannot be modified once the Pod exists.

In this case, the `securityContext` field was changed, which is not allowed.

## Solution

Delete the existing Pod and recreate it.

kubectl delete pod nginx-team-a -n team-a
kubectl apply -f challenge3.yml

Alternatively:

kubectl replace --force -f

# Error 3 — Kubernetes Error Note — `kubectl exec` Syntax

## Symptom

Tried to run:

kubectl exec -it nginx-team-a -n team-a --curl 10.244.2.10

This command failed.

## Cause

`kubectl exec` requires a space after `--`.
Everything after `--` is treated as the command that runs inside the container.

In the incorrect command, `--curl` was interpreted incorrectly.

## Solution

kubectl exec -it nginx-team-a -n team-a -- curl 10.244.2.10

## Explanation

kubectl exec → run a command inside a container
-it → interactive terminal
nginx-team-a → pod name
-n team-a → namespace
-- → separates kubectl arguments from the command inside the container

## Note

The command will only work if the container image has `curl` installed.
