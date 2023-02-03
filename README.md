This repository has a working example of how the Datadog MutatingAdmissionWebhook works. 

The examples are explained in [this blog post in detail](https://arapulido.github.io/blog/2023/02/03/datadog-admission-controller/).

# Environment setting
## Create cluster
The `kind-cluster/cluster.yaml` files creates a kind cluster mapping the `30000` port of your local machine to the `30000` port of the node. 

```
kind create cluster --config kind-cluster/cluster.yaml
```

## Deploy Datadog

```
export DD_API_KEY=<YOUR_DATADOG_API_KEY>
helm install datadog --set datadog.apiKey=$DD_API_KEY datadog/datadog -f datadog/values.yaml
```

# Examples

## Basic Mutation (`basic-mutation` folder)

In this example the MutatingAdmissionWebhook just injects several environment variables.

```
kubectl apply -f ecommerce/basic-mutation
```

## Library Injection (`library-injection` folder)

In this example the MutatingAdmissionWebhook injects and configures the Python autoinstrumentation libraries for the `advertisements` and `discounts` deployments.

```
kubectl apply -f ecommerce/library-injection
```
