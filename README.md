
```
helm install ppk ./pingpongkong-k8s-helm \
  --namespace pingpongkong-system --create-namespace \
  --set auth.gitToken="glpat-YOUR_REAL_SECRET_TOKEN" \
  --set collector.stateRepoUrl="https://gitlab.company.com/api/v4/projects/123/repository/files/k8s%2Fh100-cluster.yaml/raw?ref=main"
```
