# rstudio

![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square)  ![AppVersion: 3.2.0](https://img.shields.io/badge/AppVersion-3.2.0-informational?style=flat-square)

A Helm chart to deploy RStudio on Kubernetes and OpenShift.
Most images based on rocker can be used, such as: bioconductor/bioconductor_docker:devel
| rocker/rstudio | rocker/tidyverse | ghcr.io/maastrichtu-ids/rstudio

The aim of this Helm chart is to give an easy and straightforward way to deploy RStudio on OpenShift and Kubernetes clusters. The chart is currently mostly optimized and used in OpenShift/OKD clusters, let us know if you are using it with other Kubernetes distributions in the GitHub repository issues, we would love to hear about it!

With this Helm chart you can easily deploy any Docker image based on the popular [RStudio rocker images](https://hub.docker.com/r/rocker/rstudio) as root user, such as:
- ghcr.io/maastrichtu-ids/rstudio:latest
- bioconductor/bioconductor_docker
- rocker/rstudio
- rocker/tidyverse

You can also extend those images to build a custom one with all the packages you need already installed, we recommend you to take a look at the instructions of our custom RStudio image at https://github.com/MaastrichtU-IDS/rstudio

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
  --set serviceAccount.name=anyuid \
  --set service.openshiftRoute.enabled=true \
  --set password=changeme
```

The command deploys rstudio on the OpenShift or Kubernetes cluster in the default configuration.

## Updating the image in a deployed chart

To be able to trigger an update of the image deployed by the chart you will need to set `image.pullPolicy=Always` when deploying the chart.

You can then update the image used by the running RStudio:

```bash
helm upgrade rstudio dsri/rstudio
```

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
| extraEnvs | list | `[]` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.repository | string | `"ghcr.io/maastrichtu-ids/rstudio"` |  |
| image.tag | string | `"latest"` |  |
| imagePullSecrets | list | `[]` |    drop:   - ALL readOnlyRootFilesystem: true runAsNonRoot: true runAsUser: 1000 |
| nodeSelector | object | `{}` |  |
| openblasNumThreads | int | `1` |  Restricting the number of thread allocated to OpenBLAS can speed up computations using OpenBLAS (leave empty for default 64) |
| password | string | `""` |  |
| podAnnotations | object | `{}` |  |
| podSecurityContext | object | `{}` |  |
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
| service.port | int | `8787` |  |
| service.type | string | `"ClusterIP"` |  |
| serviceAccount.annotations | object | `{}` |  |
| serviceAccount.create | bool | `false` |  |
| serviceAccount.name | string | `"anyuid"` |  |
| storage.enabled | bool | `true` |  |
| storage.mountPath | string | `"/home/rstudio"` |  |
| storage.size | string | `"5Gi"` |  |
| tolerations | list | `[]` |  |
| username | string | `"rstudio"` |  |