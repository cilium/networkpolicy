# Tutorial: Allow Cross Namespace Traffic

Consider a scenario where we want a centralized Prometheus instance running in a monitoring namespace to be able to scrape metrics from a Redis Pod running in the default namespace. Take a look at the following network policy, which is applied in the default namespace. It allows Pods with label app=prometheus to scrape metrics from Pods with label `app=redis`:

A common mistake could be to just create an ingress rule with a podSelector, as shown in the current policy. However, as you can see in the visualization, this network policy only allows ingress traffic from `app=prometheus` from `default` namespace. In order to create a cross-namespace allow rule, you must add `namespaceSelector: {}`. 

## Use the editor to create a network policy rule with `namespaceSelector: {}

1. Click on the [+] icon inside **In Cluster** box and choose `from podSelector` option.

2. Enter required values in in the popup window

> Note: Kubernetes NetworkPolicy namespaceSelector doesn't allow the use of namespace's `name` to select a specific namespace, instead you should label your namespaces accordingly for the network policy to take effect. If you need to select namespace by name, consider using **CiliumNetworkPolicy**.



