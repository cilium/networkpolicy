# Tutorial: Misunderstanding How Policy Rules Combine

This tutorial demonstrates how network policy rules combine.

Currently Network Policy Editor is loaded with an example policy. Original intent of this policy was to allow egress traffic only to an external VM 192.168.1.22/32 port 443. However,  The additional "`-`" in front of "`ports`" means that this is interpreted as two different rules, one that allows all traffic to the VM IP (on any port) and another that allows all traffic to port 443 (regardless of IP address). The network policy specification dictates that the rules are logically ORed (not ANDed), meaning the Pod workload has significantly more connectivity than intended.

## Fix the policy

1. Remove existing 443 rule.

2. Click on the 192.168.1.22/32 and modify the rule to add port 443.