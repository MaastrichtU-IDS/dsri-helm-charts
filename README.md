# DSRI Helm Charts

[![Release Charts](https://github.com/MaastrichtU-IDS/dsri-helm-charts/actions/workflows/release.yml/badge.svg)](https://github.com/MaastrichtU-IDS/dsri-helm-charts/actions/workflows/release.yml) [![Artifact Hub](https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/dsri-helm-charts)](https://artifacthub.io/packages/search?repo=dsri-helm-charts)

Helm charts to easily deploy Data Science workspaces and services on Kubernetes and OpenShift. Developed for the [Data Science Research Infrastructure](https://maastrichtu-ids.github.io/dsri-documentation/) at Maastricht University

Checkout the `charts` folder to browse the charts available: 

* [JupyterLab](https://github.com/MaastrichtU-IDS/dsri-helm-charts/tree/main/charts/jupyterlab)
* [RStudio](https://github.com/MaastrichtU-IDS/dsri-helm-charts/tree/main/charts/rstudio)
* [Generic web app](https://github.com/MaastrichtU-IDS/dsri-helm-charts/tree/main/charts/webapp)

## Install

To deploy charts from the terminal you will need to have `helm` installed on your machine, you can [follow this documentation](https://maastrichtu-ids.github.io/dsri-documentation/docs/helm#install-helm) to install it.

Add the DSRI Helm Charts repository:

```bash
helm repo add dsri https://maastrichtu-ids.github.io/dsri-helm-charts/
helm repo update
```

## Quickstart an application

Quickstart JupyterLab on OpenShift with default settings and using existing `anyuid` service account to run as root:

```bash
helm install jupyterlab dsri/jupyterlab \
  --set serviceAccount.name=anyuid,openshiftRoute.enabled=true \
  --set password=changeme
```

Delete:

```bash
helm uninstall jupyterlab
```

Refer to the `README.md` for each application in the `charts` folder for more details.

## Develop

Lint to check for errors: 

```bash
helm lint charts/jupyterlab
yamllint charts/jupyterlab/templates/deployment.yaml
```

Test a chart without deploying:

```bash
helm install --dry-run --debug ./charts/jupyterlab --set serviceAccount.name=anyuid,openshiftRoute.enabled=true,password=changeme --generate-name
```

Deploy from local source code:

```bash
helm install code-server ./charts/jupyterlab --set serviceAccount.name=anyuid,openshiftRoute.enabled=true,password=changeme
```

Delete:

```bash
helm uninstall jupyterlab
```

Create a new chart:

```bash
helm create charts/your-new-chart
```

### Generate docs

Install [helm-docs](https://github.com/norwoodj/helm-docs) (requires `golang` installed):

```bash
GO111MODULE=on go get github.com/norwoodj/helm-docs/cmd/helm-docs
```

Generate a `README.md` for all charts by running `helm-docs` from the root of the git repository:

```bash
~/go/bin/helm-docs
```

Automatically generate docs when commiting using pre-commit hooks:

```bash
pip install pre-commit
pre-commit install
pre-commit install-hooks
```

## Add charts to your OpenShift Catalog

You can easily add this Helm charts repository to your [OpenShift cluster catalog](https://docs.openshift.com/container-platform/4.6/cli_reference/helm_cli/configuring-custom-helm-chart-repositories.html) if you have admin privileges:

```bash
cat <<EOF | oc apply -f -
apiVersion: helm.openshift.io/v1beta1
kind: HelmChartRepository
metadata:
  name: dsri-helm-charts
spec:
  name: dsri-helm-charts
  connectionConfig:
    url: https://maastrichtu-ids.github.io/dsri-helm-charts/
EOF
```

## Credits

JSON schema generated using https://www.jsonschema.net

Example JSON schema in RedHat Helm chart: https://github.com/redhat-developer/redhat-helm-charts/blob/master/alpha/nodejs-ex-k/values.schema.json

