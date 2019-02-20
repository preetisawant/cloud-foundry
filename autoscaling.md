---

copyright:
  years: 2019
lastupdated: "2019-02-11"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Autoscaling applications
{: #autoscale_cloud_foundry_apps}

{{site.data.keyword.Bluemix}} has a built-in autoscaling support for Cloud Foundry applications to adjust application instance number automatically through 
  * Dynamic scaling based on application performance metrics.
  * Scheduled scaling based on time.

This capability is offered based on Cloud Foundry open source project [App-Autoscaler][autoscaler_project]. Refer to [user guide][autoscaler_user_guide] to get started. 

## Managing autoscaling through CLI

You can use  App Autoscaler command-line interface plugin (aka AutoScaler CLI) to manage policy, query metrics and scaling history. 

### Installing AutoScaler CLI
Use the following command to install `AutoScaler CLI` which is a plugin of Cloud Foundry CLI.  

``` 
cf install-plugin -r CF-Community app-autoscaler-plugin
```
{:codeblock} 

The same command can be used to update `AutoScaler CLI` plugin to the latest version if you have a prior installation. 

### Using the AutoScaler CLI

If you already logged in to a Cloud Foundry environment on {{site.data.keyword.Bluemix}} and have applications running in your space as described in [deploying apps guide][deploy_app], follow steps below to create a scaling policy for your application, and query metrics and scaling history. 

 *  (optional) Confirm the App-Autoscaler API endpoint is set correctly by default.  

    If Cloud Foundry API endpoint is presented as `api.<DOMAIN>`, the App-Autoscaler API endpoint should be `autoscaler.<DOMAIN>`.  
    Use the command below to check the App-Autoscaler API endpoint setting.

    ```
    cf asa
    ```
    {:codeblock} 

    If the App-Autoscaler API endpoint is incorrect, you need to reset it with command:

    ```
    cf asa autoscaler.<DOMAIN>
    ```
    {:codeblock} 


*  Create a policy JSON file on your local machine. 

    ```
    cat > <YOUR_POLICY_FILE> << EOF
    {
            "instance_min_count": 1,
            "instance_max_count": 5,
            "scaling_rules": [
                    {
                            "metric_type": "memoryutil",
                            "breach_duration_secs": 120,
                            "threshold": 80,
                            "operator": ">=",
                            "cool_down_secs": 120,
                            "adjustment": "+1"
                    },
                    {
                            "metric_type": "memoryutil",
                            "breach_duration_secs": 120,
                            "threshold": 10,
                            "operator": "<",
                            "cool_down_secs": 120,
                            "adjustment": "-1"
                    }
            ]
    }
    EOF
    ```
    {:codeblock} 

    The policy above is used to trigger  scaling based on memory utilization  when the defined threshold is breached for at least `120    seconds`.  Refer to [Cloud Foundry App-Autoscaler user guide][autoscaler_user_guide] for how to create your own autoscaling policy.

*  Attach the policy to your application

    ```
    cf aasp <YOUR_APP> <YOUR_POLICY_FILE>
    ```
    {:codeblock} 

*  (optional) Furthermore, you can query the most recent aggregated metrics of your application. App-Autoscaler supports multiple [metric types][metric_type], but only the metrics you defined in your policy could be retrieved, i.e. `memoryutil` in above example.  

    ```
    cf asm <YOUR_APP> <METRIC_TYPE> --desc
    ```
    {:codeblock} 

*  (optional) Use the command below to query scaling history:

    ```
    cf ash <YOUR_APP> --desc
    ```
    {:codeblock} 

    Refer to [Cloud Foundry App Autoscaler CLI plugin guide][autoscaler_cli] for more options to use the command line. 


## Managing Autoscaling through the Stratos console 

Besides the command line interface, you can also manage autoscaling settings through Stratos console . 

If you have installed [stratos][stratos] on your {{site.data.keyword.cfee_full}} (CFEE), go to the **"Auto scaling**" tab in the application dashboard to see an overview of the auto-scaling policy and  most recent scaling events. 
Click any of the icons in any of the tiles to launch the policy editor and edit the policy.

If no auto-scaling policy is defined, the the overview page will have no information.  Click **Create policy** to launch the policy editor and create a policy.

We recommend to go through the [Cloud Foundry App-Autoscaler User Guide][autoscaler_user_guide] to understand the basic concepts to set an auto-scaling policy properly. 

### Metric Statistics

Once you have defined a policy based on one or more selected metric types, you can view the latest metric values, and  metrics history in the last 30 minutes. 

**Note:** Metrics represent data averaged over all the application instances, not raw data from each application instance.
    
### Scaling History

the **History** tab in the policy editor shows scaling actions were taken on your application triggered by the auto-scaling policy. It also shows any error messages resulting from scaling failures. You can query scaling history during the past 30 days. 


[autoscaler_project]: https://github.com/cloudfoundry-incubator/app-autoscaler
[autoscaler_user_guide]: https://github.com/cloudfoundry-incubator/app-autoscaler/blob/master/docs/Readme.md
[autoscaler_cli]: https://github.com/cloudfoundry-incubator/app-autoscaler-cli-plugin#cloud-foundry-cli-autoscaler-plug-in-
[metric_type]:https://github.com/cloudfoundry-incubator/app-autoscaler/blob/master/docs/Readme.md#metric-types
[deploy_app]:https://cloud.ibm.com/docs/cloud-foundry/deploy-apps.html#dep_apps
[stratos]: https://cloud.ibm.com/docs/cloud-foundry/getting-started.html#install-stratos
