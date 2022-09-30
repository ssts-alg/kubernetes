# ConfigMaps

A ConfigMap is an API object used to store non-confidential data in key-value pairs. Pods can consume ConfigMaps as environment variables, command-line arguments, or as configuration files in a volume.

A ConfigMap allows you to decouple environment-specific configuration from your container images, so that your applications are easily portable.

#### Create Configmap
`kubectl create configmap test-map --from-literal=vpc_id="vpc-12345" --from-literal=db_name=dev-db`

#### Create config map from yaml file

`kubectl create -f config_map.yaml`
`kubectl create -f pod.yaml`

#### Describe configmap
`kubectl describe cm CONFIG_MAP_NAME`

### To validate
`kubectl exec -it myapp bash`
`cd /etc/dev-mount`

from here you can able to find the values
