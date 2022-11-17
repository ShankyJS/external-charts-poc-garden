# Garden issue with Helm Provider

Basically what's happening is that the behaviour of valuesFiles is not working as expected, for githubRepository based charts Garden is expecting that our custom values files live in the charts repository which will not be applicable in 99% of the cases.

To reproduce it only run `garden deploy` it will give you the following error:

````
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🌍  Running in namespace default in environment default
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

✔ providers                 → Getting status... → Done
   ✔ providers                 → Getting status... → Done
   ✔ graph                     → Resolving 11 modules... → Done
✔ graph                     → Resolving 2 modules... → Done
✔ redis                     → Building version v-32d7ed7193... → Done (took 3.6 sec)
✔ extra                     → Building version v-e6a2b22017... → Done (took 0 sec)
✖ extra                     → Deploying version v-dc1327c112...
✔ redis                     → Deploying version v-f0d22b9e17... → Already deployed

Failed deploying service 'extra' (from module 'extra'). Here is the output:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Command "/Users/jhan.silva/.garden/tools/helm/87730171d8485663/darwin-arm64/helm --kube-context
docker-desktop --namespace external-charts-poc-garden-default install extra
/Users/jhan.silva/Documents/os/external-charts-poc-garden/.garden/build/extra/charts/prometheus
--namespace external-charts-poc-garden-default --timeout 300s --values
/Users/jhan.silva/Documents/os/external-charts-poc-garden/.garden/build/extra/k8s/values-prometheus.yaml
--values /Users/jhan.silva/Documents/os/external-charts-poc-garden/.garden/build/extra/charts/prometheus/g
arden-values.yml --atomic" failed with code 1:

Error: INSTALLATION FAILED: open
/Users/jhan.silva/Documents/os/external-charts-poc-garden/.garden/build/extra/k8s/values-prometheus.yaml:
no such file or directory

Error: INSTALLATION FAILED: open
/Users/jhan.silva/Documents/os/external-charts-poc-garden/.garden/build/extra/k8s/values-prometheus.yaml:
no such file or directory
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
1 deploy action(s) failed!
````