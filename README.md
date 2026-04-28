
```
helm install ppk ./pingpongkong-k8s-helm \
  --namespace pingpongkong-system --create-namespace \
  --set auth.gitToken="glpat-YOUR_REAL_SECRET_TOKEN" \
  --set clusterName="h100-cluster" \
  --set repoApiUrl="https://gitlab.company.com/api/v4/projects/123/repository/files"
```
