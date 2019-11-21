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

```
kind --version   # Should yield at least 0.6.0
docker ps        # Should not give any errors
kubectl version  # Should at least give application version
#
docker pull kindest/node
```
---

# Create cluster

```
# Create the cluster
kind create cluster
# Just test that it runs OK
kubectl get pods -A
```
---
# ...  and enable GitOps with kustomize

https://docs.fluxcd.io/en/latest/tutorials/get-started-kustomize.html

---
## GitOps

- Often mentioned as part of a CD / CI toolchain
---

## GitOps

- Often mentioned as part of a CD / CI toolchain
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
* Antlr: https://www.antlr.org/
* GraalVM as a platform:
https://www.graalvm.org/docs/graalvm-as-a-platform/
* Truffle:
https://www.graalvm.org/truffle/
* Truffle javadoc:
https://www.graalvm.org/truffle/javadoc/
* https://github.com/jyukutyo/JVM-Math-Language
* https://github.com/graalvm/simplelanguage

]
