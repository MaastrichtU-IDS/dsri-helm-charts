# webapp

![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square)  ![AppVersion: 1.16.0](https://img.shields.io/badge/AppVersion-1.16.0-informational?style=flat-square)

A generic reuseable Helm chart for deploying almost any dockerized application exposing a web interface to a HTTPS route on OpenShift and Kubernetes

## Installing the Chart

To install the DSRI Helm Charts, if not already done:

```bash
helm repo add dsri https://maastrichtu-ids.github.io/dsri-helm-charts/
helm repo update
```

## Deploying the Chart

To deploy the chart with the release name `webapp`:

```bash
helm install webapp dsri/webapp \
  --set serviceAccount.name=anyuid \
  --set service.openshiftRoute.enabled=true \
  --set service.port=80
```

The command deploys webapp on the OpenShift or Kubernetes cluster in the default configuration.

## Updating the image in a deployed chart

To be able to trigger an update of the image deployed by the chart you will need to set `image.pullPolicy=Always` when deploying the chart.

Then you can update the image in the running JupyterLab:

```bash
helm upgrade webapp dsri/webapp
```

## Uninstalling the Chart

To uninstall/delete the `webapp` deployment:

```
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
| service.port | int | `8080` |  |
| service.type | string | `"ClusterIP"` |  |
| serviceAccount.annotations | object | `{}` |  |
| serviceAccount.create | bool | `false` |  |
| serviceAccount.ingress.annotations | object | `{}` |  |
| serviceAccount.ingress.enabled | bool | `false` |  |
| serviceAccount.ingress.hosts[0].host | string | `"chart-example.local"` |  |
| serviceAccount.ingress.hosts[0].paths | list | `[]` |  |
| serviceAccount.ingress.tls | list | `[]` |  |
| serviceAccount.name | string | `"anyuid"` |  |
| serviceAccount.openshiftRoute.enabled | bool | `true` |  |
| serviceAccount.openshiftRoute.host | string | `""` |  |
| serviceAccount.openshiftRoute.path | string | `""` |  |
| serviceAccount.openshiftRoute.tls.enabled | bool | `true` |  |
| serviceAccount.openshiftRoute.tls.insecureEdgeTerminationPolicy | string | `"Redirect"` |  |
| serviceAccount.openshiftRoute.tls.termination | string | `"edge"` |  |
| serviceAccount.openshiftRoute.wildcardPolicy | string | `"None"` |  |
| storage.enabled | bool | `true` |  |
| storage.mountPath | string | `"/home/coder/project"` |  |
| storage.size | string | `"5Gi"` |  |
| tolerations | list | `[]` |  |