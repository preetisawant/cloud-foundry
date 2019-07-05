---

copyright:
  years: 2019
lastupdated: "2019-05-27"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Debugging Cloud Foundry components
{: #cf_debug}

This tutorial shows how to troubleshoot Cloud Foundry components in your {{site.data.keyword.cfee_full}} (CFEE).

You can take these general steps to ensure that your CFEE instances are up-to-date:
- Check on regular basis for available updates - [What's New in IBM Cloud Foundry Enterprise Environment](/docs/cloud-foundry?topic=cloud-foundry-what-s-new-in-ibm-cloud-foundry-enterprise-environment).
- [Update your CFEE instance](/docs/cloud-foundry?topic=cloud-foundry-update-scale) 

## Debugging unavailable stager
{: #stager_debug}
### Monitoring Alert
- N/A

### What's happening

Bulletin Board System (BBS) runs in active/passive mode and it maintains a lock in Locket to ensure that only one BBS is active. Sometimes if Locket loses connection with back-end database, it may run into an unresponsive status. In this case, no active BBS is elected and then BBS API is not accessible, and operations like cf push app will fail as Cloud Controller cannot communicate with BBS API.
Since CFEE 2.x, Diego BBS and Locket run in diego-api-x pod, so users need to restart all diego-api-x pods to bring the environment back.

### Impact

Diego BBS API is not accessible. Users are not able to do `cf push app` and CF application staging fails with an error `Stager is unavailable` as below:

  ```
    Response code: 503
    CC code:       0
    CC error code:
    Request ID:    xxxxxxx-xxxxx-xxx-xxxx-xxxxxxxx
    Description:   {
    "description": "Stager is unavailable: execution expired",
    "error_code": "CF-StagerUnavailable",
    "code": 170010
    }
    Server error, status code: 503, error code: 170010, message: Stager is unavailable: execution expired
  ```
  {: screen}

### How to fix it

The error message `Stager is unavailable` usually means that Cloud Controller has troubles to communicate with Diego BBS API.
Please follow these steps to confirm whether the issue reported is the same with this case.
If yes, please continue to recover the environment.
1. Make sure Cloud Controller is available by checking api-group-x pod status.
    ```
    kubectl get pods --namespace cf
    ```
    {: pre}
2. For example, the output indicates that 2 api-group-x pods are running.
    ```
    NAME                            READY   STATUS      RESTARTS   AGE
    api-group-0                           2/2     Running     0          1d
    api-group-1                           2/2     Running     0          1d
    ```
    {: screen}
3. Go into api-group-0 pod.
    ```
    kubectl exec --stdin --tty --namespace cf api-group-0 --container api-group /bin/bash
    ```
    {: pre}
4. In api-group-0 pod, if you get an error like below, it indicates that Cloud Controller cannot access BBS.
    ```
    nc -zv -w 5 diego-api-set.cf.svc.cluster.local 8889

    ```
    {: pre}
    - For example, the output indicates that connection failed:
    ```
    nc: connect to diego-api-set.cf.svc.cluster.local port 8889 (tcp) failed: Connection timed out
    ```
    {: screen}
5. Exit api-group-0 and then delete all diego-api-x pods as below. Kubernetes will recreate all of them automatically.
    ```
    kubectl delete pod --namespace cf diego-api-0
    ```
    {: pre}
    Before CFEE 2.0, Diego Lockets are located in separate pods named diego-locket-x. If this is the case, please restart all diego-locket-x pods like step 5.

6. Wait until all diego-api-x pods are `running` and `2/2` ready. Make sure one of diego-api-x pods is labeled as active.
    ```
    kubectl get pods --namespace cf -L skiff-role-active
    ```
    {: pre}
7. Check if Cloud Controller can access BBS API like step 3 & step 4. You should get a similar output as below.
    ```
    api/0:/$ nc -zv -w 5 diego-api-set.cf.svc.cluster.local 8889
    Connection to diego-api-set.cf.svc.cluster.local 8889 port [tcp/*] succeeded!
    ```
    {: screen}
8. Environment should be ready for CF app staging.


## CF AutoScaler pods down
{: #autoscaler_debug}
### Monitoring Alert
- CFAutoScaler: autoscaler pods down

### What's happening

The App-Autoscaler provides the capability to adjust the computation resources for Cloud Foundry applications. Sometimes if one or more autoscaler pods run into an unresponsive status, will resulting apps failed to be monitored and scaled by autoscaler service. Users need to restart failed pods to bring the environment back.

### Impact

Apps will no longer be monitored and scaled by autoscaler service.

### How to Fix

The error means that some of autoscaler pods are down.
1. Make sure autoscaler is available by checking autoscaler-x pod status. You should get a similar output as below.
  ```
  kubectl get pods --namespace cf
  ```
  {: pre}
2. As example you should see that 6 autoscaler pods are running.
  ```
  NAME                   READY     STATUS    RESTARTS   AGE
  autoscaler-actors-0    1/1       Running   0          25d
  autoscaler-actors-1    1/1       Running   0          25d
  autoscaler-api-0       1/1       Running   0          14d
  autoscaler-api-1       1/1       Running   0          14d
  autoscaler-metrics-0   1/1       Running   0          25d
  autoscaler-metrics-1   1/1       Running   0          25d
  ```
  {: screen}
3. If one of the pods in the output above is not running, try to recreate it. Use the command below but replace the pod name with the name of unresponsive pods:
  ```
  kubectl delete pod autoscaler-<pod> --namespace cf
  ```
  {: screen}
4. Wait at least 1 minute and verify the alert disappears from Prometheus.
5. Go to the [{{site.data.keyword.Bluemix_notm}} Cloud Foundry dashboard](https://cloud.ibm.com/dashboard/cloudfoundry?filter=cf_environments) and open the {{site.data.keyword.cfee_full_notm}} where you want to check the actual status of Autoscaler.
6. In the {{site.data.keyword.cfee_full_notm}} user interface, go to the **Operations** entry in the left navigation pane and click on **Health check** entry to open the _Health check_ page. The status of Autoscaler should be **No known issues**.
7. Autoscaler service should be ready.

## CF API down
{: #cfapi_debug}
### Monitoring Alert
- CF:API-target down

### Impact

The API endpoint of the CFEE is down and user is not able to connect to the CFEE environment.

### How to Fix

1. Find your cluster in https://cloud.ibm.com/resources. It usually looks like `<your CFEE name>-cluster`.
2. Select the cluster and follow the instruction in `Access` tab to setup the connection to your cluster.
3. Run
  ```
  curl https://api.<your domain>/v2/info
  ```
  {: pre}
4. When you get a similar result below and the alert is still there, it could be a private network problem. Please go to [Enable alb](#Enable-alb) and check if private alb is disabled.
  ```
  {
  "name": "IBM Cloud Foundry Enterprise Environment",
  "build": "2.7.1-rc.15",
  "support": "http://ibm.biz/bluemix-supportinfo",
  "version": 2,
  "description": "Kubernetes based Cloud Foundry",
  "authorization_endpoint": "https://iam.cloud.ibm.com/cloudfoundry/login/62f5xxx",
  "token_endpoint": "https://uaa.cfee-cluster.us-south.containers.appdomain.cloud:2793",
  "min_cli_version": null,
  "min_recommended_cli_version": null,
  "api_version": "2.115.0",
  "app_ssh_endpoint": "ssh.cfee-cluster.us-south.containers.appdomain.cloud:2222",
  "app_ssh_host_key_fingerprint": "27:96:a6:79:5e:c4:30:49:60:1d:f5:fa:7e:53:91:0f",
  "app_ssh_oauth_client": "ssh-proxy",
  "doppler_logging_endpoint": "wss://doppler.cfee-cluster.us-south.containers.appdomain.cloud:4443"
}

  ```
  {: screen}
5. When the result is
  ```
  Could not resolve host: api.<your domain>
  ```
  {: screen}
  go to [Enable ALB](#Enable-alb) and check if the ALBs are disabled. If you are using private IP, please also check your DNS configuration.
6. When the result is
  ```
  curl: (7) Failed to connect to api.<your domain> port 443: Operation timed out
  ```
  {: screen}
  go to [Restart IKS load balance pods](#Restart-IKS-load-balance-pods).
7. When the result is `502 Bad Gateway` or `Unable to fetch upstream endpoints from svc`, go to [Reboot CC](#Reboot-CC)

### Enable ALB
{: #Enable-alb}

1. Run the command below to check if all ALBs are enabled:
  ```
  ibmcloud ks albs --cluster <cluster_name>
  ```
  {: pre}
2. You should get a similar output as below:
  ```
  OK
  ALB ID                                            Enabled   Status     Type       
  private-cr8dcd643f01d34ab4a8d5b427a620ada6-alb1   false     disabled   private   
  public-cr8dcd643f01d34ab4a8d5b427a620ada6-alb1    false     disabled   public      
  ```
  {: screen}
3. Run the command below to enable the disabled ALBs:
  ```
  ibmcloud ks alb-configure --albID <ALB ID> --enable
  ```
  {: pre}
4. Wait several minutes and run the following command to make sure all IKS load balance pods started:
  ```
  kubectl --namespace kube-system get pods | grep alb
  ```
  {: pre}

5. This is an example that shows all pods started
  ```
  private-cr8dcd643f01d34ab4a8d5b427a620ada6-alb1-857d87ffbbhrm2k   4/4       Running   0          4h
  private-cr8dcd643f01d34ab4a8d5b427a620ada6-alb1-857d87ffbblqwjx   4/4       Running   0          4h
  public-cr8dcd643f01d34ab4a8d5b427a620ada6-alb1-7fc8ccc698-g74ng   4/4       Running   0          7m
  public-cr8dcd643f01d34ab4a8d5b427a620ada6-alb1-7fc8ccc698-t8wlz   4/4       Running   0          7m
  ```
  {: screen}
6. Run the following to verify the API recovery:
  ```
  curl https://api.<your domain>/v2/info
  ```
  {: pre}
7. Wait at least 1 minute and verify the alert disappears from Prometheus. If the alert still there, please go to [Restart IKS load balance pods](#Restart-IKS-load-balance-pods).

### Restart IKS load balance pods
{: #Restart-IKS-load-balance-pods}

1. Run the following to get all the IKS load balance pods.
  ```
  kubectl get pod --namespace kube-system grep alb
  ```
  {: pre}

  Here is an example output:
  ```
  private-cr8dcd643f01d34ab4a8d5b427a620ada6-alb1-857d87ffbbhrm2k   4/4       Running   0          4h
  private-cr8dcd643f01d34ab4a8d5b427a620ada6-alb1-857d87ffbblqwjx   4/4       Running   0          4h
  public-cr8dcd643f01d34ab4a8d5b427a620ada6-alb1-7fc8ccc698-g74ng   4/4       Running   0          7m
  public-cr8dcd643f01d34ab4a8d5b427a620ada6-alb1-7fc8ccc698-t8wlz   4/4       Running   0          7m
  ```
  {: screen}
2. Run the following command to delete all the IKS load balance pods. Kubernetes will recreate them automatically.
  ```
  kubectl --namespace kube-system delete pod <pod name>
  ```
  {: pre}
3. Run `kubectl get pod --namespace kube-system | grep alb` again to check all the IKS load balance pods started.
4. Run `curl https://api.<your domain>/v2/info` to verify the API recovery.
5. Wait at least 1 minute and verify the alert disappears from Prometheus. If the alert still there please submit a ticket at https://cloud.ibm.com/unifiedsupport/supportcenter to IKS team and let them check the network of your cluster. Your cluster name can be found in https://cloud.ibm.com/resources. It usually looks like `<your CFEE name>-cluster`.

### Reboot CC
{: #Reboot-CC}

1. Run following command to check if Cloud Controller is unavailable.
  ```
  kubectl get pod --namespace cf
  ```
  {: pre}
  You should get a similar output as below.
  ```
  # kubectl get pod --namespace cf
  NAME                            READY   STATUS      RESTARTS   AGE
  api-group-0                     0/1     Running     0          1d
  api-group-1                    0/1     Running     0          1d
  ```
  {: screen}
2. Run command `kubectl delete pod api-group-x --namespace cf` to delete all `api-group-x` pods . Kubernetes will recreate all of them automatically.
3. Wait until all `api-group-x` pods are running and 1/1 ready.
  ```
  # kubectl get pod --namespace cf
  NAME                            READY   STATUS      RESTARTS   AGE
  api-group-0                     1/1     Running     0          1m
  api-group-1                     1/1     Running     0          1m
  ```
  {: screen}
4. Run `curl https://api.<your domain>/v2/info` to verify the API recovery.
5. Wait at least 1 minute and verify the alert disappears from Prometheus.
6. If after 3-5 minutes the result of step 3 still looks like below, please go to [Check DB](#Check-DB)
  ```
  # kubectl get pod --namespace cf
  NAME                            READY   STATUS      RESTARTS   AGE
  api-group-0                     0/1     Running     0          5m
  api-group-1                     0/1     Running     0          5m
  ```
  {: screen}

### Check DB
{: #Check-DB}

1. If pod `api-group-x` still can't started, there might be a DB problem. Run following command to investigate.
  ```
  kubectl --namespace cf exec -it api-group-0 bash
  ```
  {: pre}
2. Check the logs for cloud_controller component.
  ```
  api-group/0:/# tail /var/vcap/sys/log/cloud_controller_ng/cloud_controller_ng.log
  ```
  {: pre}

If you find some DB error like `Encountered error: PG::ConnectionBad: could not connect to server`, this means your CFEE instance has problem to connect to PostgresDB. Please submit a ticket at https://cloud.ibm.com/unifiedsupport/supportcenter to ask support checking the PostgresDB. Your DB name can be found in https://cloud.ibm.com/resources. It usually looks like `<your CFEE name>-postgres`.

## Database not responding
{: #database_debug}
### Monitoring Alert
- CF:External-DatabaseNotResponding

### How to fix

1. Run following command to check if Cloud Controller are running.
  ```
  kubectl get pod --namespace cf
  ```
  {: pre}
2. You should get a similar output as below.
  ```
  # kubectl get pod --namespace cf
  NAME                            READY   STATUS      RESTARTS   AGE
  api-group-0                     0/1     Running     0          1d
  api-group-1                    0/1     Running     0          1d
  ```
  {: screen}
3. If the status for the pods `api-group-x` is not Running, there might be a DB problem. Run following commands to investigate:
  ```
  kubectl --namespace cf exec -it api-group-0 bash
  ```
  {: pre}
  ```
  api-group/0:/# tail /var/vcap/sys/log/cloud_controller_ng/cloud_controller_ng.log
  ```
  {: pre}

If you find any DB errors like `Encountered error: PG::ConnectionBad: could not connect to server`, this indicates that your CFEE instance have problems connecting to PostgresDB. Before opening a support ticket to report that, please check the [IBM Cloud Status](https://cloud.ibm.com/status) page if there is any ongoing issues in IBM Cloud Databases service (ICD). Otherwise, please submit a ticket at https://cloud.ibm.com/unifiedsupport/supportcenter to report the issue. Please add all necessary information to the ticket including your DB name which can be found in https://cloud.ibm.com/resources. It usually looks like `<your CFEE name>-postgres`.

## High resource usage for cells
{: #cellusage_debug}
### Monitoring Alert
- CF:HighDiskUsageForCells / CF:HighMemoryUsageForCells / CF:HighContainersUsageForCells

### What's happening

The resource usage on the cell is high. You need to take action to reduce the resource usage or scale up your {{site.data.keyword.cfee_full}}. Otherwise, running apps or provisioning new apps might be impacted if there is no free resources left.

### How to fix it

1. Check the usage of resources for your CFEE instance using existing documentation: [Resource usage](https://cloud.ibm.com/docs/cloud-foundry/manage-capacity.html)
2. You can also check the resource usage by commands `cf apps` and `cf app <APP_NAME>`.
3. When there are applications that are no longer in use, you can clean them up by deleting them `cf delete <APP_NAME>` command.
4. You can also use `cf scale` command to scale down apps, and therefore, reduce the occupied memory by your apps.
5. Try if scaling of your CFEE instance can resolve the issue: [Scaling the CFEE infrastructure](https://cloud.ibm.com/docs/cloud-foundry/updating-scaling.html#scale)

## High number of bad gateways
{: #badgw_debug}
### Monitoring Alert
- CF:HighNumberOfBadGateways

### What's happening

This alert means that gorouter gets to requests of bad gateway. If the per-second rate of HTTP bad requests as measured over the last 5 minutes is bigger than 1, you will get a warning alert and when it is bigger than 5 you will get an error alert. The reasons for the alerts are: 
1. the cell does not send the correct routing information to gorouter
2. there are some issues with your app
3. the gorouter is out of sync of routing table. 
You need to investigate the log of the gorouter to find out the error record and fix it.

### How to fix it

1. From **Alerts** tab on Prometheus, expand the alert, from the label `bosh_job_id`, you can get the information of which gorouter is reporting the problem. You can connect to the gorouter and analyze the log to find the problem and take proper action to fix it as described in the next steps..
2. Find your cluster in https://cloud.ibm.com/resources. It usually looks like `<your CFEE name>-cluster`.
3. Click the cluster and follow the instruction in `Access` tab to setup the connection to your cluster.
4. Run command `kubectl --namespace cf exec -it <router> bash` to connect to the gorouter pod. For this command use the identified router name from Step 1.
5. Run command `tail /var/vcap/sys/log/gorouter/access.log` and you will see output like:
  ```
  ...
  rubytest.appmonitor-cluster.us-south.containers.appdomain.cloud - [2019-05-09T07:43:59.862+0000] "GET / HTTP/1.1" 502 0 67 
  "-"    "curl/7.54.0" "172.30.190.193:46693" "172.30.190.202:61003" x_forwarded_for:"10.74.47.98, 172.30.190.193"
  x_forwarded_proto:"http"  vcap_request_id:"94cfa737-25aa-4f9f-744e-1f815117be52" response_time:0.00297709 
  app_id:"02fea509-b27e-4a42-b81d-25fbc8125189"   app_index:"0" x_b3_traceid:"31f58cd910f71f62" x_b3_spanid:"31f58cd910f71f62" x_b3_parentspanid:"-"
  ...
  ```
  {: screen}
6. In the log above, you can see return code `502` after `"GET / HTTP/1.1"`. This indicate a 502 bad gate error in this router. `rubytest.appmonitor-cluster.us-south.containers.appdomain.cloud` indicate the app URL that have the problem. So this message means a routing record for app `rubytest` is not correct in the routing table. 
7. You can restart app `rubytest` and continue check `/var/vcap/sys/log/gorouter/access.log` to see whether the error message still shown. If the error message disappears, wait about 5 minutes and you will see the alert disappears too. 
8. If the error still occurs after you restarted the app, this means there's something wrong with your cell, you need restart your cell to make it work properly again. The second IP from the log above "172.30.190.202:61003" indicates the IP of the cell. You can use `kubectl get pod  --namespace cf -o wide | grep 172.30.190.203` to get the pod name and restart the pod. 
*Note: before your restart the cell, please make sure other cells have enough resources to accept the instances from the rebooting cell. Otherwise  instances in this cell will be impacted for several minutes. To avoid this, you can refer to [Updating and scaling](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-update-scale#scale) to scale up your CFEE.* 
Here is the full example:
  ```
  #kubectl get pod  --namespace cf -o wide | grep 172.30.190.203
  diego-cell-0                    1/1     Running     0          72m     172.30.190.203   10.74.47.98    <none>           <none>
  #kubectl --namespace cf delete pod diego-cell-0 
  pod "diego-cell-0" deleted
  ```
  {: screen}
9. After the new cell started, the alert should disappear in about 5 minutes.


## High number of rejected requests
{: #rejectedreq_debug}
### Monitoring Alert
- CF:HighNumberOfRejectedRequests

### What's happening

This alert means that gorouter gets to many bad requests. If the per-second rate of HTTP bad requests as measured over the last 5 minutes is bigger than 1, you will get a warning alert and when it is bigger than 5 you will get an error alert. This often means your app is not working  properly. You need to take a look into the log of the gorouter and find out which app causes the error and fix it.

### How to fix it

From `Alerts` tab of Prometheus, expand the alert, from the label `bosh_job_id`, you can get the information of which gorouter is reporting the problem. You can connect to the gorouter and analyze the log to find the problem and take proper action to fix it. Here's an example for fixing 404 error.

1. Find your cluster in https://cloud.ibm.com/resources. It usually looks like `<your CFEE name>-cluster`. 
2. Click the cluster and follow the instruction in `Access` tab to setup the connection to your cluster.
3. Run command `kubectl --namespace cf exec -it <router> bash` to connect to the gorouter pod. Replace the router with the content of label `bosh_job_id` from Prometheus alert you have received.
4. Run command `tail /var/vcap/sys/log/gorouter/access.log` and you will get an output like:
  ```
  ...
  rubytest.appmonitor-cluster.us-south.containers.appdomain.cloud - [2019-05-09T06:13:48.372+0000] "GET /test HTTP/1.1" 404 0 121 
  "-" "curl/7.54.0" "172.30.190.193:33299" "-" x_forwarded_for:"10.74.47.98" x_forwarded_proto:"http"
  vcap_request_id:"673f62e8-2069-4ae6-5ffa-beeb79c31f72" response_time:0.000201752 app_id:"-" app_index:"-"
  x_b3_traceid:"e7e752a1899acdb9" x_b3_spanid:"e7e752a1899acdb9" x_b3_parentspanid:"-"
  ...
  ```
  {: screen}
Here  `rubytest.appmonitor-cluster.us-south.containers.appdomain.cloud` indicate the app URL that have the problem and the error code is `404`(the error code is after `"GET /test HTTP/1.1"`). For this message, it means  your app `rubytest` is not in the routing table. This is mostly caused by app down issue. Please find the app in your CFEE instance and restart the app. 
5. After you fix all apps in error messages you get from previous step, the alert should disappear in about 5 minutes. 

## Getting help and support
{: #ts_getting_help}

Still having issues with your {{site.data.keyword.cfee_full}}?
{: shortdesc}

-  In the terminal, you are notified when updates to the `ibmcloud` CLI and plug-ins are available. Be sure to keep your CLI up-to-date so that you can use all the available commands and flags.
-   To see whether {{site.data.keyword.Bluemix_notm}} is available, [check the {{site.data.keyword.Bluemix_notm}} status page ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/status?selected=status).
-   From the console, check if you have any relevant **Notifications**. <!-- ![Notifications icon](../icons/Notification_PUP.svg "Notifications icon"). -->
-   Contact IBM Support by opening a case. To learn about opening an IBM support case, or about support levels and case severities, see [Contacting support](/docs/get-support?topic=get-support-getting-customer-support#getting-customer-support).
When you report an issue, include your cluster ID and CFEE instance ID. To get your cluster ID, run `ibmcloud ks clusters`. To get your CFEE instance ID, run `ibmcloud cfee environments`.
{: tip}
