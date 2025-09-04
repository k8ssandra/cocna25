# Community Over Code NA 2025 K8ssandra workshop
## Step 7 - Replacing a (dead) node

Replacement of a faulty or dead (Cassandra) node is performed through a K8ssandraTask custom resource.  
It will perform the following operations:
- take down the faulty pod and delete its PVC
- restart the replacement pod and inject the `-Dcassandra.replace_address_first_boot=x.x.x.x` flag

Apply the `replacenode-task.yaml` manifest to trigger the replacement of the first node/pod:

```
kubectl apply -f ./step7/replacenode-task.yaml -n db
```