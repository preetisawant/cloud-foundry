---



copyright:

  years: 2018, 2019

lastupdated: "2019-08-12"



---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:tip: .tip}

# FAQs for {{site.data.keyword.cfee_full_notm}}
{: #cfeefaq}

## What is the difference between {{site.data.keyword.cfee_full_notm}} (CFEE) and public Cloud Foundry?
{: #cfee_diff}

You can use {{site.data.keyword.cloud}} Foundry public to run cloud-native applications that are using Cloud Foundry for simple setup, powerful scaling, and traffic management. You also have easy access to all {{site.data.keyword.cloud}} services.

You can use {{site.data.keyword.cfee_full}} for everything as you would with Cloud Foundry Public, but also to create and manage isolated environments for hosting Cloud Foundry applications exclusively for your enterprise.


## How is this offering different from previous {{site.data.keyword.cloud_notm}} Foundry offerings?
{: #cfOfferings_diff}

With respect to the public multi-tenant the most noteworthy difference is certainly the isolation properties. With respect to the existing single-tenant offering on IBM Cloud infrastructure, the main two differences are the reduced infrastructure footprint (and therefore the cost) as well as the service integration model into such a single-tenant environment.

## Where can I find the CFEE service?
{: #where}

You can find and instantiate the {{site.data.keyword.cfee_full}} service in the {{site.data.keyword.Bluemix_notm}} [catalog](https://cloud.ibm.com/catalog).

## Can I have more than one CFEE environment within a regional data center?
{: #multiple-cfees}

Yes, you can create CFEE instances on-demand, as many as you want in [these regions](https://cloud.ibm.com/docs/cloud-foundry/index.html#provisioning-targets){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon").

## Will I need to start at some minimum capacity?
{: #minimum-capacity}

Yes. Creating a CFEE instance requires a minimum of two Cloud Foundry cells, each with 4 Cores of 16GB RAM, 25GB SSD primary disk, 100GB SSD secondary disk, and 1000Mbps network speed.

## What is the underlying IaaS into which CFEE is deployed?
{: #why-kubs}

The CFEE service runs on Kuberneters containers, which allows for lower infrastructure cost and more efficient operations, since Kubernetes is a very smart IaaS that automates many operational activities.

## What are my isolation options when creating a CFEE?
{: #isolation}

You have two hardware options on the type of Kubernetes infrastructure into which the CFEE instance is deployed: _Virtual shared_ or _Virtual dedicated_ hardware. With _Virtual shared_ hardware, the worker nodes (into which the Cloud Foundry platform container is deployed) is distributed between you and other IBM customers.  With _Virtual dedicated_ the worker nodes are hosted on hardware that is dedicated exlusively to your account.  Note that in both cases, _Virtual shared_ and _Virtual dedicated_, each worker node is single-tenant to the customer.  This means that the Cloud Foundry cells in which applications run are not shared with other customers.

## Can I scale the capacity of a CFEE?
{: #scaling}

Yes, you can scale up or down the capacity of your CFEE as your needs change by adding or removing Cloud Foundry cells.

## Can I upgrade my CFEE to a new version? How does it work?
{: #upgrading}
Yes. The CFEE user interface notifies you when there is a new CFEE versions.  You control when to update to a new version. The CFEE version update is invoked by CFEE administrators in the user interface. CFEE version updates may package new versions of its components or supporting services (e.g., Cloud Foundry, Kubernetes, etc).  You update the CFEE control plane first and then the Cloud Foundry cells.  The update process is optimized to minimize disruption.

## What does it take to create a CFEE instance?
{: #create}

You can find the CFEE service listed in the {{site.data.keyword.Bluemix_notm}} catalog.  You need to have an upgraded {{site.data.keyword.Bluemix_notm}} account and permissions to the CFEE service and its supported services (Kubernetes, Cloud Object Storage and Compose for PostgreSQL).  Once you have those permissions, just provide a name for the environment and click _Create_.  Creation takes approximately 90 minutes.

## Can I use {{site.data.keyword.Bluemix_notm}} services in my CFEE?
{: #Services-ibmcloud}

Definitely!  By being integrated in the {{site.data.keyword.Bluemix_notm}}, developers in a CFEE can create {{site.data.keyword.Bluemix_notm}} service instances (or use existing instances) and bind them to applications deployed in CFEE spaces.

## Can I have my own services services in my CFEE?
{: #Services-ibmcloud}

Yes.  An administrator can register a services broker in the CFEE and make custom service plans available to users in that CFEE.  The local MCFEE marketplace includes the services from the {{site.data.keyword.Bluemix_notm}} catalog plus any customer services managed by the CFEE's local service broker.

## How do I control user access to a CFEE?
{: #Services}

Like any other {{site.data.keyword.Bluemix_notm}} service, access to a CFEE is controlled through _Identity & Access Management_ (IAM). Assigning user access policies (either individually or through access groups) with specific roles gives them specific levels of access to a CFEE.  Beyond access to the CFEE service, access to Cloud Foundry organizations and spaces in the CFEE is controlled through Cloud Foundry membership and roles assigned to users in specific organizations and spaces.

## What standards does the service comply to?
{: #standards}
Delivering a Cloud Foundry environment that meets the growing demands of enterprise security is critical. In support of this, the Cloud Foundry Enterprise product has earned several compliance and regulatory standards to ensure the service meets these critical requirements. This effort ensures that all central components managed by the service team are secured, and that the customer's environment instance can be managed to the same standards - dependent on your actual controls and processes.

IBM Cloud Foundry Enterprise Environment implements controls commensurate with the following standards:
* EU-US Privacy Shield and Swiss-US Privacy Shield Framework
* Health Insurance Portability and Accountability Act (HIPAA)
* General Data Protection Regulation (GDPR)
* Service Organization Control standards (SOC 1, SOC 2 Type 1)
* International Organization for Standardization (ISO 27001, ISO 27017, ISO 27018)

More information is available on the [IBM Cloud Compliance](https://www.ibm.com/cloud/compliance) page.

## What options do I have to secure my CFEE instance?
{: #secure}
As part of managing your CFEE instance, it is necessary to take precausions to monitor and secure the Kubernetes cluster that the CFEE is deployed on.  More information about how to secure your Kubernetes cluster is available in the IBM Cloud Kubernetes Service [FAQ](https://cloud.ibm.com/docs/containers?topic=containers-faqs&locale=en-us#secure_cluster) and [documentation](https://cloud.ibm.com/docs/containers?topic=containers-security&locale=en-us#security).
