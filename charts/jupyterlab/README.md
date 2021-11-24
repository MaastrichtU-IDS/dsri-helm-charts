# jupyterlab

![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square)  ![AppVersion: 1.16.0](https://img.shields.io/badge/AppVersion-1.16.0-informational?style=flat-square)

A Helm chart to deploy JupyterLab on CPU and GPU in OpenShift and Kubernetes clusters. Works well with images based on the jupyter/docker-stacks, and images using the root user

> The aim of this Helm chart is to give an easy and straightforward way to deploy JupyterLab on OpenShift and Kubernetes clusters. Currently the chart is mostly optimized and used in OpenShift/OKD clusters, if you are using it with other Kubernetes distributions please let us know  in the [GitHub repository issues](https://github.com/MaastrichtU-IDS/dsri-helm-charts/issues), we would love to hear about it!

With this Helm chart you can deploy any JupyterLab Docker image as root user, including those based on the [official Jupyter docker stack](https://github.com/jupyter/docker-stacks), such as:
- [ghcr.io/maastrichtu-ids/jupyterlab](https://github.com/MaastrichtU-IDS/jupyterlab) (our custom image for Data Science with VisualStudio Code, OpenRefine, conda integration, Python autocomplete, and additional Java and SPARQL kernels)
- [jupyter/minimal-notebook](https://github.com/jupyter/docker-stacks/tree/master/base-notebook)
- jupyter/scipy-notebook
- jupyter/datascience-notebook (with Julia kernel)
- jupyter/tensorflow-notebook
- jupyter/r-notebook
- jupyter/pyspark-notebook
- jupyter/all-spark-notebook

You can also extend those images to build a custom one with all the packages you need already installed, we recommend you to take a look at the instructions of our custom JupyterLab image at https://github.com/MaastrichtU-IDS/jupyterlab

## Installing the Chart

Install the DSRI Helm Charts on your machine, if not already done:

```bash
helm repo add dsri https://maastrichtu-ids.github.io/dsri-helm-charts/
helm repo update
```

## Deploying the Chart

To deploy the chart **on CPU** with the release name `jupyterlab` using the existing `anyuid` service account:

```bash
helm install jupyterlab dsri/jupyterlab \
  --set serviceAccount.name=anyuid \
  --set service.openshiftRoute.enabled=true \
  --set image.repository=ghcr.io/maastrichtu-ids/jupyterlab \
  --set image.tag=latest \
  --set storage.mountPath=/home/jovyan/work \
  --set password=changeme
```

You can also automatically clone a Git repository in the workspace by adding this to the previous command:

```bash
  --set gitUrl=https://github.com/MaastrichtU-IDS/dsri-demo
```

If you are not using a `ghcr.io/maastrichtu-ids/jupyterlab` image, you will need to also enable the `jupyter_notebook_config.py`:

```bash
  --set image.addJupyterConfig=true
```

You can also use this chart to deploy JupyterLab **on GPU** with the release name `jupyterlab-gpu` using the existing `anyuid` service account:

```bash
helm install jupyterlab-gpu dsri/jupyterlab \
  --set serviceAccount.name=anyuid \
  --set service.openshiftRoute.enabled=true \
  --set image.repository=ghcr.io/maastrichtu-ids/jupyterlab \
  --set image.tag=tensorflow \
  --set storage.mountPath=/workspace \
  --set resources.requests."nvidia\.com/gpu"=1 \
  --set resources.limits."nvidia\.com/gpu"=1 \
  --set password=changeme
```

If you deployed your application with an OpenShift Route, you can retrieve the URL of the deloyed application with this command, after changing `jupyterlab` by your application name:

```bash
echo https://$(oc get route --selector app.kubernetes.io/instance=jupyterlab --no-headers -o=custom-columns=HOST:.spec.host)
```

## Checking the logs

Get the events related to your chart deployment (replace oc by `kubectl` for Kubernetes):

```bash
oc get events | grep jupyterlab
```

Get logs of the chart deployment:

```bash
oc logs deployment/jupyterlab --tail 100
```

## Updating the image in a deployed chart

To be able to trigger an update of the image deployed by the chart you will need to set `image.pullPolicy=Always` when deploying the chart.

You can then update the image used by the running JupyterLab:

```bash
helm upgrade jupyterlab dsri/jupyterlab
```

## Uninstalling the Chart

To uninstall/delete the `jupyterlab` deployment:

```bash
helm delete jupyterlab
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following table lists the configurable parameters of the jupyterlab chart and their default values. They can be defined in the `values.yaml` file, or using the flag `--set`.

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` |  |
| extraEnvs | list | `[]` |  |
| gitEmail | string | `"default@maastrichtuniversity.nl"` |  |
| gitName | string | `"Default user"` |  |
| gitUrl | string | `""` |  |
| image.addJupyterConfig | bool | `false` |  |
| image.command | list | `[]` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.repository | string | `"ghcr.io/maastrichtu-ids/jupyterlab"` |  |
| image.tag | string | `"latest"` |  |
| imagePullSecrets | list | `[]` |  |
| nodeSelector | object | `{}` |  |
| password | string | `""` |  |
| podAnnotations | object | `{}` |  |
| podSecurityContext | object | `{}` |  |
| resources | object | `{}` |  |
| securityContext.runAsUser | int | `0` |  |
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
| service.port | int | `8888` |  |
| service.type | string | `"ClusterIP"` |  |
| serviceAccount.annotations | object | `{}` |  |
| serviceAccount.create | bool | `false` |  |
| serviceAccount.name | string | `"anyuid"` |  |
| storage.enabled | bool | `true` |  |
| storage.extraStorage | list | `[]` |  |
| storage.mountPath | string | `"/home/jovyan/work"` |  |
| storage.size | string | `"5Gi"` |  |
| storage.workingDir | string | `""` |  |
| tolerations | list | `[]` |  |