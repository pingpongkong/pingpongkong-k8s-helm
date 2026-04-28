
## Build the chart

```bash
helm lint .
helm package .
helm push pingpongkong-0.0.1.tgz \
  oci://registry-1.docker.io/kimc1992
```

This creates a chart archive like `pingpongkong-0.1.0.tgz`.

## Install or upgrade

```
helm install ppk ./pingpongkong-k8s-helm \
  --namespace pingpongkong-system --create-namespace \
  --set auth.gitToken="glpat-YOUR_REAL_SECRET_TOKEN" \
  --set clusterName="h100-cluster" \
  --set repoApiUrl="https://gitlab.company.com/api/v4/projects/123/repository/files"
```

```bash
helm upgrade --install ppk . \
  --namespace pingpongkong-system --create-namespace \
  --set auth.gitToken="glpat-YOUR_REAL_SECRET_TOKEN" \
  --set clusterName="h100-cluster" \
  --set repoApiUrl="https://gitlab.company.com/api/v4/projects/123/repository/files"
```
