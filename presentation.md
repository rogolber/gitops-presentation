name: inverse
layout: true
class: center, middle, inverse
---
# Gitops

.footnote[19.12.2019 Erlend Nossum]
???

Made with: https://github.com/gnab/remark

---
layout: false
## Agenda
.left-column[
] .right-column[
- Recapitulation of dependent technology
- Preliminaries for sing-along
- What is GitOps?
- What is fluxcd
- Sing-along (mac supported):
  - How to setup up fluxcd in kubernetes on your local computer
]
???

---
## Tech recap

- cloud solutions
- docker
- kubernetes
  - kustomize
- ops og devops

---
## Tooling

Install:
- https://docs.docker.com/install/
- https://kubernetes.io/docs/tasks/tools/install-kubectl/
- https://github.com/kubernetes-sigs/kind
- https://docs.fluxcd.io/en/latest/references/fluxctl.html

```
kind --version   # Should yield at least 0.6.0
docker ps        # Should not give any errors
kubectl version  # Should at least give application version
#
docker pull kindest/node:v1.16.3
fluxctl identity --k8s-fwd-ns flux
fluxctl sync --k8s-fwd-ns flux
```
---

# Create cluster

```
# Create the cluster
kind create cluster
# Just test that it runs OK
kubectl get pods -A
kubectl config get-contexts
kubectl config use-context kind-kind  
```
---
# ...  and enable GitOps with kustomize

https://docs.fluxcd.io/en/latest/tutorials/get-started-kustomize.html
```
mkdir fluxcd
# ... follow instructions

```

---
## GitOps

- Often mentioned as part of a CD / CI toolchain
- git repository is the source of truth for a system’s configuration,
- configuration as code https://rollout.io/blog/configuration-as-code-everything-need-know/
- when the actual state of the system drifts from the desired state.
  - k8s good fit

Argo-flux collaberation
- https://github.com/argoproj/gitops-engine/
- Effectively merging Flux and ArgoCD into a single solution is a long term goal: https://github.com/argoproj/gitops-engine/blob/master/specs/design.md
  - https://github.com/fluxcd/flux/tree/gitops-engine-poc
  - https://github.com/argoproj/argo-cd/tree/gitops-engine-poc

---
## title

- bullet

???

---
## GitOps tooling

- bullet

---
## Fluxcd
- From weaveworks
- A CNCF project
- Often mentioned

---
## Resources
.left-column[
] .right-column[
* Fluxcd: https://docs.fluxcd.io/en/latest/tutorials/get-started-kustomize.html
* Kind https://kind.sigs.k8s.io/
* AWS wants to adopt flux: https://aws.amazon.com/blogs/containers/help-us-write-a-new-chapter-for-gitops-kubernetes-and-open-source-collaboration/
]
