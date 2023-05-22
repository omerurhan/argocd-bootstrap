# ARGOCD-BOOTSTRAPPER


```
# Add cluster to bootstrap
export CLUSTER_NAME=local
export SERVER_ADDR="https://kubernetes.default.svc"
export REPO_URL="https://github.com/omerurhan/argocd-bootstrap.git"

cat bootstrap-template/bootstrap.yaml | envsubst '$CLUSTER_NAME,$SERVER_ADDR, $REPO_URL' > ${CLUSTER_NAME}.bootstrap.yaml

kubectl apply -f ${CLUSTER_NAME}.bootstrap.yaml
```
