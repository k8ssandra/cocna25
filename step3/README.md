# Community Over Code NA 2025 K8ssandra workshop
## Step 2 - Create a K8ssandraCluster

Now that k8ssandra-operator is up and running, we can create our first K8ssandraCluster.


## Create a namespace for the Cassandra Cluster

```
kubectl create namespace db
```

The above command will create a `db` namespace (ns) in the Kubernetes cluster.

Note: Don't confuse "namespace" which is a Kubernetes concept with "keyspace" which is a Cassandra concept.


## Create the K8ssandraCluster in the db namespace

Inspect the [manifest](k8ssandra-cluster.yaml) and create the K8ssandraCluster by running the following command:

```
kubectl apply -f ./step3/k8ssandra-cluster.yaml -n db
```

Monitor the cluster creation by checking the pods in the `db` namespace:

```
kubectl get pods -n db
```

Eventually, you should have 3 pods in the `db` ns:

```
kubectl get pods -n db
```
```
NAME                   READY   STATUS    RESTARTS   AGE
test-dc1-rack1-sts-0   2/2     Running   0          7m57s
test-dc1-rack1-sts-1   2/2     Running   0          7m57s
test-dc1-reaper-0      1/1     Running   0          2m40s
```

## Tail the system.log file from one of the db pods

There are multiple containers running in each db pod:
* **cassandra:** runs the management-api server as primary process and outputs its log in the standard output​
* **server-system-logger:** runs an instance of vector (vector.dev) which outputs the system.log file from the cassandra process. Also manages customizable observability pipelines

Tail the system.log output:​
```​
kubectl logs test-dc1-rack1-sts-0 -c server-system-logger -n db --follow​
```

## Create a couple of keyspaces with a table in each

A set of secrets was created by the operator in the `db` namespace

```
kubectl get secrets -n db
NAME             TYPE     DATA   AGE
test-reaper      Opaque   2      30m
test-reaper-ui   Opaque   2      30m
test-superuser   Opaque   2      30m
```

Read and decode the test-superuser secret username and password:

```
kubectl get secret test-superuser -o jsonpath='{.data.username}' -n db | base64 --decode | xargs
kubectl get secret test-superuser -o jsonpath='{.data.password}' -n db | base64 --decode | xargs
```

"Exec" into one of the db pods:

```
kubectl exec -i -t -n db test-dc1-rack1-sts-0 -c cassandra -- sh -c "clear; (bash || ash || sh)"
```

Check the topology by running nodetool:

```
nodetool status
```

Run cqlsh:

```
cqlsh -u <superuser name> -p <superuser password> test-dc1-service
```

Run the following commands:

```
create keyspace myks1 WITH replication = {'class': 'SimpleStrategy', 'replication_factor': 2};
create keyspace myks2 WITH replication = {'class': 'SimpleStrategy', 'replication_factor': 2};
create table myks1.table1 (id int PRIMARY KEY, val text);
create table myks2.table2 (id int PRIMARY KEY, val text);
```
