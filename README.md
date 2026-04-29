
## Build the chart

```bash
helm lint .
helm package .
helm push pingpongkong-0.0.3.tgz \
  oci://registry-1.docker.io/kimc1992
```

This creates a chart archive like `pingpongkong-0.0.2.tgz`.

## Install or upgrade

```bash
helm install ppk oci://registry-1.docker.io/kimc1992/pingpongkong \
  --version 0.0.2 \
  --namespace pingpongkong-system --create-namespace \
  --set CONFIG_GIT_TOKEN="glpat-YOUR_REAL_SECRET_TOKEN" \
  --set CONFIG_GIT_CLUSTERNAME="h100-cluster" \
  --set CONFIG_GIT_URL="https://gitlab.company.com/group/pingpongkong-state"
```

```
helm install ppk ./pingpongkong-k8s-helm \
  --namespace pingpongkong-system --create-namespace \
  --set CONFIG_GIT_TOKEN="glpat-YOUR_REAL_SECRET_TOKEN" \
  --set CONFIG_GIT_CLUSTERNAME="h100-cluster" \
  --set CONFIG_GIT_URL="https://gitlab.company.com/group/pingpongkong-state"
```

```bash
helm upgrade --install ppk . \
  --namespace pingpongkong-system --create-namespace \
  --set CONFIG_GIT_TOKEN="glpat-YOUR_REAL_SECRET_TOKEN" \
  --set CONFIG_GIT_CLUSTERNAME="h100-cluster" \
  --set CONFIG_GIT_URL="https://gitlab.company.com/group/pingpongkong-state"
```
