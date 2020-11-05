# Edgeless Mesh Helm Chart

Edgeless Mesh is the service mesh for the age of confidential computing.

## Quickstart and documentation

See the [Getting Started Guide](TODO) to set up a distributed confidential-computing app in a few simple steps. 
For more comprehensive documentation, start with the [docs](TODO).

## Adding Edgeless Mesh's Helm repository

```bash
helm repo add edg-mesh https://helm.edgeless.systems
helm repo update
```

## Installing the chart

### From the helm repo

* If your deploying on a cluster with nodes that support SGX1+FLC (e.g. AKS or minikube + Azure Standard_DC*s)

    ```bash
    helm install  edg-mesh-coordinator edg-mesh/coordinator --create-namespace edg-mesh
    ```

* Otherwise

    ```bash
    helm install edg-mesh-coordinator edg-mesh/coordinator --create-namespace edg-mesh --set coordinator.resources=null --set coordinator.OE_SIMULATION=1 --set tolerations=null
    ```

### From this repsoitory

* If your deploying on a cluster with nodes that support SGX1+FLC (e.g. AKS or minikube + Azure Standard_DC*s)

    ```bash
    helm install  edg-mesh-coordinator ./coordinator --create-namespace edg-mesh
    ```

* Otherwise

    ```bash
    helm install edg-mesh-coordinator ./coordinator --create-namespace edg-mesh --set coordinator.resources=null --set coordinator.OE_SIMULATION=1 --set tolerations=null
    ```

## Update the chart repository

```bash
helm package coordinator
mv coordinator-x.x.x.tgz docs
helm repo index docs --url https://helm.edgless.systems
```


## Configuration

The following table lists the configurable parameters of the Linkerd2 chart and
their default values.

| Parameter                                   | Description                                                                                                                                                                           | Default                              |
|:--------------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-------------------------------------|
| `coordinatorImage`                           | Docker image for the coordinator component                                                                                                                          | `ghcr.io/edgelesssys/coordinator`       |
| `coordinatorReplicas`                        | Number of replicas for each control plane pod                                                                                                                                         | `1`                                  |                              |                             |
| `coordinator.EDG_MESH_SERVER_HOST`           | Hostname of the mesh-api server                                                                                                                                                       | `0.0.0.0` |
| `coordinator.EDG_MESH_SERVER_PORT`           | Port of the mesh-api server, needs match the data-plane configuration                                                                                                                 | `25554` |
| `coordinator.EDG_CLIENT_SERVER_HOST`         | Hostname of the client-api server                                                                                                                                                     | `0.0.0.0` |
| `coordinator.EDG_CLIENT_SERVER_PORT`         | Port of the client-api server, needs match the client tool-stack configuration                                                                                                        | `25555` |
| `coordinator.EDG_COORDINATOR_DNS_NAMES`      | DNS-Names for the coordinator certificate, need contain the coordinator's hostname                                                                                                    | `coordinator-mesh-api,coordinator-client-api,coordinator-mesh-api.emojivoto,coordinator-client-api.emojivoto,coordinator-mesh-api.emojivoto.svc.cluster.local,coordinator-client-api.emojivoto.svc.cluster.local` |
| `coordinator.EDG_COORDINATOR_SEAL_DIR`       | Path to the directory used for sealing data. Needs to be consistent with the persisten storage setup                                                                                  | `/coordinator/data/` |
| `coordinator.OE_SIMULATION`                  | SGX simulation settings, set to 1 if your not running on an SGX capable cluster                                                                                                        | `0` |
| `global.coordinatorComponentLabel`           | Control plane label. Do not edit                                                                                                                                                      | `edgeless.systems/control-plane-component` |
| `global.coordinatorImageVersion`             | Tag for the coordinator container docker image                                                                                                                                         | latest version                       |
| `global.coordinatorNamespaceLabel`           | Control plane label. Do not edit                                                                                                                                                      | `edgeless.systems/control-plane-ns`        |                                                                                                                                    |                                 |
| `global.podLabels`                          | Additional labels to add to all pods                                                                                                                                                  | `{}`                                 |
| `global.podAnnotations`                     | Additional annotations to add to all pods                                                                                                                                             | `{}`                                 |                    |
| `global.imagePullPolicy`                    | Docker image pull policy                                                                                                                                                              | `IfNotPresent`                       |                     |
| `global.namespace`                          | Control plane namespace                                                                                                                                                               | `edg-mesh`                            |
| `nodeSelector`                        | NodeSelector section, See the [K8S documentation](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/#nodeselector) for more information                                   | `beta.kubernetes.io/os: linux`                                 |
| `tolerations`                        | Tolerations section, See the [K8S documentation](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/) for more information                                   | `{}`                                 |
