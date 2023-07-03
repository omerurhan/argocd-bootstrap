# LCW K8S Bootstrapping using Argo CD

## Introduction

The argocd-bootstrapper leverages the [Argo CD's App of Apps](https://argo-cd.readthedocs.io/en/stable/operator-manual/cluster-bootstrapping/) pattern on `RKE2` by using Helm.

## Bootstrap Directory Structure
The following is the directory structure for the bootstrap process:

```bash
.
├── Chart.yaml # boiler plate chart.yaml
├── README.md 
├── templates # child app templates (one file per app)
└── values.yaml # bootstrapper chart overrides: enable/disable apps
```

In this case, the parent app "**bootstrap**" is installed along with its *child apps* which are rendered from `templates/`  directories.
By default, most of the apps are disabled. You can easily enable them by setting the flags in the [values.yaml](./values.yaml)

## Enabling Apps

To enable/disable apps, modify the enable flag in the values.yaml file.

```yaml
# values.yaml
kyverno:
  enable: false  
logging:
  enable: false
observability:
  enable: false
  storageSize: 150Gi
  retention: 30d
trivy:
  enable: false
```


## Bootstrapping

To bootstrap, apply the bootstrap.yaml file:

```bash
kubectl apply -f https://raw.githubusercontent.com/kloia/argocd-eks-bootstrapper/main/bootstrap.yaml
```