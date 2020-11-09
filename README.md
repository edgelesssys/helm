# Edgeless Systems - Helm charts

## Documentation

See the [Getting Started Guide](TODO) to set up a distributed confidential-computing app in a few simple steps. 
For more comprehensive documentation, start with the [docs](TODO).

## Add Repository (stable)

```bash
helm repo add edgeless https://helm.edgeless.systems/stable
helm repo update
```

## Install Packages (stable)

* If your deploying on a cluster with nodes that support SGX1+FLC (e.g. AKS or minikube + Azure Standard_DC*s)

    ```bash
    helm install  edg-mesh-coordinator edgeless/coordinator --create-namespace edg-mesh
    ```

* Otherwise

    ```bash
    helm install edg-mesh-coordinator edgeless/coordinator --create-namespace edg-mesh --set coordinator.resources=null --set coordinator.simulation=1 --set tolerations=null
    ```

## Configuration

The following table lists the configurable parameters of the coordinator chart and
their default values.

| Parameter                                    | Description    | Default                              |
|:---------------------------------------------|:---------------|:-------------------------------------|
| `coordinatorImage`                           | Docker image for the coordinator component | `ghcr.io/edgelesssys/coordinator` |
| `coordinatorReplicas`                        | Number of replicas for each control plane pod | `1` |
| `coordinator.meshServerHost`                 | Hostname of the mesh-api server | `0.0.0.0` |
| `coordinator.meshServerPort`                 | Port of the mesh-api server configuration | `25554` |
| `coordinator.clientServerHost`               | Hostname of the client-api server | `0.0.0.0` |
| `coordinator.clientServerPort`               | Port of the client-api server configuration | `25555` |
| `coordinator.dnsNames`                       | DNS-Names for the coordinator certificate | `coordinator-mesh-api,coordinator-client-api,coordinator-mesh-api.edg-mesh,coordinator-client-api.edg-mesh,coordinator-mesh-api.edg-mesh.svc.cluster.local,coordinator-client-api.edg-mesh.svc.cluster.local` |
| `coordinator.sealDir`                        | Path to the directory used for sealing data. Needs to be consistent with the persisten storage setup | `/coordinator/data/` |
| `coordinator.simulation`                     | SGX simulation settings, set to 1 if your not running on an SGX capable cluster | `0` |
| `global.coordinatorComponentLabel`           | Control plane label. Do not edit | `edgeless.systems/control-plane-component` |
| `global.coordinatorImageVersion`             | Tag for the coordinator container docker image | latest version |
| `global.coordinatorNamespaceLabel`           | Control plane label. Do not edit | `edgeless.systems/control-plane-ns` |
| `global.podLabels`                           | Additional labels to add to all pods | `{}` |
| `global.podAnnotations`                      | Additional annotations to add to all pods | `{}`|
| `global.imagePullPolicy`                     | Docker image pull policy | `IfNotPresent` |
| `global.namespace`                           | Control plane namespace | `edg-mesh` |
| `nodeSelector`                               | NodeSelector section, See the [K8S documentation](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/#nodeselector) for more information | `beta.kubernetes.io/os: linux` |
| `tolerations`                                | Tolerations section, See the [K8S documentation](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/) for more information | `{}` |

## Add new version (maintainers)

```bash
helm package coordinator
mv coordinator-x.x.x.tgz stable
helm repo index stable --url https://helm.edgeless.systems/stable
```
