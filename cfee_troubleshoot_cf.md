---

copyright:
  years: 2019
lastupdated: "2019-04-29"

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

Bulletin Board System (BBS) run in active/passive mode and it maintains a lock in Locket to ensure that only one BBS is active. Sometimes if Locket loses connection with back-end database, it may run into an unresponsive status. In this case, no active BBS is elected and then BBS API is not accessible, and operations like cf push app will fail as Cloud Controller cannot communicate with BBS API.
In CFEE 2.x, Diego BBS and Locket run in diego-api-x pod, so users need to restart all diego-api-x pods to bring the environment back.

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
1. Make sure Cloud Controller is available by checking api-x pod status.
    ```
    kubectl get pod -n cf
    ```
    {: pre}
2. For example, the output indicates that 2 api-x pods are running.
    ```
    NAME                            READY   STATUS      RESTARTS   AGE
    api-0                           2/2     Running     0          1d
    api-1                           2/2     Running     0          1d
    ```
    {: screen}
3. Go into api-0 pod.
    ```
    kubectl exec -ti api-0 bash -n cf
    ```
    {: pre}
4. In api-0 pod, if you get an error like below, it indicates that Cloud Controller cannot access BBS.
    ```
    nc -zv diego-api.cf.svc.cluster.local 8889

    ```
    {: pre}
    - For example, the output indicates that connection failed:
    ```
    nc: connect to diego-api.cf.svc.cluster.local port 8889 (tcp) failed: Connection timed out
    ```
    {: screen}
5. Exit api-0 and then delete all diego-api-x pods as below. Kubernetes will recreate all of them automatically.
    ```
    kubectl delete pod diego-api-0 -n cf
    ```
    {: pre}
    Before CFEE 2.0, Diego Lockets are located in separate pods named diego-locket-x. If this is the case, please restart all diego-locket-x pods like step 5.

6. Wait until all diego-api-x pods are `running` and `2/2` ready. Make sure one of diego-api-x pods is labeled as active.
    ```
    kubectl get pod  -n cf -L skiff-role-active
    ```
    {: pre}
