```markdown
# FinalProject — Kubernetes manifests and instructions

This directory contains Kubernetes manifests and step-by-step instructions to deploy your Dockerized web application on a Kubernetes cluster (Docker Desktop). Included manifests:

- namespace.yaml
- configmap.yaml
- secret.yaml
- deployment.yaml (with liveness & readiness probes)
- replicaset.yaml (demo / learning)
- service.yaml (LoadBalancer)
- hpa.yaml (HorizontalPodAutoscaler)
- cronjob.yaml (in-cluster HTTP health checks)

IMPORTANT: Adjust image name, container port, and health path as needed for your app.

## Quick overview of the resources

- Namespace: `finalproject` isolates resources
- Deployment: manages pods (replicas set to 3)
- ReplicaSet: provided as an educational example (Deployments normally manage ReplicaSets automatically)
- Service: `finalproject-svc` (LoadBalancer) exposes the app within the cluster and, on Docker Desktop, typically maps to localhost
- HPA: auto-scales the Deployment between 2 and 10 replicas based on CPU usage
- ConfigMap & Secret: configuration and secrets injected into the pod
- CronJob: periodically curls the service from inside the cluster
- Liveness & Readiness probes: HTTP probes at `/health` to manage traffic and restarts

## Apply manifests (order recommended)

From the folder containing these YAMLs:
kubectl apply -f k8s/namespace.yaml
kubectl apply -f k8s/configmap.yaml
kubectl apply -f k8s/secret.yaml
kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml
kubectl apply -f k8s/hpa.yaml
kubectl apply -f k8s/cronjob.yaml

(Optional) For learning/demo:
kubectl apply -f k8s/replicaset.yaml

## Verify deployment

Get resources:
kubectl get all -n finalproject

Watch pods:
kubectl get pods -n finalproject --watch

Describe a pod or deployment:
kubectl describe deployment finalproject-app -n finalproject
kubectl describe pod <pod-name> -n finalproject

Logs:
kubectl logs deployment/finalproject-app -n finalproject --tail=200

Service access:
- If using LoadBalancer with Docker Desktop, the service is often reachable at localhost (Docker Desktop maps LB to localhost). Use:
  kubectl get svc -n finalproject
- Or port-forward locally:
  kubectl port-forward svc/finalproject-svc -n finalproject 8080:80
  Then open http://localhost:8080/

Check HPA:
kubectl get hpa -n finalproject
kubectl describe hpa finalproject-hpa -n finalproject

Check CronJob executions:
kubectl get cronjob -n finalproject
kubectl get jobs -n finalproject --sort-by=.metadata.creationTimestamp
kubectl logs job/<job-name> -n finalproject
```