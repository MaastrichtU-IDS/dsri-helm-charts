# rstudio

![Version: 0.1.3](https://img.shields.io/badge/Version-0.1.3-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 3.2.0](https://img.shields.io/badge/AppVersion-3.2.0-informational?style=flat-square)

A Helm chart to deploy RStudio on Kubernetes and OpenShift.
Most images based on rocker can be used, such as: bioconductor/bioconductor_docker:devel
| rocker/rstudio | rocker/tidyverse | ghcr.io/maastrichtu-ids/rstudio

## Installing the Chart

To install the DSRI Helm Charts, if not already done:

```bash
helm repo add dsri https://maastrichtu-ids.github.io/dsri-helm-charts/
helm repo update
```

## Deploying the Chart

To deploy the chart with the release name `rstudio`:

```bash
helm install rstudio dsri/rstudio \
  --set serviceAccount.name=anyuid,openshiftRoute.enabled=true \
  --set password=changeme
```

The command deploys rstudio on the OpenShift or Kubernetes cluster in the default configuration.

## Uninstalling the Chart

To uninstall/delete the `rstudio` deployment:

```
helm delete rstudio
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following table lists the configurable parameters of the rstudio chart and their default values. They can be defined in the `values.yaml` file, or using the flag `--set`.

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.repository | string | `"ghcr.io/maastrichtu-ids/rstudio"` |  |
| image.tag | string | `"latest"` |  |
| imagePullSecrets | list | `[]` |    drop:   - ALL readOnlyRootFilesystem: true runAsNonRoot: true runAsUser: 1000 |
| ingress.annotations | object | `{}` |  |
| ingress.enabled | bool | `false` |  |
| ingress.hosts[0].host | string | `"chart-example.local"` |  |
| ingress.hosts[0].paths | list | `[]` |  |
| ingress.tls | list | `[]` |  |
| nodeSelector | object | `{}` |  |
| openblasNumThreads | string | `"1"` |  Restricting the number of thread allocated to OpenBLAS can speed up computations using OpenBLAS (leave empty for default 64) |
| openshiftRoute.enabled | bool | `true` |  |
| openshiftRoute.host | string | `""` |  |
| openshiftRoute.path | string | `""` |  |
| openshiftRoute.tls.enabled | bool | `true` |  |
| openshiftRoute.tls.insecureEdgeTerminationPolicy | string | `"Redirect"` |  |
| openshiftRoute.tls.termination | string | `"edge"` |  |
| openshiftRoute.wildcardPolicy | string | `"None"` |  |
| password | string | `""` |  |
| podAnnotations | object | `{}` |  |
| podSecurityContext | object | `{}` |  |
| resources | object | `{}` |  |
| securityContext | object | `{}` |  |
| service.port | int | `8787` |  |
| service.type | string | `"ClusterIP"` |  |
| serviceAccount.annotations | object | `{}` |  |
| serviceAccount.create | bool | `false` |  |
| serviceAccount.name | string | `"anyuid"` |  |
| storage.mountPath | string | `"/home/rstudio"` |  |
| storage.size | string | `"5Gi"` |  |
| tolerations | list | `[]` |  |
| username | string | `"rstudio"` |  |# rstudio

![Version: 0.1.3](https://img.shields.io/badge/Version-0.1.3-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 3.2.0](https://img.shields.io/badge/AppVersion-3.2.0-informational?style=flat-square)

A Helm chart to deploy RStudio on Kubernetes and OpenShift.
Most images based on rocker can be used, such as: bioconductor/bioconductor_docker:devel
| rocker/rstudio | rocker/tidyverse | ghcr.io/maastrichtu-ids/rstudio

**Homepage:** <https://github.com/MaastrichtU-IDS/dsri-helm-charts>

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| Vincent Emonet | vincent.emonet@gmail.com |  |

## Source Code

* <https://github.com/MaastrichtU-IDS/dsri-helm-charts>

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.repository | string | `"ghcr.io/maastrichtu-ids/rstudio"` |  |
| image.tag | string | `"latest"` |  |
| imagePullSecrets | list | `[]` |    drop:   - ALL readOnlyRootFilesystem: true runAsNonRoot: true runAsUser: 1000 |
| ingress.annotations | object | `{}` |  |
| ingress.enabled | bool | `false` |  |
| ingress.hosts[0].host | string | `"chart-example.local"` |  |
| ingress.hosts[0].paths | list | `[]` |  |
| ingress.tls | list | `[]` |  |
| nodeSelector | object | `{}` |  |
| openblasNumThreads | string | `"1"` |  Restricting the number of thread allocated to OpenBLAS can speed up computations using OpenBLAS (leave empty for default 64) |
| openshiftRoute.enabled | bool | `true` |  |
| openshiftRoute.host | string | `""` |  |
| openshiftRoute.path | string | `""` |  |
| openshiftRoute.tls.enabled | bool | `true` |  |
| openshiftRoute.tls.insecureEdgeTerminationPolicy | string | `"Redirect"` |  |
| openshiftRoute.tls.termination | string | `"edge"` |  |
| openshiftRoute.wildcardPolicy | string | `"None"` |  |
| password | string | `""` |  |
| podAnnotations | object | `{}` |  |
| podSecurityContext | object | `{}` |  |
| resources | object | `{}` |  |
| securityContext | object | `{}` |  |
| service.port | int | `8787` |  |
| service.type | string | `"ClusterIP"` |  |
| serviceAccount.annotations | object | `{}` |  |
| serviceAccount.create | bool | `false` |  |
| serviceAccount.name | string | `"anyuid"` |  |
| storage.mountPath | string | `"/home/rstudio"` |  |
| storage.size | string | `"5Gi"` |  |
| tolerations | list | `[]` |  |
| username | string | `"rstudio"` |  |

