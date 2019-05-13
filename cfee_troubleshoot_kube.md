---

copyright:
  years: 2019
lastupdated: "2019-04-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Debugging Kubernetes cluster
{: #debug_cluster}

CFEE instances are provisioned on a Kubernetes cluster. 
This tutorial shows how to debug your Kubernetes cluster, on which your {{site.data.keyword.cfee_full}} (CFEE) is running.

## API server down / high number of errors / high latency
{: #apiserver_debug}
### Monitoring Alert
KUBE:K8SApiserverDown / KUBE:APIServerErrorsHigh / KUBE:APIServerLatencyHigh

## K8S kubelet down
{: #kubelet_debug}
### Monitoring Alert
KUBE:K8SKubeletDown 

## K8S nodes not ready
{: #nodes_debug}
### Monitoring Alert
KUBE:K8SNodeNotReady / KUBE:K8SManyNodesNotReady

## Node disk full
{: #nodediskfull}
### Monitoring Alert
KUBE:NodeDiskRunningFull 

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
