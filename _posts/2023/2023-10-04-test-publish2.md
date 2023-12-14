---
title: "How to install Kyverno using helm"
categories:
  - Kubernetes
tags:
  - Kyverno
---




## What is Kyverno 
Kyverno is a policy engine designed for Kubernetes. It allows users to validate, mutate, and generate Kubernetes resources as well as manage policies as Kubernetes objects. This makes it easy to manage policies across different clusters and environments. Kyverno policies are written in YAML, making them easy to read and write.

## How to Install

1. **Add the Kyverno Helm repository**:
   ```shell
   helm repo add kyverno https://kyverno.github.io/kyverno/
   ```

2. **Update your local Helm chart repository cache**:
   ```shell
   helm repo update
   ```

3. **Install Kyverno using Helm**. You can provide your custom values in a `values.yaml` file or override them on the command line:
   ```shell
   helm install kyverno kyverno/kyverno --namespace kyverno --create-namespace -f values.yaml
   ```

### Values for Helm Chart

When installing Kyverno via Helm, you can customize its installation by modifying the values in the Helm chart. Here are some common values you might want to configure:

1. **Replica Count**: Number of Kyverno replicas for high availability.
   ```yaml
   replicaCount: 3
   ```

2. **Resource Limits and Requests**: Define CPU and memory for the Kyverno pod.
   ```yaml
   resources:
     limits:
       cpu: "100m"
       memory: "512Mi"
     requests:
       cpu: "50m"
       memory: "256Mi"
   ```

3. **Image Configuration**: Specify the Kyverno image and tag.
   ```yaml
   image:
     repository: ghcr.io/kyverno/kyverno
     pullPolicy: IfNotPresent
     tag: "latest"
   ```

4. **Service Type and Port**: Configure the service type and port.
   ```yaml
   service:
     type: ClusterIP
     port: 443
   ```

5. **Custom Configurations**: Any additional configurations like log level, custom labels, annotations, etc.
   ```yaml
   config:
     logLevel: "info"
   ```

6. **Node Selector, Affinity, and Tolerations**: To control where Kyverno pods are scheduled.
   ```yaml
   nodeSelector: {}
   affinity: {}
   tolerations: []
   ```

7. **Security Context**: Define the security context for the Kyverno pod.
   ```yaml
   securityContext:
     runAsNonRoot: true
     runAsUser: 1001
   ```
