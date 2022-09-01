## To create cluster
```
eksctl create cluster -f eksctl/create-cluster/create-cluster-west-2.yaml

```

## To Delete Cluster
```
eksctl delete cluster -f eksctl/create-cluster/create-cluster-west-2.yaml

```
## To generate cluster template
```
eksctl create cluster --name development --dry-run > template.yaml
```

## Create & Associate IAM OIDC Provider for our EKS Cluster
- To enable and use AWS IAM roles for Kubernetes service accounts on our EKS cluster, we must create & associate OIDC identity provider.

```
eksctl utils associate-iam-oidc-provider \
    --region us-east-1 \
    --cluster eksdemo-live \
    --approve

```
