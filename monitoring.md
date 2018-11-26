---

copyright:
  years: 2018
lastupdated: "2018-11-26"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Monitoring
{: #monitoring}

Monitoring an {{site.data.keyword.cfee_full}} instance and its supported infrastructure is supported by an open-source toolset consisting of Prometheus and Grafana.  The solution enables you to analyze, visualize and manage alerts for metrics in the Cloud Foundry environment.  There are three web consoles from which monitoring takes place: A Grafana console, a Prometheus console, and a Prometheus Alert Manager console.

**Note:** Access to the monitoring capability in an {{site.data.keyword.cfee_full}} instance requires an _Administrator_ or _Editor_ role in that Kubernetes cluster supporting the CFEE instance.  The default name of the Kubernetes cluster supporting a CFEE instance is _`<CFEEname>`-cluster_.

## Prometheus
{: #prometheus}

Prometheus is an open-source systems monitoring and alerting toolkit. Since its inception in 2012, many companies and organizations have adopted Prometheus, and the project has a very active developer and user community.
It is a standalone open source project and maintained independently of any company. To emphasize this, and to clarify the project's governance structure, Prometheus joined the Cloud Native Computing Foundation in 2016 as the second hosted project, after Kubernetes. See the [Prometheus documentation](https://prometheus.io/docs/introduction/overview/) for more information.

The Prometheus ecosystem consists of multiple components, many of which are optional:

* The main Prometheus server which scrapes and stores time series data.</li>
* [Alertmanager](https://prometheus.io/docs/alerting/alertmanager/) to handle alerts.</li>
* Various special-purpose exporters like node exporter, blackbox exporter, etc.</li>
* A push gateway for supporting short-lived jobs.</li>

Prometheus gathers metrics from instrumented jobs, either directly or via an intermediary push gateway for short-lived jobs. It stores all gathered samples locally and runs rules over this data to either aggregate and record new time series from existing data, or to generate alerts.

## Grafana
{: #grafana}

Grafana is an open-source analytics platform for all metrics collected by Prometheus. The deployed Grafana version on your cluster is already configured to use the underlying Prometheus database. It also contains some valuable Grafana dashboards.  See the [Grafana documentation](http://docs.grafana.org/guides/getting_started/) for more information.

## Getting Started with Monitoring
{: #gettingStarted_monitor}

The Prometheus and Grafana components comprising the monitoring solution are pre-installed in the Kubernetes infrastructure supporting the CFEE instance.  To access the monitoring tools require to forward the ports of the Prometheus, Prometheus AlertManager, and Grafana servers.  This is done through the Kubernetes CLI.
The following guides you through the steps for installing the required CLI's, forwarding the server ports, and launching the consoles.

**Note:** The following instructions are also available in the {{site.data.keyword.cfee_full}} user interface.  Open the CFEE instance user interface and click **Monitoring** in the left navigation pane to see the instructions displayed.

### Prerequisites

1. Check your [Access Policies](https://console.bluemix.net/iam/#/users) to ensure that you have at least a Viewer role on the Kubernetes cluster supporting the environment.
2. Install the [IBM Cloud CLI](https://console.bluemix.net/docs/cli/reference/ibmcloud/download_cli.html#install_use).
3. Install the [Kubernetes CLI](https://kubernetes.io/docs/tasks/tools/install-kubectl/).  If you have an existing Kubernetes CLI, we recommend that you install the latest version.
4. Install the container service plug-in:
```
    ibmcloud plugin install container-service -r Bluemix
```

### Access the Kubernetes cluster

1. Log into your IBM Cloud account:

  ```
  ibmcloud login -a https://api.ng.bluemix.net
  ```
  {: pre}

  If you have a federated ID, use __ibmcloud login -sso__ to log into the IBM Cloud CLI.

2. Target the IBM Cloud Container Service region in which you want to work (e.g., us-south):

  ```
  ibmcloud cs region-set us-south
  ```
  {: pre}

3. Set the context of the cluster in your cli:

  a. Get the command to set the environment variable and download the Kubernetes configuraton files:

  ```
  ibmcloud cs cluster-config <CFEE_instance_name>-cluster
  ```
  {: pre}

  b. Set the KUBECONFIG environment variable. Copy the output from the previous command and paste it in your terminal. The command output should look similar to the following:
  __export KUBECONFIG=/Users/$USER/.bluemix/plugins/container-service/clusters/cf-admin-0703-cluster/kube-config-dal10-cf-admin-0703-cluster.yml__

### Forward server ports
4. Set up port-forwarding in the Kubernetes cluster for the pods running Prometheus, AlertManager and Grafana. This will enable you to host the monitoring metrics by proxy on your local machine (localhost):

  ```
  sh -c 'kubectl -n monitoring port-forward deployment/prometheus-server 9090 & kubectl -n monitoring port-forward deployment/prometheus-alertmanager 9093 & kubectl -n monitoring port-forward deployment/grafana 3000'
  ```
  {: pre}

### Launch the monitoring consoles on your local web proxy

5. Launch the Grafana console to see analytics on selected metrics.  There are default Grafana dashboards included in the CFEE instance. Those default dashboards are interactive and give you a view of the infrastructure used to host your CFEE instance (Kubernetes cluster). Once you launch the Grafana console, click the **Home** button at the top of the Grafana console to select one of the pre-deployed dashboards (see list below), which will graph the corresponding metrics:

   There is a default `admin` user in Grafana, with the default password set to `admin`. We recommend to login with Userd/Password `admin/admin`, and change them to new credentials:

     [Launch Grafana console](https://localhost:3000)

   The following default dashboards are provided with the CFEE instance and are available from the _Home_ dropdown.

   Dashboards for the Kubernetes infrastructure supporting your CFEE environment:
   - _Kubernetes Capacity Planning_ dashboard
        - Shows the capacity of the kubernetes infrastructure .
   - _Kubernetes Cluster Health_ dashboard
        - Shows the health of the Kubernetes cluster.
   - _Kubernetes Cluster Status_ dashboard
        - Shows the status of the Kubernetes cluster.
   - _Kubernetes Resource Requests_ dashboard
        - Shows the used CPU, memory and other parameters of the Kubernetes cluster.
   - _Nodes_ dashboard
        - Shows details for each worker node of the Kubernetes cluster.
   - _Pods_ dashboard
        - Shows details for each pod running on the Kubernetes cluster.
   - _Replica Set_ dashboard
        - Shows the status of the Kubernetes replica sets.
   - _Deployment_ dashboard
        - Shows the status of your Kubernetes deployments.

   Cloud Foundry dashboards:
   - _CF: Cells Capacity_ dashboard
        - Shows the general status of the Cloud Foundry cells where the Cloud Foundry applications are deployed.
   - _CF: Router_ dashboard
        - Shows the Cloud Foundry router status running on your CFEE environment.
   - _CF: Diego_Cell_ dashboard
        - Shows the status of the Cloud Foundry cells and Diego components.

6. Optionally, you can also launch the Prometheus console to see the raw data collected by the Prometheus server, and the Prometheus Alertmanager to manage the alerts sent by the Prometheus server:

     [Launch Prometheus server](https://localhost:9090)

     [Launch Prometheus Alertmanager server](https://localhost:9093)
