# Allow Cross Namespace Traffic

As you can see in the editor's visualization, the network policy will only work if both pods are in the same namespace. The podSelector is scoped to the policy's namespace unless you explicitly use namespaceSelector to select other namespaces.

**Kubernetes Network Policy rule must contain networkPolicy selector in order for the rule to be applied across multiple namespaces.**

There are several options in fixing the policy:


**Option 1.** Use namespaceSelector: {}

namespaceSelector: {} selects all namespace in the cluster. 

**Option 2.** Match on namespace labels

todo
