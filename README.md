Create chart:

```bash
helm create charts/code-server
```

Lint: 

```bash
helm lint charts/code-server
```

Test:

```bash
helm install --dry-run --debug ./charts/code-server --set service.internalPort=8080 --generate-name
```

Deploy:

```bash
helm install code-server ./charts/code-server --set serviceAccount.name=anyuid,openshiftRoute.enabled=true,password=changeme
```

Delete:

```bash
helm uninstall code-server
```

