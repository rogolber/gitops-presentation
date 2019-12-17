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
- Preliminaries for sing-along
- What is GitOps?
- What is fluxcd
- Sing-along (mac supported):
  - How to setup up fluxcd in kubernetes on your local computer
]
???

---
## Tech recap

- docker
- kubernetes
  - kustomize
- ops and devops
- ... and chatops
- cloud solutions

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
kubectl version  # Should at least give 1.14
fluxctl version  # Should at least give 1.16.0
#
docker pull kindest/node:v1.16.3
docker pull nginx:1.17.6
```

---
## GitOps

- git repository is the source of truth for a system’s configuration,
- configuration as code https://rollout.io/blog/configuration-as-code-everything-need-know/
- when the actual state of the system drifts from the desired state.
  - k8s good fit
- Easily set up as part of a CD / CI toolchain


---
name: inverse
layout: true
class: center, middle, inverse
---
# Load your own docker image
---
layout: false
## Example: Docker image

```
cd dockerimage
docker build -t local-test:v1 .
kind load docker-image local-test:v1
cd ..
fluxctl --k8s-fwd-ns=flux sync
kc port-forward svc/nginx-test 8080

docker build -t local-test:v2 .
kind load docker-image local-test:v2
```

???

---
## GitOps tooling

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

```
kubectl apply -k fluxcd
fluxctl identity --k8s-fwd-ns flux
fluxctl --k8s-fwd-ns=flux sync
```

---
## Fluxcd
- From weaveworks
- A CNCF project
- Argo-flux collaberation
  - https://github.com/argoproj/gitops-engine/
  - Effectively merging Flux and ArgoCD into a single solution is a long term goal: https://github.com/argoproj/gitops-engine/blob/master/specs/design.md
    - https://github.com/fluxcd/flux/tree/gitops-engine-poc
    - https://github.com/argoproj/argo-cd/tree/gitops-engine-poc

---
## title

- bullet

???


---
## Resources
.left-column[
] .right-column[
* Fluxcd: https://docs.fluxcd.io/en/latest/tutorials/get-started-kustomize.html
* Kind https://kind.sigs.k8s.io/
* AWS wants to adopt flux: https://aws.amazon.com/blogs/containers/help-us-write-a-new-chapter-for-gitops-kubernetes-and-open-source-collaboration/
]
