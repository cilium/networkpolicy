# Tutorial: Allow Egress To Pod

If you come from a traditional Networking background, it might be tempting to use a /32 CIDR rule to allow traffic to the IP address of a Pod as shown in the output of kubectl describe pod. For example:

```yaml
  egress:
    - to:
        - ipBlock:
            cidr: 10.0.2.125/32
```


However, Pod IPs are ephemeral and unpredictable, and depending on a network plugin implementation, ipBlock rules might only allow egress traffic to destinations outside of a cluster. [Kubernetes documentation](https://kubernetes.io/docs/concepts/services-networking/network-policies/#behavior-of-to-and-from-selectors) recommends using ipBlocks only for IP addresses outside of your cluster.

Instead of using ipBlock, use podSelector and namespaceSelector to:

* Allow egress traffic to only certain pods
* Allow all egress traffic within same namespace
* Allow all egress traffic within cluster

Use Network Policy Editor and click on [+] in the relevant box: In Cluster, In Same Namespace for ingress or egress. 