# ARGOCD-BOOTSTRAPPER

## Introduction 

The argocd-bootstrapper leverages the [Argo CD's App of Apps](https://argo-cd.readthedocs.io/en/stable/operator-manual/cluster-bootstrapping/) pattern on `K8S` by using Helm.

## Directory Structure
The following is the directory structure for the bootstrap process:

```bash
.
├── app-of-apps # bootstrap manifest per cluster
├── README.md 
├── app-templates/apps # child app templates (one file per app)
├── app-templates/bootstrap.yaml # bootstrap manifest template
└── cluster # live manifests for parent apps per cluster
└── helpers-crds # deployed crds & helper apps per cluster
```

## Add new bootstrap to cluster

Firstly set environment variable for related cluster.
```
export CLUSTER_NAME=local
export SERVER_ADDR="https://kubernetes.default.svc"
export REPO_URL="https://github.com/omerurhan/argocd-bootstrap.git"
```

Create app of apps bootstrap file
```
cat app-templates/bootstrap.yaml | envsubst '$CLUSTER_NAME,$SERVER_ADDR, $REPO_URL' > app-of-apps/${CLUSTER_NAME}.bootstrap.yaml

```
Copy templates files to related cluster folder
```
cp -R app-templates/apps/* clusters/${CLUSTER_NAME} 
```

## Bootstrapping

To bootstrap, apply the bootstrap.yaml file:

```bash
kubectl apply -f app-of-apps/${CLUSTER_NAME}.bootstrap.yaml
```
