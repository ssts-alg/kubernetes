## Helm is the package manager for Kubernetes:

## Installing Helm:

In mac os `brew install helm`

In Linux/Mac/JenkinsLinux:
  1. Download from [Link](https://github.com/helm/helm/releases)
  2. `tar -zxvf helm-v3.0.0-linux-amd64.tar.gz`
  3. `mv linux-amd64/helm /usr/local/bin/helm`

***Reference:*** https://helm.sh/docs/intro/install/

***Note:*** If you want to install helm in Windows Download from [Link](https://github.com/helm/helm/releases) and set path in environment variables.

### HELM Commands:

#### To Generate Skelton for Helm Cart:

`helm create myapp`

Modify values according to your requirement.

#### To generate package use following command:

`helm package myapp` --> It will generate random version for package.

`helm package myapp --version 0.1.2` --> To specify package version

#### To deploy app into kubernetes:

`helm install myapp myapp-0.1.0.tgz`

#### To upgrade app in kubernetes:

`helm upgrade myapp myapp-0.1.1.tgz`

#### To list all deployments in helm:
`helm list`

#### To to delete app in helm:
`helm delete myapp`

## Pushing Helm charts to AWS ECR (Elastic Container Registry):

1. `aws ecr create-repository --repository-name myapp --region us-west-2`
2. `aws ecr get-login-password --region us-west-2 | helm registry login --username AWS --password-stdin 1234567890.dkr.ecr.us-west-2.amazonaws.com`.
3. `helm push myapp-0.0.0.tgz oci://1234567890.dkr.ecr.us-west-2.amazonaws.com/`
4. **Optional:** `aws ecr describe-images --repository-name myapp --region us-west-2`


## Download Helm chart from ECR:

1. `aws ecr get-login-password \
     --region us-west-2 | helm registry login \
     --username AWS \
     --password-stdin 1234567890.dkr.ecr.us-west-2.amazonaws.com`
2. `helm install myapp oci://1234567890.dkr.ecr.us-west-2.amazonaws.com/myapp --version 0.0.0`
3. To list `helm list -n default`
4. **Optional:**`kubectl describe configmap helm-test-chart-configmap`
5. To uninstall helm chart `helm uninstall myapp`.
