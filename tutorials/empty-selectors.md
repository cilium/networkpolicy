# Tutorial: Understanding Empty Selectors `{}`

Network Policy Editor is pre-loaded with a policy that contains different variations of empty curly braces (i.e "{}"):

```yaml
ingress:
  - {}
  - from:
    - podSelector: {}
```

You mouse over the visual representation of each rule to learn more about it. 

At first glance, empty curly braces (i.e. "{}") could mean "match on everything". However, it's not always true:

```
ingress:
  - {}
```

An empty curly braces are used at a rule level, they're translated to an empty rule. In theory, it should match on everything: all pods in the same namespace, all pods in other namespaces, and even traffic from or to outside of the cluster. However, in reality they only match on all pods in the cluster, and effectively, represent the following policy rule:
```
ingress:
  - from:
    - podSelector: {}
      namespaceSelector: {}
```

> **Note**: it doesn't not include ipBlock, therefore this rule is not going to match on any out-of the cluster traffic.

At the same time, the following rule might look almost identical:

```
  - from:
    - podSelector: {}
```

However, it will only match on the pods in the same namespace, and will not match on ingress traffic from other namespaces.