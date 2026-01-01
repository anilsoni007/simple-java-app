# Java App Helm Chart

Helm chart for deploying simple Java Spring Boot application.

## Installation Options

### 1. ClusterIP (Default - Internal Only)
```bash
helm install java-app ./java-app
```

### 2. NodePort (Direct Access via Node)
```bash
helm install java-app ./java-app \
  --set service.type=NodePort \
  --set service.nodePort=30080
```
Access: `http://<node-ip>:30080`

### 3. LoadBalancer (Cloud Provider)
```bash
helm install java-app ./java-app \
  --set service.type=LoadBalancer
```
Access: Use external IP from `kubectl get svc`

### 4. Ingress (ALB/Nginx)
```bash
helm install java-app ./java-app \
  --set ingress.enabled=true \
  --set ingress.host=myapp.example.com
```
Access: `http://myapp.example.com`

## Common Commands

```bash
# Upgrade
helm upgrade java-app ./java-app

# Uninstall
helm uninstall java-app

# Custom values file
helm install java-app ./java-app -f custom-values.yaml
```

## Key Values

| Parameter | Default | Description |
|-----------|---------|-------------|
| `replicaCount` | `1` | Number of replicas |
| `image.repository` | `asoni007/simple-java-webapp` | Image repository |
| `image.tag` | `latest` | Image tag |
| `service.type` | `ClusterIP` | Service type (ClusterIP/NodePort/LoadBalancer) |
| `service.port` | `8080` | Service port |
| `service.nodePort` | `null` | NodePort (30000-32767) |
| `ingress.enabled` | `false` | Enable ingress |
| `ingress.host` | `""` | Ingress hostname |
