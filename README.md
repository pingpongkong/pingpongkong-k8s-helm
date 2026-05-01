
## Build the chart

```bash
helm lint .
helm package .
helm push pingpongkong-0.0.8.tgz \
  oci://registry-1.docker.io/kimc1992
```

This creates a chart archive like `pingpongkong-0.0.5.tgz`.

## Install or upgrade

```bash
helm install ppk oci://registry-1.docker.io/kimc1992/pingpongkong \
  --version 0.0.8 \
  --namespace pingpongkong-system --create-namespace \
  --set CONFIG_GIT_TOKEN="glpat-YOUR_REAL_SECRET_TOKEN" \
  --set K8S_CLUSTERNAME="h100-cluster" \
  --set CONFIG_GIT_URL="https://gitlab.company.com/group/pingpongkong-state" \
  --set LOG_LEVEL=DEBUG \
  --set COLLECTOR_UPDATE_INTERVAL=5m \
  --set AGENT_CHECK_INTERVAL=5m \
  --set AGENT_API_PORT=8080 \
  --set COLLECTOR_API_PORT=8081
```

```
helm install ppk ./pingpongkong-k8s-helm \
  --namespace pingpongkong-system --create-namespace \
  --set CONFIG_GIT_TOKEN="glpat-YOUR_REAL_SECRET_TOKEN" \
  --set K8S_CLUSTERNAME="h100-cluster" \
  --set CONFIG_GIT_URL="https://gitlab.company.com/group/pingpongkong-state" \
  --set LOG_LEVEL=DEBUG \
  --set COLLECTOR_UPDATE_INTERVAL=5m \
  --set AGENT_CHECK_INTERVAL=5m \
  --set AGENT_API_PORT=8080 \
  --set COLLECTOR_API_PORT=8081
```

```bash
helm upgrade --install ppk . \
  --namespace pingpongkong-system --create-namespace \
  --set CONFIG_GIT_TOKEN="glpat-YOUR_REAL_SECRET_TOKEN" \
  --set K8S_CLUSTERNAME="h100-cluster" \
  --set CONFIG_GIT_URL="https://gitlab.company.com/group/pingpongkong-state" \
  --set LOG_LEVEL=DEBUG \
  --set COLLECTOR_UPDATE_INTERVAL=5m \
  --set AGENT_CHECK_INTERVAL=5m \
  --set AGENT_API_PORT=8080 \
  --set COLLECTOR_API_PORT=8081
```

By default the chart also creates
`pingpongkong-system/pingpongkong-sample-cluster-ping-state` with key
`desiredPingState.yaml`, grants the agent ServiceAccount permission to
get/list/watch ConfigMaps, and grants the collector ServiceAccount permission to
get/patch ConfigMaps in the release namespace. `K8S_NAMESPACE` is injected from
the pod namespace by Kubernetes.

## Runtime settings

These chart values are rendered as runtime environment variables with the same names:

| Helm value / environment variable | Allowed/example values | Default |
| --- | --- | --- |
| `K8S_CLUSTERNAME` | cluster name, for example `h100-cluster` | `sample-cluster` |
| `LOG_LEVEL` | `TRACE`, `DEBUG`, `INFO`, `WARN`, `ERROR` | `INFO` |
| `COLLECTOR_UPDATE_INTERVAL` | `30s`, `5m`, `1h` | `5m` |
| `AGENT_CHECK_INTERVAL` | `30s`, `5m`, `1h` | `5m` |
| `AGENT_API_PORT` | port number, for example `8080` | `8080` |
| `COLLECTOR_API_PORT` | port number, for example `8081` | `8081` |

```yaml
K8S_CLUSTERNAME: sample-cluster
LOG_LEVEL: INFO # TRACE, DEBUG, INFO, WARN, ERROR
COLLECTOR_UPDATE_INTERVAL: 5m
AGENT_CHECK_INTERVAL: 5m
AGENT_API_PORT: 8080
COLLECTOR_API_PORT: 8081

matrixConfigMap:
  key: desiredPingState.yaml
```
