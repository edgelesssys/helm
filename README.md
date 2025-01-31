# Helm chart repository for the Edgeless Systems organization

```sh
helm repo add edgeless https://helm.edgeless.systems/stable
helm repo update
```

## MarbleRun

[edgeless/marblerun](https://github.com/edgelesssys/marblerun/tree/master/charts)

```sh
helm install marblerun edgeless/marblerun \
    --create-namespace \
    -n marblerun
```

## EdgelessDB

[edgeless/edgelessdb](https://github.com/edgelesssys/edgelessdb/tree/main/charts)

```sh
helm install edgelessdb edgeless/edgelessdb \
    --create-namespace \
    -n edb
```

## Constellation S3 proxy

[edgeless/s3proxy](https://github.com/edgelesssys/constellation/tree/main/s3proxy/deploy/s3proxy)

```sh
helm install s3proxy edgeless/s3proxy \
    --create-namespace \
    -n s3proxy \
    --set awsAccessKeyID="$ACCESS_KEY" \
    --set awsSecretAccessKey="$ACCESS_SECRET"
```

## Privatemode-proxy

[privatemode-proxy](https://docs.privatemode.ai/guides/proxy-configuration)

```sh
helm install privatemode-proxy edgeless/privatemode-proxy \
    --create-namespace \
    -n privatemode-proxy
```


## Continuum-proxy (legacy)

Please use the `Privatemode-proxy` starting with v1.6.

[continuum-proxy](https://docs.privatemode.ai/1.5/guides/proxy-configuration)

```sh
helm install continuum-proxy edgeless/continuum-proxy \
    --create-namespace \
    -n continuum-proxy
```
