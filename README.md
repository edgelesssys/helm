# Edgeless Mesh Helm Chart

Edgeless Mesh is the service mesh for the age of confidential computing.

## Quickstart and documentation

See the [Getting Started Guide](TODO) to set up a distributed confidential-computing app in a few simple steps. 
For more comprehensive documentation, start with the [docs](TODO).

## Adding Edgeless Mesh's Helm repository

```bash
TODO
```

## Installing the chart

1. Create ns

    ```bash
    kubectl create ns edg-mesh
    ```

2. Create secret for private registry

    ```bash
    kubectl -n edg-mesh create secret generic regcred \
    --from-file=.dockerconfigjson=$HOME/.docker/config.json \
    --type=kubernetes.io/dockerconfigjson
    ```

3. Install the chart

    * If your deploying on a cluster with nodes that support SGX1+FLC (e.g. AKS or minikube + Azure Standard_DC*s)

        ```bash
        helm install  edg-mesh-coordinator ./edg-mesh-coordinator
        ```

    * Otherwise

        ```bash
        helm install -f ./nosgx.yaml edg-mesh-coordinator ./edg-mesh-coordinator
        ```

## Configuration
