---
title: "How to set all Pods in the cluster have resource limits using Kyverno"
categories:
  - Kubernetes
tags:
  - Kyverno
---


### What is Kyverno 
Kyverno is a policy engine designed for Kubernetes. It allows users to validate, mutate, and generate Kubernetes resources as well as manage policies as Kubernetes objects. This makes it easy to manage policies across different clusters and environments. Kyverno policies are written in YAML, making them easy to read and write.

Key features of Kyverno include:

1. **Validation**: Ensuring data integrity by checking resource configurations against policies and preventing the creation of resources that violate these policies.

2. **Mutation**: Automatically modifying resource configurations when they are created or updated. This can include setting default values or transforming existing configurations.

3. **Generation**: Creating additional Kubernetes resources based on the existing ones. For example, generating network policies, role bindings, or other resources in response to triggers defined in policies.

4. **Policy Management**: Policies in Kyverno are Kubernetes resources themselves, so they can be managed using the same tools and processes used for managing other Kubernetes resources.

5. **Extensive Coverage**: Kyverno policies can be applied to almost all Kubernetes resources, providing a broad range of control over the environment.


Here is how you can ensures that all Pods in the cluster have resource limits (CPU and memory) using Kyverno policy. This is a common best practice to avoid resource overconsumption by a single pod.

```yaml
apiVersion: kyverno.io/v1
kind: ClusterPolicy
metadata:
  name: require-resources-limits
spec:
  validationFailureAction: enforce
  rules:
  - name: validate-resources
    match:
      resources:
        kinds:
          - Pod
    validate:
      message: "CPU and memory resource limits are required."
      pattern:
        spec:
          containers:
          - name: "*"
            resources:
              limits:
                memory: "?*"
                cpu: "?*"
```

This policy will block the creation of any Pod that does not have CPU and memory limits defined. Thanks for reading this article.

