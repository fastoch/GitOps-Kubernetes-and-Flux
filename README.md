# Sources

- https://www.youtube.com/watch?v=GVq-LOfOwzE

# What is Flux?

Flux is an open-source GitOps toolkit that helps us automate how we deploy and manage applications on Kubernetes clusters.  
The key principle is that it uses a Git repository as the single source of truth for managing a given cluster.  

This means that all our application configurations, infrastructure definitions, and deployment specifications are stored in a Git repo.  

Flux is built around 4 core capabilities:
1. Continuous Delivery: it automatically deploys changes to our cluster
2. Declarative Configuration: it specifies the desired state of a system, such as infrastructure, applications, or Kubernetes objects, without detailing the exact steps to achieve it
3. Automated Reconciliation: it continuously ensures our cluster matches what's defined in our Git repo
4. CNCF-graduated project: it's been thoroughly vetted and is considered production-ready (Cloud Native Computing Foundation)

# GitOps Principles



1/9
