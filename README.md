
## Build the chart

```bash
helm lint .
helm package .
helm push pingpongkong-0.0.16.tgz \
  oci://registry-1.docker.io/kimc1992
```


## GET CLUSTER NAME
```
kubectl config current-context
```


## Install or upgrade

```bash
helm install ppk oci://registry-1.docker.io/kimc1992/pingpongkong \
  --version 0.0.16 \
  --namespace pingpongkong --create-namespace \
  --set CONFIG_GIT_TOKEN="glpat-YOUR_REAL_SECRET_TOKEN" \
  --set CONFIG_GIT_CLUSTERNAME="h100-cluster" \
  --set CONFIG_GIT_URL="https://gitlab.company.com/group/pingpongkong-state.git" \
  --set LOG_LEVEL=INFO \
  --set COLLECTOR_UPDATE_INTERVAL=5m \
  --set AGENT_CHECK_INTERVAL=5m \
  --set AGENT_API_PORT=8080 \
  --set COLLECTOR_API_PORT=8081
```

```
helm install ppk ./pingpongkong-k8s-helm \
  --namespace pingpongkong --create-namespace \
  --set CONFIG_GIT_TOKEN="glpat-YOUR_REAL_SECRET_TOKEN" \
  --set CONFIG_GIT_CLUSTERNAME="h100-cluster" \
  --set CONFIG_GIT_URL="https://gitlab.company.com/group/pingpongkong-state.git" \
  --set LOG_LEVEL=DEBUG \
  --set COLLECTOR_UPDATE_INTERVAL=5m \
  --set AGENT_CHECK_INTERVAL=5m \
  --set AGENT_API_PORT=8080 \
  --set COLLECTOR_API_PORT=8081
```

```bash
helm upgrade --install ppk . \
  --namespace pingpongkong --create-namespace \
  --set CONFIG_GIT_TOKEN="glpat-YOUR_REAL_SECRET_TOKEN" \
  --set CONFIG_GIT_CLUSTERNAME="h100-cluster" \
  --set CONFIG_GIT_URL="https://gitlab.company.com/group/pingpongkong-state.git" \
  --set LOG_LEVEL=DEBUG \
  --set COLLECTOR_UPDATE_INTERVAL=5m \
  --set AGENT_CHECK_INTERVAL=5m \
  --set AGENT_API_PORT=8080 \
  --set COLLECTOR_API_PORT=8081
```

The collector creates and patches the ping-state ConfigMap in the release
namespace. The chart grants the agent ServiceAccount permission to get/list/watch
ConfigMaps and get/list/watch Nodes. It grants the collector ServiceAccount
permission to get/create/patch ConfigMaps in that namespace and get/list/watch
Nodes. `K8S_NAMESPACE` is injected from the pod namespace by Kubernetes.

## Runtime settings

These chart values are rendered as runtime environment variables with the same names:

| Helm value / environment variable | Allowed/example values | Default |
| --- | --- | --- |
| `CONFIG_GIT_CLUSTERNAME` | Git config directory/file stem, for example `h100-cluster` | `sample-cluster` |
| `LOG_LEVEL` | `TRACE`, `DEBUG`, `INFO`, `WARN`, `ERROR` | `INFO` |
| `COLLECTOR_UPDATE_INTERVAL` | `30s`, `5m`, `1h` | `5m` |
| `AGENT_CHECK_INTERVAL` | `30s`, `5m`, `1h` | `5m` |
| `AGENT_API_PORT` | port number, for example `8080` | `8080` |
| `COLLECTOR_API_PORT` | port number, for example `8081` | `8081` |

```yaml
CONFIG_GIT_CLUSTERNAME: sample-cluster
LOG_LEVEL: INFO # TRACE, DEBUG, INFO, WARN, ERROR
COLLECTOR_UPDATE_INTERVAL: 5m
AGENT_CHECK_INTERVAL: 5m
AGENT_API_PORT: 8080
COLLECTOR_API_PORT: 8081
```
