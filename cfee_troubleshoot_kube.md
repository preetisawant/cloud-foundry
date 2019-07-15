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

# Debugging Kubernetes cluster
{: #debug_cluster}

CFEE instances are provisioned on a Kubernetes cluster ({{site.data.keyword.containerlong}}).
This tutorial shows how to debug your Kubernetes cluster, on which your {{site.data.keyword.cfee_full}} (CFEE) is running.
You can also use the debugging documentation for {{site.data.keyword.containerlong}}:
- [Troubleshooting clusters and worker nodes](/docs/containers?topic=containers-cs_troubleshoot_clusters)

## API server down / high number of errors / high latency
{: #apiserver_debug}
### Monitoring Alerts
{: #apiserver_debug_mon}
KUBE:K8SApiserverDown / KUBE:APIServerErrorsHigh / KUBE:APIServerLatencyHigh

### What's happening
{: #apiserver_debug_hap}

The [Kubernetes master](/docs/containers?topic=containers-ibm-cloud-kubernetes-service-technology#architecture) is the main component that keeps your cluster up and running. The master stores cluster resources and their configurations in the etcd database that serves as the single point of truth for your cluster. The Kubernetes API server is the main entry point for all cluster management requests from the worker nodes to the master, or when you want to interact with your cluster resources. These alerts mean that there is an issue with your API server and some cluster tasks could be not possible. The alerts are in place to notify you about possible limitations for cluster
related tasks during the issues on API server.

### Impact
{: #apiserver_debug_imp}

If the Kubernetes API Server is down or crashing it will be not possible to stop, update, or start new pods and services. Existing pods and services should continue to work.  

Do not restart or reboot a worker node during a master outage. This action removes the pods from your worker node. Because the Kubernetes API server is unavailable, the pods cannot be rescheduled onto other worker nodes in the cluster.
{: important}

### How to Fix
{: #apiserver_debug_fix}

1. Your IBM Cloud Kubernetes Service includes an IBM-managed master with highly available replicas, automatic security patch updates applied for you, and automation in place to recover in case of an incident. You can check the health, status, and state of the cluster master by running `ibmcloud ks cluster-get --cluster <cluster_name_or_ID>`.

2. If you need more details about actual status for the issue - contact IBM Support for {{site.data.keyword.containerlong}} by opening a case as describe at the end of this page.

## Issues with DaemonSets
{: #daemonset_debug}
### Monitoring Alert
{: #daemonset_debug_mon}
KUBE:DaemonSetRolloutStuck / KUBE:DaemonSetsMissScheduled / KUBE:K8SDaemonSetsNotScheduled

### What's happening
{: #daemonset_debug_hap}

A DaemonSet make sure that all or some Kubernetes nodes run a copy of a pod. The default update strategy for DaemonSets is RollingUpdate - that means, if you update a DaemonSet template, old DaemonSet pods will be killed, and new pods will be created automatically. The alerts mean that one of operations is not successful for DaemonSet pods.

### Impact
{: #daemonset_debug_imp}

The impact from these alerts is depend on the pods affected by the issue. E.g. if a `prometheus-node-exporter` pod can not be created on one of the node, you will not be able to receive monitoring metrics for this node during the issue.

### How to Fix
{: #daemonset_debug_fix}

1. Find your cluster in https://cloud.ibm.com/resources. It usually looks like `<your CFEE name>-cluster`.
2. Select the cluster and follow the instruction in `Access` tab to setup the connection to your cluster.
3. You can list all active DaemonSets on your cluster using the command `kubectl get ds --all-namespaces` . By default you see 4 active DaemonSets on your CFEE cluster - `calico-node`, `ibm-keepalived-watcher`, `ibm-kube-fluentd`, `prometheus-node-exporter`.
4. The DaemonSet settings can be checked using `kubectl describe daemonset <daemonset-name> -n <namespace>`.
5. Sometimes, a DaemonSet rolling update may be stuck - the causes could be that some of nodes run out of resources or the recent DaemonSet template is broken.
6. Identify the nodes that don't have the DaemonSet pods scheduled on by using the output of `kubectl get nodes -n <namespace>` and `kubectl get pods -n <namespace> -o wide` commands. Try to clean-up the identified nodes (e.g. delete non-DaemonSet pods using `kubectl delete pod <name>`).
7. To resolve the broken DaemonSet template use `kubectl edit ds/<daemonset-name>` to update and fix a possible template issue.


## File descriptors issue
{: #fdlimit_debug}
### Monitoring Alert
{: #fdlimit_debug_mon}
KUBE:FdExhaustionClose

### What's happening
{: #fdlimit_debug_hap}

The operating system uses file descriptors to handle file-system files as well as pseudo files, such as connections and listener sockets.
The alert means that the number of allocated file descriptors is near to the limit for the system.

### Impact
{: #fdlimit_debug_imp}

If the system will reach the limit, that could be a serious problem because the system will be not able to open any more files.

### How to Fix
{: #fdlimit_debug_fix}

1. Find your cluster in https://cloud.ibm.com/resources. It usually looks like `<your CFEE name>-cluster`.
2. Select the cluster and follow the instruction in `Access` tab to setup the connection to your cluster.
3. Check the actual status of pods from your cluster using the command below (you can find <namespace> in the alert).
  ```
  kubectl get pods -n <namespace>
  ```
  {: screen}
4. If you don't see any resource issues on the cluster, try to recreate the problematic pod. Use the command below - replace the pod name with the name of pod from Prometheus alert and appropriated namespace:
  ```
  kubectl delete pod <pod> -n <namespace>
  ```
  {: screen}
5. Wait at least 1 minute and verify the alert disappears from Prometheus.


## K8S nodes not ready
{: #nodes_debug}
### Monitoring Alert
{: #nodes_debug_mon}
KUBE:K8SNodeNotReady / KUBE:K8SManyNodesNotReady

### What's happening
{: #nodes_debug_hap}

When this alert comes in, it means that one or more Kubernetes cluster worker nodes are not in a healthy state. Validation is required to not only validate the state but know what follow up actions are required to run a manual fix.

### Impact
{: #nodes_debug_imp}

It depends on the number of unhealthy worker nodes and which worked nodes are affected.

### How to Fix
{: #nodes_debug_fix}

1. Find your cluster in https://cloud.ibm.com/resources. It usually looks like `<your CFEE name>-cluster`.
2. Select the cluster and follow the instruction in `Access` tab to setup the connection to your cluster.
3. Take a deeper look at the cluster you need to investigate with `ibmcloud cs cluster-get <cluster_name>`.
4. Using the command `ibmcloud cs workers <cluster_name>` you can see the actual status of worker nodes.
5. If unhealthy worker node is in a `reloading` state, wait and allow the reload to attempt to complete before continuing with the instructions below.
6. Check at the events in your IBM Cloud account that aren't any planned or unplanned events that might be affecting the worker nodes.
7. The last possibility to resolve the issue is to manually re-create the unhealthy worker node.
From the information retrieved in the `worker-get` command above fill out this command with the appropriate values. These will be the replacement worker nodes before you remove the ones in a bad state.
```
ibmcloud cs worker-add --cluster <cluster_name> --private-vlan <vlan_num> --public-vlan <pub_vlan_num> --machine-type b2c.4x16 --workers <number_of_workers>
```
{:screen}
Validate that the new worker is provisioned and in a running state.
8. Removing the old workers in a bad state:
```
ibmcloud cs worker-rm --cluster <cluster_name> --workers worker_name,<worker_name>
```
9. Check the actual status of your cluster using `ibmcloud cs workers <cluster_name>` command.

## Certificate expires
{: #certexpires}
### Monitoring Alert
{: #certexpires_mon}
KUBE:K8sCertificateExpirationNotice

### What's happening
{: #certexpires_hap}

Kubernetes API Certificate is expiring soon (less than 7 days)

### Impact
{: #certexpires_imp}

If the Kubernetes cluster certificate expires on the Kubernetes master, then the kubelet service will fail. Issuing a kubectl command, such as `kubectl get pods` or `kubectl exec -it <container_name> bash`, will result in a message similar to **unable to connect to the server: x509: certificate has expired or is not yet valid**. Pods on the respective worker nodes can no longer be managed.

### How to Fix
{: #certexpires_fix}

Kubernetes master is IBM-managed. You need to contact IBM Support by opening a case - see [Getting Help and Support](/docs/cloud-foundry?topic=cloud-foundry-debug_cluster#ts_getting_help).


## Issue with frequently restarted pods
{: #podsrestarting}
### Monitoring Alert
{: #podsrestarting_mon}
KUBE:PodFrequentlyRestarting

### What's happening
{: #podsrestarting_hap}

Every pod has a restartPolicy setting. If the pod has an issue, Kubernetes will automatically perform a restart of this pod according to the pod's restart policy. If a pod is restarting frequently, this shows a potential issue on the pod.

### Impact
{: #podsrestarting_imp}

The services running on the affected pod are not available during restarts.

### How to Fix
{: #podsrestarting_fix}

1. Find your cluster in https://cloud.ibm.com/resources. It usually looks like `<your CFEE name>-cluster`.
2. Select the cluster and follow the instruction in `Access` tab to setup the connection to your cluster.
3. Check the status of pods in your cluster using `kubectl get pods --all-namespaces` command. You can also list the pods which are not in the state `Running` - `kubectl get pods --all-namespaces | grep -iv Running`.
4. Even if you see the pod listed in the Prometheus alert is in state **Running**, a high counter of Restarts shows a potential issue on this pod.
5. Run `kubectl describe pod <pod_name> -n <namespace>` to get details about the pod startup and running containers on this pod. Check the `Events` section in the output, to see possible error messages related to the restarts.
6. Another possibility to find the cause for restarts, is to check the container logs using `kubectl logs <pod_name> -c <container> -n <namespace>`.
7. Run the next command to delete pod from alert. Kubernetes will recreate it automatically.
  ```
  kubectl delete pod <pod name> -n <namespace>
  ```
  {: pre}


## Getting help and support
{: #ts_getting_help}

Still having issues with your {{site.data.keyword.cfee_full}}?
{: shortdesc}

-  In the terminal, you are notified when updates to the `ibmcloud` CLI and plug-ins are available. Be sure to keep your CLI up-to-date so that you can use all the available commands and flags.
-   To see whether {{site.data.keyword.Bluemix_notm}} is available, [check the {{site.data.keyword.Bluemix_notm}} status page ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/status?selected=status).
-   From the console, check if you have any relevant **Notifications** ![Notifications icon](../icons/Notification_PUP.svg "Notifications icon").
-   Contact IBM Support by opening a case. To learn about opening an IBM support case, or about support levels and case severities, see [Contacting support](/docs/get-support?topic=get-support-getting-customer-support#getting-customer-support).
When you report an issue, include your cluster ID. To get your cluster ID, run `ibmcloud ks clusters`.
{: tip}
