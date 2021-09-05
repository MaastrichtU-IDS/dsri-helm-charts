# jupyterlab

![Version: 0.1.5](https://img.shields.io/badge/Version-0.1.5-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 1.16.0](https://img.shields.io/badge/AppVersion-1.16.0-informational?style=flat-square)

A Helm chart for JupyterLab on Kubernetes and OpenShift

## Installing the Chart

To install the DSRI Helm Charts, if not already done:

```bash
helm repo add dsri https://maastrichtu-ids.github.io/dsri-helm-charts/
helm repo update
```

## Deploying the Chart

To deploy the chart with the release name `jupyterlab`:

```bash
helm install jupyterlab dsri/jupyterlab \
  --set serviceAccount.name=anyuid,openshiftRoute.enabled=true \
  --set password=changeme
```

The command deploys jupyterlab on the OpenShift or Kubernetes cluster in the default configuration.

## Uninstalling the Chart

To uninstall/delete the `jupyterlab` deployment:

```
helm delete jupyterlab
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following table lists the configurable parameters of the jupyterlab chart and their default values. They can be defined in the `values.yaml` file, or using the flag `--set`.

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` |  |
| gitUrl | string | `""` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.repository | string | `"ghcr.io/maastrichtu-ids/jupyterlab"` |  |
| image.tag | string | `"latest"` |  |
| imagePullSecrets | list | `[]` |  |
| ingress.annotations | object | `{}` |  |
| ingress.enabled | bool | `false` |  |
| ingress.hosts[0].host | string | `"chart-example.local"` |  |
| ingress.hosts[0].paths | list | `[]` |  |
| ingress.tls | list | `[]` |  |
| nodeSelector | object | `{}` |  |
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
| securityContext.runAsUser | int | `0` |  |
| service.port | int | `8888` |  |
| service.type | string | `"ClusterIP"` |  |
| serviceAccount.annotations | object | `{}` |  |
| serviceAccount.create | bool | `false` |  |
| serviceAccount.name | string | `"anyuid"` |  |
| storage.mountPath | string | `"/home/jovyan/work"` |  |
| storage.size | string | `"5Gi"` |  |
| tolerations | list | `[]` |  |# jupyterlab

![Version: 0.1.5](https://img.shields.io/badge/Version-0.1.5-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 1.16.0](https://img.shields.io/badge/AppVersion-1.16.0-informational?style=flat-square)

A Helm chart for JupyterLab on Kubernetes and OpenShift

**Homepage:** <https://github.com/MaastrichtU-IDS/dsri-helm-charts>

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| Vincent Emonet | vincent.emonet@gmail.com |  |

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` |  |
| gitUrl | string | `""` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.repository | string | `"ghcr.io/maastrichtu-ids/jupyterlab"` |  |
| image.tag | string | `"latest"` |  |
| imagePullSecrets | list | `[]` |  |
| ingress.annotations | object | `{}` |  |
| ingress.enabled | bool | `false` |  |
| ingress.hosts[0].host | string | `"chart-example.local"` |  |
| ingress.hosts[0].paths | list | `[]` |  |
| ingress.tls | list | `[]` |  |
| nodeSelector | object | `{}` |  |
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
| securityContext.runAsUser | int | `0` |  |
| service.port | int | `8888` |  |
| service.type | string | `"ClusterIP"` |  |
| serviceAccount.annotations | object | `{}` |  |
| serviceAccount.create | bool | `false` |  |
| serviceAccount.name | string | `"anyuid"` |  |
| storage.mountPath | string | `"/home/jovyan/work"` |  |
| storage.size | string | `"5Gi"` |  |
| tolerations | list | `[]` |  |

