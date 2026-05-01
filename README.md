
## Build the chart

```bash
helm lint .
helm package .
helm push pingpongkong-0.0.5.tgz \
  oci://registry-1.docker.io/kimc1992
```

This creates a chart archive like `pingpongkong-0.0.5.tgz`.

## Install or upgrade

```bash
helm install ppk oci://registry-1.docker.io/kimc1992/pingpongkong \
  --version 0.0.5 \
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

By default the chart also creates `default/pingpongkong-matrix` with key
`matrix.yaml`, and grants the agent ServiceAccount permission to get/list/watch
ConfigMaps in `default`.

## Runtime settings

```yaml
logLevel: INFO # TRACE, DEBUG, INFO, WARN, ERROR

collector:
  updateInterval: 5m
  apiPort: 8081

agent:
  checkInterval: 5m
  apiPort: 8080
```
