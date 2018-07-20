---

copyright:
  years: 2018
lastupdated: "2018-07-17"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Preparing your account
{: #prepare}

ICFEE instances are deployed on infrastructure resources (Kubernetes worker nodes from the IBM Container service) that are billed to the IBM Cloud account. This means that the IBM Cloud account under which the ICFEE instance is created must be a paid account (Pay-As-You-Go or a Subscription account).  If the IBM Cloud account under which you intend to create an ICFEE instance is a trial  account you will be asked to upgrade the account when you try to create an ICFEE instance.  When an IBM Cloud account is upgraded (from a trial account to a Pay-As-You-Go or a Subscription account), the IBM Cloud account becomes linked to a SoftLayer account (through which infrastructure resources can be created). For more information, see [Account types](https://console.bluemix.net/docs/account/index.html#accounts). The cost of those infrastructure resources shows up in your IBM Cloud invoice.

## How to determine if the IBM Cloud account can create ICFEE instances
{: #account-check}

You can determine if a IBM Cloud account is a trial or paid account, and whether it is linked to a SoftLayer account, by looking at the account information at the top right corner of the IBM Cloud banner.  

In the example below user _Mary Smith_ is logged into the IBM Cloud account _MyCompany_, which is a trial account.
![Account Checking](img/AccountExample_1.png)

In the example below the same IBM Cloud account _MyCompany_ has been upgraded to a paid account.  As a result of the upgrade the account is now linked to the SoftLayer account _1684806_.  Both accounts are shown in the "Account" field.
![Account Checking](img/AccountExample_2.png)

## Switching the SoftLayer account linked to the IBM Cloud account
{: #account-linkswitching}

If you have Administrator role in an IBM Cloud account you can set the SoftLayer account to which that IBM Cloud account is linked. This would allow users in an IBM Cloud account to use an existing SoftLayer account to create the infrastructure resources that support ICFEE instances.

**Warning:**  Switching the SoftLayer account linked to the IBM Cloud account (by issuing  the commands that follow) can prevent users to access infrastructure resources previously provisioned under the SoftLayer account to which the IBM Cloud account was previously linked.  We recommend not to switch the SoftLayer account linked to an upgraded IBM Cloud account.

To manually link an IBM Cloud account to a SoftLayer account:

1. Get the SofLayer account's user name and API Key by accessing the [SoftLayer console](https://control.softlayer.com). Once you log in to SoftLayer, select the account you want to link to the {{site.data.keyword.Bluemix_notm}} account. Selecting the account opens the account's profile page. Scroll down to the end of the page to find the account's user name and API key. If you don't have an API key, you can generate it if you're the account owner. If you're not the account owner, ask the account owner to generate it.
2. Log in to {{site.data.keyword.Bluemix_notm}} from the command line. If your organization uses a federated login, you might need to use the `-sso` option.

  ```
  ibmcloud login
  ```

3. In the command line interface, set the API endpoint to the us-south region of the IBM Cloud:

  ```
  ibmcloud api https://api.ng.mybluemix.net
  ```

4. Set your SoftLayer credentials in the IBM Container Service registry:

  ```
  ibmcloud cs credentials-set --infrastructure-username <SofLayer_username> --infrastructure-api-key <SoftLayer_api_key>
  ```

**Note:** You must have sufficient permissions in the SoftLayer account to create a regular Kubernetes cluster from the IBM Container service. If you don't, ask the SoftLayer account administrator, or the user who gave you access to the SoftLayer account to grant you those additional permissions.
