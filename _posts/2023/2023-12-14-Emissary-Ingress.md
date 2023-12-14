---
title: "Setting Up Emissary-Ingress in Your Kubernetes Cluster: A Fun and Easy Guide"
categories:
  - Kubernetes
tags:
  - Emissary-Ingress
  - Ingress
---


### Setting Up Emissary-Ingress in Your Kubernetes Cluster: A Fun and Easy Guide!

Hey there, Kubernetes adventurers! 🌟 Are you ready to embark on a journey to set up Emissary-Ingress in your Kubernetes cluster? Emissary-Ingress (formerly known as Ambassador) is an open-source Kubernetes-native API Gateway and Ingress Controller. It's all about making routing and managing traffic in your Kubernetes cluster a breeze. Let's dive right in and get your Emissary-Ingress up and running!

#### Why Emissary-Ingress?

But first, why Emissary-Ingress? If you're looking to manage traffic flow into your cluster, apply security policies, or simply need an easy way to expose your services to the outside world, Emissary-Ingress is your go-to. It's built on Envoy Proxy, ensuring high performance and reliability.

#### Prerequisites: What You'll Need

- A Kubernetes cluster, of course! You could be using Minikube, kind, a cloud-based Kubernetes service like GKE, AKS, or EKS, or any other type of cluster.
- `kubectl` command-line tool, connected to your cluster.
- Helm 3, for easy and efficient deployment.

#### Step 1: Add the Emissary-Ingress Helm Repository

First up, let's add the Emissary-Ingress Helm chart repository. This is like telling your package manager where to find the goodies. Run this in your terminal:

```shell
helm repo add emissary-ingress https://app.getambassador.io
helm repo update
```

#### Step 2: Install Emissary-Ingress with Helm

Now, let's get Emissary-Ingress installed. You can customize the installation to your heart's content, but for now, let's keep it simple:

```shell
helm install emissary-ingress emissary-ingress/emissary-ingress --namespace emissary --create-namespace
```

This command installs Emissary-Ingress into its own namespace, keeping things nice and tidy.

#### Step 3: Verify Your Installation

Patience is a virtue, but who likes to wait? Let's check if Emissary-Ingress is happily running:

```shell
kubectl get pods -n emissary
```

All systems go? Great! Let's move to the fun part.

#### Step 4: Configure Your First Mapping

Emissary-Ingress routes traffic based on mappings. Let's create a simple one. Imagine you have a service named `my-awesome-service` running on port `8080`.

Create a file named `my-service-mapping.yaml`:

```yaml
apiVersion: getambassador.io/v3alpha1
kind: Mapping
metadata:
  name: my-service-mapping
  namespace: emissary
spec:
  prefix: /my-service/
  service: my-awesome-service:8080
```

This Mapping tells Emissary-Ingress to route all traffic that comes to `/my-service/` to your `my-awesome-service`.

Apply it:

```shell
kubectl apply -f my-service-mapping.yaml
```

#### Step 5: Access Your Service

Depending on your environment, the way you access your service might differ. If you're using Minikube, for instance, you can run:

```shell
minikube service emissary-ingress -n emissary
```

For other environments, you might set up a LoadBalancer or NodePort to expose Emissary-Ingress.

#### And... You're All Set!

There you have it! You've successfully set up Emissary-Ingress in your Kubernetes cluster. Now, you're all set to route, manage, and secure traffic like a pro.

#### Bonus Tip: Keep Exploring!

Emissary-Ingress is packed with features. From setting up canary releases, adding authentication, rate limiting, to enabling TLS – there's a lot more you can do. Dive into the [Emissary-Ingress documentation](https://www.getambassador.io/docs/emissary/) to explore all its capabilities.

#### Wrapping Up

Congratulations on adding a powerful tool to your Kubernetes toolkit! Emissary-Ingress not only simplifies traffic management but also opens up a world of possibilities for scaling and securing your applications. Happy coding, and here's to smooth sailing through the seas of Kubernetes! 🚢🌊

Got questions or cool stories about your Emissary-Ingress experience? Feel free to share in the comments below! 🎉💬
