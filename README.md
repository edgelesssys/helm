# Edgeless Mesh Helm Chart

Edgeless Mesh is the service mesh for the age of confidential computing.

## Quickstart and documentation

See the [Getting Started Guide](TODO) to set up a distributed confidential-computing app in a few simple steps. 
For more comprehensive documentation, start with the [docs](TODO).

## Adding Edgeless Mesh's Helm repository

```bash
helm repo add edg-mesh https://helm.edgeless.systems/stable
helm repo update
```

## Installing the chart

* If your deploying on a cluster with nodes that support SGX1+FLC (e.g. AKS or minikube + Azure Standard_DC*s)

```bash
helm install  edg-mesh-coordinator edg-mesh/coordinator --create-namespace edg-mesh
```

* Otherwise

```bash
helm install edg-mesh-coordinator edg-mesh/coordinator --create-namespace edg-mesh --set coordinator.resources=null --set coordinator.OE_SIMULATION=1 --set tolerations=null

## Configuration


## Update the chart repository

```bash
helm package coordinator
mv coordinator-x.x.x.tgz docs
helm repo index docs --url https://helm.edgless.systems
```
