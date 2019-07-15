---

copyright:
  years: 2019
lastupdated: "2019-07-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Debugging monitoring components
{: #monitoring_debug}

This tutorial shows how to debug monitoring components on your {{site.data.keyword.cfee_full}} (CFEE).

Monitoring an {{site.data.keyword.cfee_full}} instance and its infrastructure is supported by an open-source toolset consisting of Prometheus and Grafana.  The solution enables you to analyze, visualize and manage alerts for metrics in the Cloud Foundry environment.  There are three web consoles from which monitoring takes place: A Grafana console, a Prometheus console, and a Prometheus Alert Manager console.

More details about monitoring components are available: [CFEE Monitoring](/docs/cloud-foundry?topic=cloud-foundry-monitoring)

## Alertmanager reload failed
{: #alertmanager_debug}
### Monitoring Alert
{: #alertmanager_debug_mon}
OPS:AlertmanagerFailedReload

### What's happening
{: #alertmanager_debug_hap}

Alertmanager has a default configuration file that defines the policies for handling, grouping, and notification routing of Alertmanager alerts. A reload of configuration file can be done at runtime. If this file is not well-formed, the changes will not be loaded and an error will be logged.

### Impact
{: #alertmanager_debug_imp}

The configuration file that has to be reloaded can not be activated. But the actual running configuration for Alertmanager should be still active without any impact.

### How to Fix
{: #alertmanager_debug_fix}

1. Find your cluster in https://cloud.ibm.com/resources. It usually looks like `<your CFEE name>-cluster`.
2. Select the cluster and follow the instruction in `Access` tab to setup the connection to your cluster.
3. Check the actual status of prometheus-alertmanager pod from your cluster using the commands below.
  ```
  kubectl get pods -n monitoring
  ```
  {: pre}
  Using the name of pod for prometheus-alertmanager from output above, try the next command:
  ```
  kubectl describe pod <prometheus-alertmanager-pod> -n monitoring
  ```
  {: screen}
  Check the `Events` section and address any error or warning messages that are listed.
  Under `Containers` section - there should be 2 containers running on prometheus-alertmanager pod:
  - `prometheus-alertmanager-config-updater`
  - `prometheus-alertmanager`  
4. Check the logs of containers:
  ```
  kubectl logs <prometheus-alertmanager-pod> -c prometheus-alertmanager-config-updater -n monitoring
  ```
  {:screen}
  ```
  kubectl logs <prometheus-alertmanager-pod> -c prometheus-alertmanager -n monitoring
  ```
  {:screen}
5. Check the active configmap for the running instance of alertmanager:
  ```
  kubectl describe configmaps prometheus-alertmanager -n monitoring
  ```
  {:pre}
7. If you don't see any exact sign what causing the issue, try to recreate the problematic pod. Use the command below - replace the pod name with the name of pod from step 3:
  ```
  kubectl delete pod <prometheus-alertmanager-pod> -n monitoring
  ```
  {: screen}

## Prometheus config reload failed
{: #prometheus_config_debug}
### Monitoring Alert
{: #prometheus_config_debug_mon}
OPS:PrometheusConfigReloadFailed

### What's happening
{: #prometheus_config_debug_hap}

Reloading Prometheus’ configuration has failed for a given namespace `monitoring`.

### Impact
{: #prometheus_config_debug_imp}

Prometheus can reload its configuration at runtime. If the new configuration is not well-formed, the changes will not be applied. The previous configuration should be still active and have no impact to the running services.

### How to Fix
{: #prometheus_config_debug_fix}

1. Find your cluster in https://cloud.ibm.com/resources. It usually looks like `<your CFEE name>-cluster`.
2. Select the cluster and follow the instruction in `Access` tab to setup the connection to your cluster.
3. Check the actual status of prometheus-server pod from your cluster using the commands below.
  ```
  kubectl get pods -n monitoring
  ```
  {: pre}
  Using the name of pod for prometheus-server from output above, try the next command:
  ```
  kubectl describe pod <prometheus-server-pod> -n monitoring
  ```
  {: screen}
  Under `Containers` section - there should be 2 containers running on prometheus-server pod:
  - `prometheus-server-configmap-reload`
  - `prometheus-server`  
4. Check the active configmap for the running instance of prometheus_server:
  ```
  kubectl describe configmaps prometheus-server -n monitoring
  ```
  {:pre}
5. The configuration files are stored on PVC (persistent volume claim) - monitoring/prometheus-server.
Check if the PVC status is `Bound`:
  ```
  kubectl describe pvc prometheus-server -n monitoring
  ```
  {: pre}
6. Try to recreate prometheus-server pod:
  ```
  kubectl delete pod <prometheus-server-pod> -n monitoring
  ```
  {: screen}

## Prometheus error sending alerts / Prometheus not connected to Alertmanager
{: #prometheus_alertm_error_debug}
### Monitoring Alert
{: #prometheus_alertm_error_debug_mon}
OPS:PrometheusErrorSendingAlerts / OPS:PrometheusNotConnectedToAlertmanagers

### What's happening
{: #prometheus_alertm_error_debug_hap}

Errors while sending alerts from Prometheus server to Alertmanager / Prometheus is not connected to any Alertmanagers.

### Impact
{: #prometheus_alertm_error_debug_imp}

The defined rules to process alerts from Prometheus server can not be executed on Alertmanager (e.g. deduplication, grouping, send alerts to the appropriate receiver via e-mail, PagerDuty, Slack).

### How to Fix
{: #prometheus_alertm_error_debug_fix}

1. Using the document [Accessing the Kubernetes cluster: Port forwarding](/docs/cloud-foundry?topic=cloud-foundry-monitoring#accessing-the-kubernetes-cluster-port-forwarding) check the status of Prometheus server and Alertmanager (after port forwarding activated - `curl localhost:9090` and `curl localhost:9093`).
2. Make sure that the appropriated pods are up and running:
  ```
  kubectl -n monitoring get pods
  ```
  {:pre}
  If you see any pods in status `Unknown` or `NodeLost` try to resolve the situation using [Troubleshooting clusters](/docs/containers?topic=containers-cs_troubleshoot_clusters).
3. The logs of prometheus-server and alertmanager can give more details about possible issue:
  ```
  kubectl logs -n monitoring <prometheus-server-pod> -c prometheus-server
  kubectl logs -n monitoring <prometheus-alertmanager-pod> -c prometheus-alertmanager
  ```
  {:screen}
4. Try to recreate prometheus-server and alertmanager pods:
  ```
  kubectl delete pod <prometheus-server-pod> -n monitoring
  kubectl delete pod <alertmanager-pod> -n monitoring
  ```
  {: screen}

## Prometheus notification queue running full
{: #promqueue_full}
### Monitoring Alert
{: #promqueue_full_mon}
OPS:PrometheusNotificationQueueRunningFull

### What's happening
{: #promqueue_full_hap}

Prometheus' alert notification queue is running full. Prometheus is generating more alerts than it can send to Alertmanagers in time. The default capacity for the notification queue is 10000.

### Impact
{: #promqueue_full_imp}

If the Prometheus notification queue is full, the alerts could be dropped and not forwarded to the Alertmanager.

### How to Fix
{: #promqueue_full_fix}

1. Using the document [Accessing the Kubernetes cluster: Port forwarding](/docs/cloud-foundry?topic=cloud-foundry-monitoring#accessing-the-kubernetes-cluster-port-forwarding) check the status of your Prometheus server
2. As next step of debugging you can check how the metrics listed below developed over time on the problematic Prometheus instance (Go to `Alerts` tab on Prometheus console, copy the metric below into the metrics field and click on `Execute`button):
  - prometheus_notifications_queue_length
  - rate(prometheus_notifications_sent_total[1m])
  - rate(prometheus_notifications_dropped_total[1m])
  - rate(alertmanager_notifications_failed_total[1m])
  - rate(prometheus_notifications_latency_seconds_sum[5m]) / rate(prometheus_notifications_latency_seconds_count[5m])
3. Try to understand where the alerts come from and to resolve a possible issue on these problematic components.
4. The prometheus-server logs can be also useful to find the reason for the long queue:
  ```
  kubectl logs -n monitoring <prometheus-server-pod> -c prometheus-server
  ```
  {:screen}
5. If you see any connections issues to/from Prometheus server, try to recreate the prometheus-server pod:
  ```
  kubectl delete pod <prometheus-server-pod> -n monitoring
  ```
  {: screen}

## Prometheus TSDB issues
{: #tsdb_debug}
### Monitoring Alert
{: #tsdb_debug_mon}
OPS:PrometheusTSDBCompactionsFailing / OPS:PrometheusTSDBReloadsFailing / OPS:PrometheusTSDBWALCorruptions

### What's happening
{: #tsdb_debug_hap}

Prometheus includes a on-disk time series database. This database stores time series data und actually located at /data directory (mount from storage volume - PersistentVolume) on Prometheus server. See [Prometheus  storage](https://prometheus.io/docs/prometheus/latest/storage/).
The alerts mean that there is an issue with this database:
a. Prometheus has issues compacting sample blocks
b. Prometheus has issues reloading data blocks from disk
c. Prometheus write-ahead log is corrupted

### Impact
{: #tsdb_debug_imp}

If the Prometheus database becomes corrupted, you might lose monitoring data.

### How to Fix
{: #tsdb_debug_fix}

If you see any issues with storage volume you can also follow [Troubleshooting cluster storage](/docs/containers?topic=containers-cs_troubleshoot_storage) for debugging.

1. Find your cluster in https://cloud.ibm.com/resources. It usually looks like `<your CFEE name>-cluster`.
2. Select the cluster and follow the instruction in `Access` tab to setup the connection to your cluster.
3. Check the pod status for prometheus_server:
  ```
  kubectl -n monitoring get pods
  ```
  {:pre}
  If the server has been crashed, you can lose data or the date might be left in an inconsistent state.
4. List the logs of prometheus_server to see any reasons for the issue:
  ```
  kubectl logs -n monitoring <prometheus-server-pod> -c prometheus-server
  ```
  {:screen}
  If you see any errors regarding data chunks (`/data/*` sub-directories) try to restore the old files to these sub-directories from backup (if available). If there are no backup files try to move the coruppted data to a temporary place and recreate the prometheus_server pod.
5. To check the local data directly, login to prometheus_server container:
  ```
  kubectl exec -it  <prometheus-server-pod> -c prometheus-server -n monitoring -- /bin/bash
  ```
  {:screen}
  Check disk usage (change into /data directory): `find . ls` or `du -s *`
  If you see any *.tmp directories not being actively written, try to delete them because they are not recoverable.
6. Check the `meta.json` files in each TSDB directory to find any messages for possible reason of the issue.


## Getting help and support
{: #ts_getting_help}

Still having issues with your {{site.data.keyword.cfee_full}}?
{: shortdesc}

-  In the terminal, you are notified when updates to the `ibmcloud` CLI and plug-ins are available. Be sure to keep your CLI up-to-date so that you can use all the available commands and flags.
-   To see whether {{site.data.keyword.Bluemix_notm}} is available, [check the {{site.data.keyword.Bluemix_notm}} status page ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/status?selected=status).
-   From the console, check if you have any relevant **Notifications** ![Notifications icon](../icons/Notification_PUP.svg "Notifications icon").
-   Contact IBM Support by opening a case. To learn about opening an IBM support case, or about support levels and case severities, see [Contacting support](/docs/get-support?topic=get-support-getting-customer-support#getting-customer-support).
When you report an issue, include your cluster ID. To get your cluster ID, run `ibmcloud ks clusters`. To get your CFEE instance ID, run `ibmcloud cfee environments`.
{: tip}
