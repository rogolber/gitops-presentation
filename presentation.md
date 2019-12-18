name: inverse
layout: true
class: center, middle, inverse
---
# GitOps

.footnote[19.12.2019 Erlend Nossum]
???

Made with: https://github.com/gnab/remark

---
layout: false
## Agenda
.left-column[
] .right-column[
- Recapitulation of dependent technology
- Preliminaries
- What is GitOps?
- What is fluxcd?
- Sing-along (mac supported):
  - How to setup up fluxcd in kubernetes on your local computer
]
???
- Flux from weaveworks
---
## Tech recap
.left-column[
] .right-column[
- docker
- kubernetes
  - kustomize
- ops and devops
- ... and chatops
- cloud solutions
]
???
Alternatives to kustomize is jsonnet and helm
---
## Tooling - what is presented today

Install:
- https://docs.docker.com/install/
- https://kubernetes.io/docs/tasks/tools/install-kubectl/
- https://github.com/kubernetes-sigs/kind
- https://docs.fluxcd.io/en/latest/references/fluxctl.html

```
kind --version   # Should yield at least 0.6.0
docker ps        # Should not give any errors
kubectl version  # Should at least give 1.14
fluxctl version  # Should at least give 1.16.0
#
docker pull kindest/node:v1.16.3
docker pull nginx:1.17.6
```
???
- Docker for containers
- kubectl for kubernetes interaction
- kind to run kubernetes in docker
- flux for gitops

---
## GitOps

- git repository is the source of **truth** for a system's configuration
- configuration as code <br/>https://rollout.io/blog/configuration-as-code-everything-need-know/
- when the actual state of the system drifts from the desired state
  - k8s good fit
  - kustomize, patches and namespace
- Easily set up as part of a CD / CI toolchain

---
## Fluxcd
- From https://weave.works
- A CNCF project
- Argo-flux collaboration
  - AWS wants to adopt flux
  - https://github.com/argoproj/gitops-engine/
  - Effectively merging Flux and ArgoCD into a single solution is a long term goal: https://github.com/argoproj/gitops-engine/blob/master/specs/design.md
    - https://github.com/fluxcd/flux/tree/gitops-engine-poc
    - https://github.com/argoproj/argo-cd/tree/gitops-engine-poc
???
* AWS wants to adopt flux: https://aws.amazon.com/blogs/containers/help-us-write-a-new-chapter-for-gitops-kubernetes-and-open-source-collaboration/
---
name: inverse
layout: true
class: center, middle, inverse
---
# Practical example
---
layout: false
## Fire up docker based kubernetes

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

Follow flux tutorial
- https://docs.fluxcd.io/en/latest/tutorials/get-started-kustomize.html
- https://github.com/nostra/gitops-presentation

```
kubectl apply -k fluxcd
fluxctl identity --k8s-fwd-ns flux
kubectl logs -n flux -f flux
```

---
## Load your own docker image

Create an example docker image...

```
cd dockerimage
docker build -t local-test:v1 .
kind load docker-image local-test:v1
cd ..
fluxctl --k8s-fwd-ns=flux sync
kc port-forward svc/nginx-test 8080
```

---
## Update the example deployment

```
docker build -t local-test:v2 .
kind load docker-image local-test:v2
vi k8s/nginx.yaml  # Update the image reference
git commit k8s/nginx.yaml -m "Update"
git push
kc port-forward svc/nginx-test 8080
```

---
name: inverse
layout: true
class: center, middle, inverse
---
# What did we learn?
