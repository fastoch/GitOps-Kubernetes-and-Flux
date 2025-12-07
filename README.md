# Sources

- https://www.youtube.com/watch?v=GVq-LOfOwzE

# What is Flux?

Flux is an open-source GitOps toolkit that helps us automate how we deploy and manage applications on Kubernetes clusters.  
The key principle is that it uses a Git repository as the single source of truth for managing a given cluster.  

This means that all our application configurations, infrastructure definitions, and deployment specifications are stored in a Git repo.  

Flux is built around 4 core capabilities:
1. Continuous Delivery: it automatically deploys changes to our cluster
2. Declarative Configuration: it specifies the desired state of a system, such as infrastructure, applications, or Kubernetes objects, without detailing the steps to achieve it
3. Automated Reconciliation: it continuously ensures our cluster matches what's defined in our Git repo
4. CNCF-graduated project: it's been thoroughly vetted and is considered production-ready (Cloud Native Computing Foundation)

# GitOps Principles

Flux is built upon the GitOps principles, which are:
1. Git as single source of truth: Git repositories contain the complete and authoritative state of your system
2. Declarative Infrastructure & Applications (same as Declarative Configuration)
3. Automated Deployment & Synchronization: once changes are committed to Git, they're automatically deployed
4. Continuous Reconciliation & Self-Healing: Flux constantly monitors your cluster and automatically fixes any drift from the desired state

# Flux Architecture

Its architecture consists of 3 main layers that work together seamlessly.  
1. Source: Git repos (manifests), Helm repos (packaged apps), OCI registries (container images & artifacts)
2. Control: controllers monitor and reconcile state, they're the brains of Flux
3. Deploy: apply changes to Kubernetes cluster

3/9
