# Community Over Code NA 2025 K8ssandra workshop
## Step 4 - Scheduling repairs

## Port forwarding and accessing the Reaper UI

```
kubectl port-forward svc/test-dc1-reaper-service -n db 8080:8080
```

Then open your browser at: [http://127.0.0.1:8080/webui](http://127.0.0.1:8080/webui)

## Reading Reaper's UI credentials

Read and decode the reaper-ui username and password:

```
kubectl get secret test-reaper-ui -o jsonpath='{.data.username}' -n db | base64 --decode | xargs
kubectl get secret test-reaper-ui -o jsonpath='{.data.password}' -n db | base64 --decode | xargs
```

Use the values to authenticate to the UI.

## Start a repair from the UI

Navigate through the UI and create a one off repair run.


## Enable auto-scheduling

Enabling auto-scheduling:​

```
  reaper:​
    autoscheduling:​

      enabled: true​
```

Apply the updated manifest from the step4 folder:​
​
```
kubectl apply -f ./step4/k8ssandra-cluster.yaml -n db​
```

Wait for the reaper pod to restart and then port-forward the UI again.
After a bit, we should have a repair schedule created for both `myks1` and `myks2`.