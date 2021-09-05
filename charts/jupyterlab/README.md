# jupyterlab

![Version: 0.1.4](https://img.shields.io/badge/Version-0.1.4-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 1.16.0](https://img.shields.io/badge/AppVersion-1.16.0-informational?style=flat-square)

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

