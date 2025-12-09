# Sources

- https://www.youtube.com/watch?v=GVq-LOfOwzE

# What is Flux?

Flux is an open-source GitOps toolkit that helps us automate how we deploy and manage applications on Kubernetes clusters.  
The key principle is that it uses Git as the single source of truth for managing clusters.  

This means that all our application configurations, infrastructure definitions, and deployment specifications are stored in a Git repo.  

Flux is built around 4 core capabilities:
1. **Continuous Delivery**: it automatically deploys changes to our cluster
2. **Declarative Configuration**: it specifies the desired state of a system, such as infrastructure, applications, or Kubernetes objects, without detailing the steps to achieve it
3. **Automated Reconciliation**: it continuously ensures our cluster matches what's defined in our Git repo
4. **CNCF-graduated project**: it's been thoroughly vetted and is considered production-ready (Cloud Native Computing Foundation)

# GitOps Principles

Flux is built upon the GitOps principles, which are:
1. **Git as single source of truth**: Git repositories contain the complete and authoritative state of your system
2. **Declarative Infrastructure & Applications** (same as Declarative Configuration)
3. **Automated Deployment & Synchronization**: once changes are approved in Git, they're automatically deployed
4. **Continuous Reconciliation & Self-Healing**: Flux constantly monitors your cluster and automatically fixes any drift from the desired state

# Flux Architecture

Its architecture consists of 3 main layers that work together seamlessly:  
1. **Source**: Git repos (manifests), Helm repos (packaged apps), OCI registries (container images & artifacts)
2. **Control**: controllers monitor and reconcile state, they're the brains of Flux
3. **Deploy**: apply approved changes to your Kubernetes cluster

# Core Components

Flux is composed of several specialized controllers that work together as a toolkit:
- **Source controller**: responsible for fetching artifacts from various sources (Git, Helm, or OCI).
  - It keeps track of changes and makes them available to other controllers.
- **Kustomize controller**: applies Kustomize configurations to your clusters.
  - It allows us to customize Kubernetes manifests without modifying the original files.
- **Helm controller**: manages Helm chart releases and upgrades
  - if you're using Helm to package your applications, this controller handles the entire lifecycle
- **Notification controller**: handles events and webhook notifications
  - it can send alerts when deployments succeed or fail
  - it can receive webhooks from Git providers to trigger immediate reconciliation when code is pushed

# GitRepository resource

`GitRepository` is a Custom Resource Definition (**CRD**) from FluxCD's source-controller that defines a source for fetching and archiving Git repository contents as a tarball artifact for Kubernetes reconciliation in GitOps workflows.

Here's an example of a GitRepository resource definition (YAML file):
```yaml
apiVersion: source.toolkit.fluxcd.io/v1
kind: GitRepository
metadata:
  name: my-app
spec:
  interval: 1m
  url: https://github.com/org/my-app
  ref:
    branch: main
```
The first line tells Kubernetes this is a Flux source resource.  
Flux will check this Git repo for changes every minute.  
The URL points to the GitHub repo location.  
The ref section specifies which branch to monitor.  

The above spec tells Flux where to find the application configuration, and how often to check for updates.  

# Kustomization resource

```yaml
apiVersion: kustomize.toolkit.fluxcd.io/v1
kind: Kustomization
metadata:
  name: my-app
spec:
  interval: 5m
  sourceRef:
    kind: GitRepository
    name: my-app
  path: ./deploy
  prune: true
```
Here, the spec section defines how to deploy the configuration.  
Flux will reconcile this resource every 5 minutes.  
The sourceRef section links this Kustomization to the Git repo we've defined earlier.  
The path field specifies which directory in the repository contains the manifests to deploy.  

`prune: true` = if you delete a manifest from the Git repo, Flux will delete the corresponding resource from your cluster.  
This ensures your cluster stays perfectly synchronized with Git.

# The Reconciliation Loop

The Reconciliation Loop is the heart of how Flux operates.  
It's a continuous cycle that keeps you cluster in sync with Git.  

1. Flux pulls the latest changes from your Git repository. It's constantly watching for commits and updates.
2. Flux compares the desired state defined in Git with the actual state currently running in your cluster.
3. If it detects differences, Flux applies the necessary changes to bring the cluster to the desired state.
4. This could mean creating new resources, updating existing ones, or deleting resources that no longer exist in Git.
5. After applying changes, the loop repeats at the defined interval.

This continuous process ensures your cluster is always synchronized with your Git repository, and provides self-healing  
capabilities if manual changes are made to the cluster.  

# Key Benefits

Flux provides several compelling benefits for managing Kubernetes clusters.  
1. **Audit Trail**:
2. 

7/9
