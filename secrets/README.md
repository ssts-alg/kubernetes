# Kubernetes secrets used to store sensitive data


## 1. Pulling private images using Secrets

#### Create kubernetes secrets using command line

```
kubectl create secret docker-registry docker-creds --docker-server=https://index.docker.io/v1/ --docker-username=sstechnosolutions --docker-password=<your-password> --docker-email=sstechnosolutions3@gmail.com
```
#### Create ssecrets using config.json

The following command will create config.json file in your <home-dir>/.docker/config.json
```
docker login
```

```
kubectl create secret generic docker-creds --from-file=.dockerconfigjson=/home/ec2-user/.docker/config.json --type=kubernetes.io/dockerconfigjson
```

After create secret, lets create pod which uses private images.

```
apiVersion: v1
kind: Pod
metadata:
  name: private-reg
spec:
  containers:
  - name: privateapp
    image: sstechnosolutions/myapp:v0
  imagePullSecrets:
  - name: docker-creds

```

Create pod which uses private image

```
kubectl create -f https://raw.githubusercontent.com/sstechnosolutions/kubernetes/master/secrets/private_pod.yaml
```



#### To generate skelton
```
kubectl create secret docker-registry --dry-run=client docker-creds \
  --docker-server=https://index.docker.io/v1/ \
  --docker-username=sstechnosolutions \
  --docker-password=admin12345 \
  --docker-email=sstechnosolutions3@gmail.com -o yaml > docker-secret.yaml
```

## Examples

#### Create a new secret named my-secret with keys for each file in folder bar
  `kubectl create secret generic my-secret --from-file=path/to/bar`

#### Create a new secret named my-secret with specified keys instead of names on disk
  `kubectl create secret generic my-secret --from-file=ssh-privatekey=~/.ssh/id_rsa --from-file=ssh-publickey=~/.ssh/id_rsa.pub`

#### Create a new secret named my-secret with key1=supersecret and key2=topsecret
  `kubectl create secret generic my-secret --from-literal=key1=supersecret --from-literal=key2=topsecret`
