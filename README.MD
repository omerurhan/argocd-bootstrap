# ARGOCD-BOOTSTRAPPER


```
# Add cluster to bootstrap
export CLUSTER_NAME=local
export SERVER_ADDR="https://kubernetes.default.svc"
export REPO_URL=""

cat bootstrap-templates/bootstrap.yaml | envsubst '$CLUSTER_NAME,$SERVER_ADDR, $REPO_URL' > ${CLUSTER_NAME}.bootstrap.yaml
```
