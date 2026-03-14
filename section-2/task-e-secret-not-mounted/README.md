# Task E – Secret Not Mounted as ENV

## Goal
Discover why the environment variable is missing at runtime and fix the namespace or resource mismatch.

## Notes
This task will contain:
- Secret troubleshooting steps,
- namespace/resource validation,
- safe debugging approach,
- corrected manifest notes.

This task is about debugging why a Kubernetes Secret is not available to the application as an environment variable.

## Problem
The application expects the environment variable `DB_PASSWORD` from a Kubernetes Secret.
The deployment uses:
```yaml
env:
  - name: DB_PASSWORD
    valueFrom:
      secretKeyRef:
        name: db-secret
        key: password
```
And the Secret is defined as:
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: db-secret
type: Opaque
data:
  password: c2VjcmV0cGFzcw==
```

The issue described in the task is that `DB_PASSWORD` is missing at runtime.


---Root cause---
The most likely root cause is that the application and the Secret are not available in the same namespace, or the Secret has not been created in the namespace where the Pod is running.
In Kubernetes, a Pod can only reference a Secret from the same namespace.
So even if `db-secret` exists, the environment variable will still be missing if:
the Secret is in a different namespace,
the Deployment is in a different namespace,
or the Secret was not created at all.
Another possible issue is a mismatch in:
Secret name,
key name,
or the resource was applied in the wrong order.

How I would debug it safely
The task explicitly says to debug it without printing the secret in logs, so I would only verify metadata and resource existence.
1. Check which namespace the Pod is running in
```bash
kubectl get pods -A
kubectl get deployment -A
```
2. Check whether the Secret exists in the same namespace
Example:
```bash
kubectl get secret -n <namespace>
kubectl describe secret db-secret -n <namespace>
```
This confirms whether the Secret exists and whether the key is present, without printing the decoded secret value.
3. Check the Deployment manifest
```bash
kubectl get deployment <deployment-name> -n <namespace> -o yaml
```
Verify that:
`secretKeyRef.name` is `db-secret`
`secretKeyRef.key` is `password`
4. Check Pod events
```bash
kubectl describe pod <pod-name> -n <namespace>
```
If the Secret is missing, Kubernetes usually shows an event similar to:
secret not found
couldn't find key in Secret
error generating container environment
5. Verify the environment variable without exposing the value
Instead of printing the secret, check whether the variable exists:
```bash
kubectl exec -it <pod-name> -n <namespace> -- /bin/sh
printenv | grep DB_PASSWORD
```
This confirms whether the variable is present, but the secret value itself should not be copied into logs, screenshots, or documentation.
---
Fix
---
The correct fix is to make sure that:
the Deployment and Secret are in the same namespace,
the Secret name matches `db-secret`,
the key matches `password`,
the Secret is created before the Pod starts.
Example fixed Secret
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: db-secret
  namespace: app
type: Opaque
data:
  password: c2VjcmV0cGFzcw==
```
Example fixed Deployment
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: demo-app
  namespace: app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: demo-app
  template:
    metadata:
      labels:
        app: demo-app
    spec:
      containers:
        - name: demo-app
          image: nginx:alpine
          env:
            - name: DB_PASSWORD
              valueFrom:
                secretKeyRef:
                  name: db-secret
                  key: password
```
---
Why this works
---
Kubernetes resolves `secretKeyRef` only inside the same namespace as the Pod.
After placing both resources in the same namespace and making sure the Secret name and key are correct:
the Pod can read the Secret,
`DB_PASSWORD` is injected into the container environment,
and the application can access it at runtime.

---Prevention---
To avoid this problem in production, I would use these practices:
1. Always define namespaces explicitly
Do not rely on the default namespace by accident.
2. Keep related resources together
Deployment, Secret, ConfigMap, and Service should be applied into the same intended namespace.
3. Validate manifests before applying
Use:
```bash
kubectl apply --dry-run=client -f .
kubectl diff -f .
```
4. Check resource references
Double-check:
Secret name
key name
namespace
deployment order
5. Avoid exposing secrets in logs
Never print decoded secret values to logs, screenshots, or README output.
---
Final answer
`DB_PASSWORD` is missing at runtime because the Pod cannot resolve the referenced Secret correctly.
The most likely reason is a namespace mismatch or a missing Secret resource.
The fix is to ensure that:
the Secret exists,
the Secret name is `db-secret`,
the key is `password`,
and both the Secret and Deployment are in the same namespace.
This allows Kubernetes to inject `DB_PASSWORD` into the container environment safely.
