# DSRI Helm charts

[![Release Charts](https://github.com/MaastrichtU-IDS/dsri-helm-charts/actions/workflows/release.yml/badge.svg)](https://github.com/MaastrichtU-IDS/dsri-helm-charts/actions/workflows/release.yml)

Helm charts for the Data Science Research Infrastructure at Maastricht University

* VisualStudio Code server
* JupyterLab

## Install

Add the Helm repository:

```bash
helm repo add dsri https://maastrichtu-ids.github.io/dsri-helm-charts/
helm repo update
```

## Start applications

Start VisualStudio Code server:

```bash
helm install code-server dsri/code-server --set serviceAccount.name=anyuid,openshiftRoute.enabled=true,password=changeme
```

Delete:

```bash
helm uninstall code-server
```

## Develop

Create a chart:

```bash
helm create charts/code-server
```

Lint to check for errors: 

```bash
helm lint charts/code-server
```

Test a chart without deploying:

```bash
helm install --dry-run --debug ./charts/code-server --set service.internalPort=8080 --generate-name
```

Deploy from local source code:

```bash
helm install code-server ./charts/code-server --set serviceAccount.name=anyuid,openshiftRoute.enabled=true,password=changeme
```

Delete:

```bash
helm uninstall code-server
```

Generate JSON schema file for `values.yaml` using https://jsonformatter.org/yaml-to-jsonschema
