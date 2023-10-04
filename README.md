# A Kubernetes HELM Chart to add a Traefik IngressRoute for your application

Traefik 2 adds an IngressRoute resource to support defining forwarding for your application. This is not directly equivalent to the Ingress of the past, and therefore doesn't easily insert itself in most helm charts that have an Ingress definition included.  The simple solution however, is to add this either as a standalone chart (it's connecting the dots as most Kubernetes resources do), and as most Traefik systems are setup to support multiple services (simplifying much of the other forwarding decisions), it's easy to just add your route as a part of that service.

## Install this chart

You'll want to configure this chart to map your outbound facing DNS name to your service. If everything resides in the same namespace, you can just define host, path, service name and service port and your off.

You can also include a service target namespace if it differs from where you install this chart.

Create a values.yaml document for your particular app:

```
host: test.example.com
path: /
service:
  name: test
  port: 80
```

And then install from the repository.  *NOTE*: the chart name needs to be different than your app, but the only critical information for forwarding is already included in the values.yaml:

```
helm install ingressroute app-ir --repo https://kumulustech.github.io/ingressroute --values values.yaml
```

## Contributing

Fork and submit a pull request.  We follow the code of conduct outlined in our [Code of Conduct](CODEOFCONDUCT.md) file in the root directory of the repository.
