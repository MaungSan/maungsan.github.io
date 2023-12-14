---
title: "How to install Kyverno using helm"
categories:
  - Kubernetes
tags:
  - Kyverno
---


### Installing Kyverno on Kubernetes with Helm: A Step-by-Step Guide
Hey Kubernetes enthusiasts! Today, we're diving into how to install Kyverno, a powerful policy engine for Kubernetes, using Helm, the go-to package manager for Kubernetes applications. Whether you're a DevOps pro or just starting out with Kubernetes, follow these steps to get Kyverno up and running on your cluster.

#### Why Kyverno?

Before we jump in, let's talk a bit about why Kyverno is a game-changer. Kyverno simplifies Kubernetes policy management by allowing you to validate, mutate, and generate Kubernetes resources with ease. It's all about making policy management as Kubernetes-native as possible. With Kyverno, you can ensure your cluster adheres to your organization's requirements without breaking a sweat.

#### Pre-requisites

- **Kubernetes Cluster**: You need access to a Kubernetes cluster. You can use any cloud-based service like AKS, EKS, GKE, or even a local setup like Minikube.
- **Helm 3**: Make sure you have Helm 3 installed. It's the latest and greatest when it comes to Kubernetes package management.

#### Step 1: Add the Kyverno Helm Repository

First things first, let's add the Kyverno repository to our Helm setup. Open your terminal and run:

```shell
helm repo add kyverno https://kyverno.github.io/kyverno/
```

This command tells Helm where to find the Kyverno charts.

#### Step 2: Update Helm Repositories

To ensure you have the latest list of charts and versions, update your Helm repositories:

```shell
helm repo update
```

This step is like refreshing your package list in traditional package managers.

#### Step 3: Install Kyverno

Now, let's install Kyverno. You can deploy it into a specific namespace or the default one. If you want to create a new namespace for Kyverno, you can add `--create-namespace` to the command. Run:

```shell
helm install kyverno kyverno/kyverno --namespace kyverno --create-namespace
```

This command pulls the Kyverno chart from the repository and installs it in your Kubernetes cluster.

#### Step 4: Verify the Installation

After installation, it's always good to check if everything went smoothly. Run:

```shell
kubectl get pods -n kyverno
```

You should see the Kyverno pods running. If there are any issues, this is where you'll spot them.

#### Step 5: Configure Kyverno Policies

With Kyverno installed, the next step is to set up your policies. Policies in Kyverno are written in YAML and are pretty straightforward to understand and create. You can define what resources are allowed, modify existing resources on the fly, or even generate new resources based on certain conditions.

#### Optional: Customize the Installation

If you need to customize your Kyverno installation, Helm allows you to tweak various settings using a custom `values.yaml` file. For instance, you might want to modify resource limits or enable specific features. Check out the [Kyverno Helm chart documentation](https://github.com/kyverno/kyverno) for more details on what you can customize.

#### Wrapping Up

And there you have it! Installing Kyverno with Helm is a straightforward process that can significantly enhance your Kubernetes policy management. Remember, the key to a successful Kubernetes setup is managing your resources effectively, and Kyverno is a great tool in your arsenal for doing just that.

Happy Kubernetes managing! Stay tuned for more Kubernetes tips and tricks! 🚀💻
