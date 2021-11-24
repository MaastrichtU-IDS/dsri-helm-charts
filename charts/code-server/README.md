# code-server

![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square)  ![AppVersion: 1.16.0](https://img.shields.io/badge/AppVersion-1.16.0-informational?style=flat-square)

A Helm chart to deploy VisualStudio Code server on Kubernetes and OpenShift

## Installing the Chart

To install the DSRI Helm Charts, if not already done:

```bash
helm repo add dsri https://maastrichtu-ids.github.io/dsri-helm-charts/
helm repo update
```

## Deploying the Chart

To deploy the chart with the release name `code-server`:

```bash
helm install code-server dsri/code-server \
  --set serviceAccount.name=anyuid \
  --set openshiftRoute.enabled=true \
  --set password=changeme
```

The command deploys code-server on the OpenShift or Kubernetes cluster in the default configuration.

## Uninstalling the Chart

To uninstall/delete the `code-server` deployment:

```
helm delete code-server
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following table lists the configurable parameters of the code-server chart and their default values. They can be defined in the `values.yaml` file, or using the flag `--set`.

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` |  |
| extraEnvs | list | `[]` |  |
| gitUrl | string | `""` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.repository | string | `"ghcr.io/maastrichtu-ids/code-server"` |  |
| image.tag | string | `"latest"` |  |
| imagePullSecrets | list | `[]` |    drop:   - ALL readOnlyRootFilesystem: true runAsNonRoot: true runAsUser: 1000 |
| ingress.annotations | object | `{}` |  |
| ingress.enabled | bool | `false` |  |
| ingress.openshiftHost.clusterUrl | string | `"apps.dsri2.unimaas.nl"` |  |
| ingress.openshiftHost.project | string | `"workspace-vemonet"` |  |
| ingress.tls | list | `[]` |    - host: "code-server-workspace-vemonet.apps.dsri2.unimaas.nl"     paths: ["/"] |
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
| securityContext | object | `{}` |  |
| service.port | int | `8080` |  |
| service.type | string | `"ClusterIP"` |  |
| serviceAccount.annotations | object | `{}` |  |
| serviceAccount.create | bool | `false` |  |
| serviceAccount.name | string | `"anyuid"` |  |
| storage.enabled | bool | `true` |  |
| storage.mountPath | string | `"/home/coder/project"` |  |
| storage.size | string | `"5Gi"` |  |
| tolerations | list | `[]` |  |