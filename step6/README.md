# Community Over Code NA 2025 K8ssandra workshop
## Step 6 - Expanding to a new DC

Expanding to a new datacenter requires the addition of a new entry in `.spec.cassandra.datacenters`.

Apply the manifest from the step6 folder after inspecting it:

```
kubectl apply -f ./step6/k8ssandra-cluster.yaml -n db
```

Now observe the new CassandraDatacenter being created:

```
kubectl get CassandraDatacenter -n db
```

and eventually the dc2 pods starting up:

```
kubectl get pods -n db
```

The rebuild operation is scheduled automatically once all db pods are up in DC2.