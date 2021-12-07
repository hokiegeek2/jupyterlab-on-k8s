# jupyterlab-on-k8s

The jupyterlab-on-k8s project is a simple means of deploying jupyterlab on Kubernetes.

## Docker Build

```
export VERSION=0.0.1
export JUPYTER_VERSION=3.0.0

docker build --build-arg JUPYTER_VERSION=$JUPYTER_VERSION -f src/docker/jupyterlab-docker -t hokiegeek2/jupyterlab-k8s:$VERSION .
```

## Helm Install

### values.yaml Options

```
######################## Pod Settings ########################

releaseVersion: 0.0.1
imagePullPolicy: IfNotPresent

#################### Jupyterlab Settings #####################

app:
  namespace: default
  numServers: 1
  resources:
    limits:
      cpu: 500m
      memory: 512Mi
    requests:
      cpu: 250m
      memory: 256Mi

service:
  name: jupyterlab
  port: 8888
  targetPort: 8888
  type: LoadBalancer

```

### Install Command

```
helm install jupyterlab deployment/charts/jupyterlab-on-k8s/
```
