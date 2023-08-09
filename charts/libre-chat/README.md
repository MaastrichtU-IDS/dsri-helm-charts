# libre-chat

![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square)  ![AppVersion: 0.0.6](https://img.shields.io/badge/AppVersion-0.0.6-informational?style=flat-square)

A Helm chart to deploy JupyterLab on CPU and GPU in OpenShift and Kubernetes clusters. Works well with images based on the jupyter/docker-stacks, and images using the root user

A Helm chart to deploy a free and completely Open Source chatbot web service with UI and API on CPU or GPU.

Visit the Libre Chat documentation website for more details on how to configure it: [vemonet.github.io/libre-chat](https://vemonet.github.io/libre-chat)

We recommend to use a `values.yml` file that you pass to `helm install` to configure the chatbot. Start from the default `values.yaml` file in this repository.

## Installing the Chart

Install the DSRI Helm Charts on your machine, if not already done:

```bash
helm repo add dsri https://maastrichtu-ids.github.io/dsri-helm-charts/
helm repo update
```

## Deploying the Chart

### On CPU

To deploy the chart **on CPU** with the release name `libre-chat` using a `values.yml` file:

```bash
helm install libre-chat dsri/libre-chat -f values.yml
```

<!--
### On GPU

You can also use this chart to deploy JupyterLab **on GPU**, here is an example with the release name `libre-chat-gpu`, using the existing `anyuid` service account, and our custom [`ghcr.io/vemonet/libre-chat:gpu` image:

```bash
helm install libre-chat-gpu dsri/libre-chat \
  -f values.yml \
  --set service.openshiftRoute.enabled=true \
  --set image.repository=ghcr.io/vemonet/libre-chat \
  --set image.tag=gpu \
  --set image.pullPolicy=Always \
  --set resources.requests."nvidia\.com/gpu"=1 \
  --set resources.limits."nvidia\.com/gpu"=1 \
  --set tolerations[0].effect=NoSchedule \
  --set tolerations[0].key=nvidia.com/gpu \
  --set tolerations[0].operator=Exists \
  --set password=changeme
```
-->

You can add an additional existing volume easily:

```bash
  --set storage.extraStorage[0].name=scratch-storage \
  --set storage.extraStorage[0].mountPath=/workspace/scratch \
  --set storage.extraStorage[0].readOnly=false \
```

If you deployed your application with an OpenShift Route, you can retrieve the URL of the deloyed application with this command, after changing `libre-chat` by your application name:

```bash
oc get route --selector app.kubernetes.io/instance=libre-chat --no-headers -o=custom-columns=HOST:.spec.host
```

## Checking the logs

Get the events related to your chart deployment (replace `oc` by `kubectl` for Kubernetes):

```bash
oc get events | grep libre-chat
```

Get logs of the chart deployment:

```bash
oc logs deployment/libre-chat --tail 100
```

## Updating the image in a deployed chart

To be able to trigger an update of the image deployed by the chart you will need to set `image.pullPolicy=Always` when deploying the chart.

You can then update the image used by the running JupyterLab:

```bash
helm upgrade libre-chat dsri/libre-chat
```

## Uninstalling the Chart

To uninstall/delete the `libre-chat` deployment:

```bash
helm delete libre-chat
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following table lists the configurable parameters of the libre-chat chart and their default values. They can be defined in the `values.yaml` file, or using the flag `--set`.

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` |  |
| chatConf.info.contact.email | string | `"vincent.emonet@gmail.com"` |  |
| chatConf.info.contact.name | string | `"Vincent Emonet"` |  |
| chatConf.info.description | string | `"Open source and free question-answering chatbot powered by [LangChain](https://python.langchain.com) and [Llama 2](https://ai.meta.com/llama) [7B](https://huggingface.co/TheBloke/Llama-2-7B-Chat-GGML)\n"` |  |
| chatConf.info.examples[0] | string | `"What is the capital of the Netherlands?"` |  |
| chatConf.info.examples[1] | string | `"Which drugs are approved by the FDA to mitigate Alzheimer symptoms?"` |  |
| chatConf.info.examples[2] | string | `"What was the GDP of France in 1998?"` |  |
| chatConf.info.favicon | string | `"https://raw.github.com/vemonet/libre-chat/main/docs/docs/assets/logo.png"` |  |
| chatConf.info.license_info.name | string | `"MIT license"` |  |
| chatConf.info.license_info.url | string | `"https://raw.github.com/vemonet/libre-chat/main/LICENSE.txt"` |  |
| chatConf.info.public_url | string | `"https://chat.semanticscience.org"` |  |
| chatConf.info.repository_url | string | `"https://github.com/vemonet/libre-chat"` |  |
| chatConf.info.title | string | `"Libre Chat"` |  |
| chatConf.info.version | string | `"0.1.0"` |  |
| chatConf.info.workers | int | `4` |  |
| chatConf.llm.max_new_tokens | int | `1024` |  |
| chatConf.llm.model_download | string | `"https://huggingface.co/TheBloke/Llama-2-7B-Chat-GGML/resolve/main/llama-2-7b-chat.ggmlv3.q3_K_L.bin"` |  |
| chatConf.llm.model_path | string | `"./models/llama-2-7b-chat.ggmlv3.q3_K_L.bin"` |  |
| chatConf.llm.model_type | string | `"llama"` |  |
| chatConf.llm.temperature | float | `0.01` |  |
| chatConf.prompt.template | string | `"Use the following pieces of information to answer the user's question.\nIf you don't know the answer, just say that you don't know, don't try to make up an answer.\n\nContext: {context}\nQuestion: {question}\n\nOnly return the helpful answer below and nothing else.\nHelpful answer:\n"` |  |
| chatConf.prompt.variables[0] | string | `"question"` |  |
| chatConf.prompt.variables[1] | string | `"context"` |  |
| chatConf.vector.chain_type | string | `"stuff"` |  |
| chatConf.vector.chunk_overlap | int | `50` |  |
| chatConf.vector.chunk_size | int | `500` |  |
| chatConf.vector.documents_path | string | `"./documents"` |  |
| chatConf.vector.embeddings_download | string | `"https://public.ukp.informatik.tu-darmstadt.de/reimers/sentence-transformers/v0.2/all-MiniLM-L6-v2.zip"` |  |
| chatConf.vector.embeddings_path | string | `"./embeddings/all-MiniLM-L6-v2"` |  |
| chatConf.vector.return_sources_count | int | `2` |  |
| chatConf.vector.score_threshold | string | `nil` |  |
| chatConf.vector.search_type | string | `"similarity"` |  |
| chatConf.vector.vector_download | string | `nil` |  |
| chatConf.vector.vector_path | string | `"./vectorstore/db_faiss"` |  |
| extraEnvs | list | `[]` |  |
| image.command | list | `[]` |  |
| image.pullPolicy | string | `"Always"` |  |
| image.repository | string | `"ghcr.io/maastrichtu-ids/libre-chat"` |  |
| image.tag | string | `"main"` |  |
| imagePullSecrets | list | `[]` |  |
| nodeSelector | object | `{}` |  |
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
| service.port | int | `8000` |  |
| service.type | string | `"ClusterIP"` |  |
| serviceAccount.annotations | object | `{}` |  |
| serviceAccount.create | bool | `false` |  |
| serviceAccount.name | string | `"anyuid"` |  |
| storage.enableDshm | bool | `true` |  |
| storage.enabled | bool | `true` |  |
| storage.extraStorage | list | `[]` |  |
| storage.mountPath | string | `"/data"` |  |
| storage.size | string | `"10Gi"` |  |
| storage.workingDir | string | `"/data"` |  |
| tolerations | list | `[]` |  |