7. Check if Cloud Controller can access BBS API like step 3 & step 4. You should get a similar output as below.
    ```
    api/0:/$ nc -zv diego-api.cf.svc.cluster.local 8889
    Connection to diego-api.cf.svc.cluster.local 8889 port [tcp/*] succeeded!
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

Apps failed to be monitored and scaled by autoscaler service.

### How to Fix

The error means that some of autoscaler pods are down.
1. Make sure autoscaler is available by checking autoscaler-x pod status. You should get a similar output as below.
  ```
  kubectl get pod -n cf
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
3. If one of the pods in the output above is not running, try to recreate it. Use the command below but replace the pod name with
the name of unresponsive pods:
  ```
  kubectl delete pod autoscaler-<pod> -n cf
  ```
  {: screen}

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
4. When you get a meaningful result like below and the alert is still there, this means a private network problem. Please go to [Enable alb](#Enable-alb) and check if private alb is disabled.
  ```
  {"name":"IBM Cloud Foundry Enterprise Environment","build":"2.7.1-rc.15","support":"http://ibm.biz/bluemix-   supportinfo","version":2,"description":"Kubernetes based Cloud Foundry","authorization_endpoint":"https://iam.bluemix.net/cloudfoundry/login/62f5xxx","token_endpoint":"https://uaa.cfee-cluster.us-south.containers.appdomain.cloud:2793","min_cli_version":null,"min_recommended_cli_version":null,"api_version":"2.115.0","app_ssh_endpoint":"ssh.cfee-cluster.us-south.containers.appdomain.cloud:2222","app_ssh_host_key_fingerprint":"27:96:a6:79:5e:c4:30:49:60:1d:f5:fa:7e:53:91:0f","app_ssh_oauth_client":"ssh-proxy","doppler_logging_endpoint":"wss://doppler.cfee-cluster.us-south.containers.appdomain.cloud:4443"}
  ```
  {: screen}
5. When the result is
  ```
  Could not resolve host: api.<your domain>
  ```
  {: screen}
  go to [Enable ALB](#Enable-alb) and check if the ALBs are disabled. If you are using private IP, please also check your DNS     configuration.
6. When the result is
  ```
  curl: (7) Failed to connect to api.<your domain> port 443: Operation timed out
  ```
  {: screen}
  go to [Restart IKS load balance pods](#Restart-IKS-load-balance-pods).
7. When the result is `502 Bad Gateway` or `Unable to fetch upstream endpoints from svc`, go to [Reboot CC](#Reboot-CC)

### Enable ALB
{: #Enable-alb}

1. Run command below to check if all ALBs are enabled.
  ```
  ibmcloud ks albs --cluster <cluster_name>
  ```
  {: pre}
2. You should get a similar output as below.
  ```
  OK
  ALB ID                                            Enabled   Status     Type       
  private-cr8dcd643f01d34ab4a8d5b427a620ada6-alb1   false     disabled   private   
  public-cr8dcd643f01d34ab4a8d5b427a620ada6-alb1    false     disabled   public      
  ```
  {: screen}
3. Run command below to enable the disabled ALBs.
  ```
  ibmcloud ks alb-configure --albID <ALB ID> --enable
  ```
  {: pre}
4. Wait several minutes and run
  ```
  kubectl -n kube-system get pod | grep alb
  ```
  {: pre}
  to make sure all IKS load balance pods started. 
5. This is an example that shows all pods started
  ```
  private-cr8dcd643f01d34ab4a8d5b427a620ada6-alb1-857d87ffbbhrm2k   4/4       Running   0          4h
  private-cr8dcd643f01d34ab4a8d5b427a620ada6-alb1-857d87ffbblqwjx   4/4       Running   0          4h
  public-cr8dcd643f01d34ab4a8d5b427a620ada6-alb1-7fc8ccc698-g74ng   4/4       Running   0          7m
  public-cr8dcd643f01d34ab4a8d5b427a620ada6-alb1-7fc8ccc698-t8wlz   4/4       Running   0          7m
  ```
  {: screen}
6. Run
  ```
  curl https://api.<your domain>/v2/info
  ```
  {: pre}
  to verify the API recovery.
7. Wait at least 1 minute and verify the alert disappears from Prometheus. If the alert still there please go to [Restart IKS load balance pods](#Restart-IKS-load-balance-pods).

### Restart IKS load balance pods
{: #Restart-IKS-load-balance-pods}

1. Run
  ```
  kubectl get pod -n kube-system grep alb
  ```
  {: pre}
  to get all the IKS load balance pods. Here is an example output:
  ```
  private-cr8dcd643f01d34ab4a8d5b427a620ada6-alb1-857d87ffbbhrm2k   4/4       Running   0          4h
  private-cr8dcd643f01d34ab4a8d5b427a620ada6-alb1-857d87ffbblqwjx   4/4       Running   0          4h
  public-cr8dcd643f01d34ab4a8d5b427a620ada6-alb1-7fc8ccc698-g74ng   4/4       Running   0          7m
  public-cr8dcd643f01d34ab4a8d5b427a620ada6-alb1-7fc8ccc698-t8wlz   4/4       Running   0          7m
  ```
  {: screen}
2. Run the next command to delete all the IKS load balance pods. Kubernetes will recreate all of them automatically.
  ```
  kubectl -n kube-system delete pod <pod name>
  ```
  {: pre}
  to delete all the IKS load balance pods. Kubernetes will recreate all of them automatically.
3. Run `kubectl get pod -n kube-system grep alb` again to check all the IKS load balance pods started.
4. Run `curl https://api.<your domain>/v2/info` to verify the API recovery.
5. Wait at least 1 minute and verify the alert disappears from Prometheus. If the alert still there please submit a ticket at https://cloud.ibm.com/unifiedsupport/supportcenter to IKS team and let them check the network of your cluster. Your cluster name can be found in https://cloud.ibm.com/resources. It usually looks like `<your CFEE name>-cluster`.

### Reboot CC
{: #Reboot-CC}

1. Run following command to check if Cloud Controller is unavailable.
  ```
  kubectl get pod -n cf
  ```
  {: pre}
  You should get a similar output as below.
  ```
  # kubectl get pod -n cf
  NAME                            READY   STATUS      RESTARTS   AGE
  api-group-0                     0/1     Running     0          1d
  api-group-1                    0/1     Running     0          1d
  ```
  {: screen}
2. Run command `kubectl delete pod api-group-x -n cf` to delete all `api-group-x` pods . Kubernetes will recreate all of them automatically.
3. Wait until all `api-group-x` pods are running and 1/1 ready.
  ```
  # kubectl get pod -n cf
  NAME                            READY   STATUS      RESTARTS   AGE
  api-group-0                     1/1     Running     0          1m
  api-group-1                     1/1     Running     0          1m
  ```
  {: screen}
4. Run `curl https://api.<your domain>/v2/info` to verify the API recovery.
5. Wait at least 1 minute and verify the alert disappears from Prometheus.
6. If after 3-5 minutes the result of step 3 still looks like below, please go to [Check DB](#Check-DB)
  ```
  # kubectl get pod -n cf
  NAME                            READY   STATUS      RESTARTS   AGE
  api-group-0                     0/1     Running     0          5m
  api-group-1                     0/1     Running     0          5m
  ```
  {: screen}

### Check DB
{: #Check-DB}

1. If pod `api-group-x` still can't started, there might be a DB problem. Run following command to investigate.
  ```
  kubectl -n cf exec -it api-group-0 bash
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
  kubectl get pod -n cf
  ```
  {: pre}
2. You should get a similar output as below.
  ```
  # kubectl get pod -n cf
  NAME                            READY   STATUS      RESTARTS   AGE
  api-group-0                     0/1     Running     0          1d
  api-group-1                    0/1     Running     0          1d
  ```
  {: screen}
3. If the status for the pods `api-group-x` is not Running, there might be a DB problem. Run following commands to investigate:
  ```
  kubectl -n cf exec -it api-group-0 bash
  ```
  {: pre}
  ```
  api-group/0:/# tail /var/vcap/sys/log/cloud_controller_ng/cloud_controller_ng.log
  ```
  {: pre}

If you find some DB error like `Encountered error: PG::ConnectionBad: could not connect to server`, this means your CFEE instance has problem to connect to PostgresDB. Please submit a ticket at https://cloud.ibm.com/unifiedsupport/supportcenter to ask support checking the PostgresDB. Your DB name can be found in https://cloud.ibm.com/resources. It usually looks like `<your CFEE name>-postgres`.

## High resource usage for cells
{: #cellusage_debug}
### Monitoring Alert
- CF:HighDiskUsageForCells / CF:HighMemoryUsageForCells / CF:HighContainersUsageForCells

### What's happening

The resource usage on the cell is high. You need to take action to reduce the resource usage or scale up your {{site.data.keyword.cfee_full}}. Otherwise the apps in this cell might be impacted. If there's not enough resources in all cells you may not be able to push new applications and the running applications could be also impacted.

### How to fix it

1. Check the usage of resouces for your CFEE instance using existing documentation: [Resource usage](https://cloud.ibm.com/docs/cloud-foundry/manage-capacity.html)
2. You can also check the resource usage by commands `cf apps` and `cf app <APP_NAME>`.
3. When there are applications no longer used, you can remove them using `cf delete <APP_NAME>` command.
4. You can also use `cf scale` command to reduce the memory usage of your apps.
5. Try if scaling of your CFEE instance can resolve the issue: [Scaling the CFEE infrastructure](https://cloud.ibm.com/docs/cloud-foundry/updating-scaling.html#scale)

## High number of bad gateways
{: #badgw_debug}
### Monitoring Alert
- CF:HighNumberOfBadGateways

## High number of rejected requests
{: #rejectedreq_debug}
### Monitoring Alert
- CF:HighNumberOfRejectedRequests


## Getting help and support
{: #ts_getting_help}

Still having issues with your {{site.data.keyword.cfee_full}}?
{: shortdesc}

-  In the terminal, you are notified when updates to the `ibmcloud` CLI and plug-ins are available. Be sure to keep your CLI up-to-date so that you can use all the available commands and flags.
-   To see whether {{site.data.keyword.Bluemix_notm}} is available, [check the {{site.data.keyword.Bluemix_notm}} status page ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/status?selected=status).
-   From the console, check if you have any relevant **Notifications**. <!-- ![Notifications icon](../icons/Notification_PUP.svg "Notifications icon"). -->
-   Contact IBM Support by opening a case. To learn about opening an IBM support case, or about support levels and case severities, see [Contacting support](/docs/get-support?topic=get-support-getting-customer-support#getting-customer-support).
When you report an issue, include your cluster ID. To get your cluster ID, run `ibmcloud ks clusters`.
{: tip}
