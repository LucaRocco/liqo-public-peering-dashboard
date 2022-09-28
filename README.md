
# Liqo peering dashboard

Liqo peering dashboard is an open-source dashboard that shows you the status of peerings enabled by the cluster and the number of resources in terms of vCPUs and Memory used by each liqo peer.

## Prerequisites

Since the dashboard shows data related to Liqo you must have it installed in your cluster. If you want to start using Liqo you can check the [doc](https://docs.liqo.io/en/stable/) and the [quick start tutorial](https://docs.liqo.io/en/stable/examples/quick-start.html)

To install this dashboard you should have helm installed on your machine. You can find more about helm on the [official site](https://helm.sh/). You can also decide to avoid helm but in this case, you need to write down all the required YAML manifests.

Additionally, this dashboard can be deployed in a cluster that has an ingress controller installed. To learn more about ingress controller you can read the [official Kubernetes documentation](https://kubernetes.io/docs/concepts/services-networking/ingress-controllers/)

## Deployment

The dashboard runs divided into two different pods although you don't need to care about it since you can use a simple helm command:

```bash
helm install liqo-dashboard ./chart
```

The command above deploys a few resources into the cluster in the liqo-dashboard namespace.

When the dashboard is deployed on a production environment you should set the host using the following command otherwise the dashboard's ingress will catch every host because by default the ingress listens on `*` wildcard.

```bash
helm install liqo-dashboard --set host=<<host_here>> ./chart
```

Additionally, if you want to use TLS encryption to enable HTTPS you should set tls.secretName as follows
```bash
helm install liqo-dashboard --set host=<<host_here>> --tls.secretName=<<certificate_secret_here>> ./chart
```

You can find the complete list of additional values [here](./chart/README.md)

## Contributing

All contributors are excitedly welcome. If you notice a bug you can open an issue to let us know or you can figure out how to fix it and open a pull request. Inside [client](./client/README.md)[ readme](./client/README.md) and [server readme](./server/README.md) you can find all the information you need to start coding on your machine and run the application locally.
