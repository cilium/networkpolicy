# Tutorial: Allow Egress To Kubernetes DNS

The Pods will likely want to resolve DNS queries on port 53/UDP. For example, when Pod is trying to resolve Service IP by Service Name, or when resolving IPs of external resources by domain names.

However, once you start enforcing egress network policy rules, egress traffic is going to be dropped by default, unless it's explicitly allowed by a network policy rule. That is a common mistake to make, and it's easy to forget about a need to allow egress traffic to Kubernetes DNS.

Let’s say you created a NetworkPolicy to prevent your Pods from the `default` namespace from sending traffic anywhere except to Pods in the same `default` namespace The Network Policy Editor was preloaded with an example of such a network policy.

After deploying this network policy all DNS queries to `kube-dns` in `kube-system` namespace will fail. 


### Use Network Policy Editor To Fix It

1. Click on **Kubernetes DNS** on the right side of the visualization

2. Click the **Allow rule** button

The following network policy egress rule will be added to the policy:

```yaml
 - to:
        - namespaceSelector: {}
          podSelector:
            matchLabels:
              k8s-app: kube-dns
      ports:
        - port: 53
          protocol: UDP
```


> Note: The rule explicitly allows DNS queries only to Kubernetes DNS, it does **NOT** allow egress DNS traffic to DNS servers outside of Kubernetes. This is the recommended approach to prevent DNS data exfiltration attacks.