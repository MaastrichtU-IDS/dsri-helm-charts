# webapp

![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square)  ![AppVersion: 1.16.0](https://img.shields.io/badge/AppVersion-1.16.0-informational?style=flat-square)

A generic reuseable Helm chart for deploying almost any dockerized application exposing a web interface to a HTTPS route on OpenShift and Kubernetes

> The aim of this Helm chart is to give an easy and straightforward way to deploy any Docker image exposing a web interface on OpenShift and Kubernetes clusters. Currently the chart is mostly optimized and used in OpenShift/OKD clusters, if you are using it with other Kubernetes distributions please let us know  in the [GitHub repository issues](https://github.com/MaastrichtU-IDS/dsri-helm-charts/issues), we would love to hear about it!

## Installing the Chart

Install the DSRI Helm Charts on your machine, if not already done:

```bash
helm repo add dsri https://maastrichtu-ids.github.io/dsri-helm-charts/
helm repo update
```

> Visit the [dsri-helm-charts GitHub repository](https://github.com/MaastrichtU-IDS/dsri-helm-charts) for more details on how to develop and tests the charts, feel free to send us pull requests to propose your improvements!

## Deploying the Chart

To deploy the chart with the release name `webapp`, here is an example to deploy VisualStudio Code server:

```bash
helm install webapp dsri/webapp \
  --set serviceAccount.name=anyuid \
  --set service.openshiftRoute.enabled=true \
  --set service.port=8080 \
  --set image.repository=ghcr.io/maastrichtu-ids/code-server \
  --set image.tag=latest \
  --set storage.mountPath=/home/coder/project \
  --set extraEnvs[0].name=PASSWORD \
  --set extraEnvs[0].value=changeme
```

## Updating the image in a deployed chart

To be able to trigger an update of the image deployed by the chart you will need to set `image.pullPolicy=Always` when deploying the chart.

You can then update the image used by the running webapp:

```bash
helm upgrade webapp dsri/webapp
```

## Uninstalling the Chart

To uninstall/delete the `webapp` deployment:

```bash
helm delete webapp
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following table lists the configurable parameters of the webapp chart and their default values. They can be defined in the `values.yaml` file, or using the flag `--set`.

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` |  |
| autoscaling.enabled | bool | `false` |  |
| extraEnvs | list | `[]` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.repository | string | `"ghcr.io/maastrichtu-ids/code-server"` |  |
| image.tag | string | `"latest"` |  |
| imagePullSecrets | list | `[]` |    drop:   - ALL readOnlyRootFilesystem: true runAsNonRoot: true runAsUser: 1000 |
| nodeSelector | object | `{}` |  |
| podAnnotations | object | `{}` |  |
| podSecurityContext | object | `{}` |  |
| replicaCount | int | `1` |  |
| resources | object | `{}` |  |
| securityContext | object | `{}` |  |
| service.ingress.annotations | object | `{}` |  |
| service.ingress.enabled | bool | `false` |  |
| service.ingress.hosts[0].host | string | `"chart-example.local"` |  |
| service.ingress.hosts[0].paths | list | `[]` |  |
| service.ingress.tls | list | `[]` |  |
| service.openshiftRoute.enabled | bool | `true` |  |
| service.openshiftRoute.host | string | `""` |  |
| service.openshiftRoute.path | string | `""` |  |
| service.openshiftRoute.tls.enabled | bool | `true` |  |
| service.openshiftRoute.tls.insecureEdgeTerminationPolicy | string | `"Redirect"` |  |
| service.openshiftRoute.tls.termination | string | `"edge"` |  |
| service.openshiftRoute.wildcardPolicy | string | `"None"` |  |
| service.port | int | `8080` |  |
| service.type | string | `"ClusterIP"` |  |
| serviceAccount.annotations | object | `{}` |  |
| serviceAccount.create | bool | `false` |  |
| serviceAccount.name | string | `"anyuid"` |  |
| storage.enabled | bool | `true` |  |
| storage.mountPath | string | `"/home/coder/project"` |  |
| storage.size | string | `"5Gi"` |  |
| tolerations | list | `[]` |  |