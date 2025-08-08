# Community Over Code NA 2025 K8ssandra workshop
## Step 5 - Upgrading

Upgrading Cassandra is as simple as changing the serverVersion value in the K8ssandraCluster manifest.

Apply the manifest from the step5 folder after inspecting it:

```
kubectl apply -f ./step5/k8ssandra-cluster.yaml -n db
```

Now observe the pods roll restarting and updating the underlying image:

```
kubectl describe pod/test-dc1-rack1-sts-1 -n db
```

### Post upgrade: run upgradesstables using a K8ssandraTask

There are a few common operations that K8ssandra can orchestrate in a rolling fashion, upgradesstables being one of them.

Check the [upgradesstables-task.yaml](upgradesstables-task.yaml) manifest and apply it to your cluster:

```
kubectl apply -f ./step5/upgradesstables-task.yaml -n db
```

Watch the execution status:

```
% kubectl get K8ssandraTask -n db
```
```
NAME                  JOB               SCHEDULED   STARTED   COMPLETED
upgradesstables-dc1   upgradesstables               4s   
```

Until completion:

```
NAME                  JOB               SCHEDULED   STARTED   COMPLETED
upgradesstables-dc1   upgradesstables               20s       10s
```

Look for upgradesstables completion log lines:

```
kubectl logs pod/test-dc1-rack1-sts-1 -c server-system-logger -n db |grep "Completed Upgrade sstables"
```

Should output something like:

```
INFO  [pool-2-thread-1] 2025-08-08 15:09:14,463 StorageService.java:4228 - Completed Upgrade sstables with status SUCCESSFUL
INFO  [pool-2-thread-1] 2025-08-08 15:09:14,465 StorageService.java:4228 - Completed Upgrade sstables with status SUCCESSFUL
INFO  [pool-2-thread-1] 2025-08-08 15:09:14,465 StorageService.java:4228 - Completed Upgrade sstables with status SUCCESSFUL
INFO  [pool-2-thread-1] 2025-08-08 15:09:14,466 StorageService.java:4228 - Completed Upgrade sstables with status SUCCESSFUL
INFO  [pool-2-thread-1] 2025-08-08 15:09:14,468 StorageService.java:4228 - Completed Upgrade sstables with status SUCCESSFUL
INFO  [pool-2-thread-1] 2025-08-08 15:09:14,474 StorageService.java:4228 - Completed Upgrade sstables with status SUCCESSFUL
```

