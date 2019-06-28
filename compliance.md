---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}


# Protecting sensitive data
{: #compliance}

The {{site.data.keyword.cfee_full}} (CFEE) is a platform-as-a-service. As such, the client is free to use the service instance for anything it is capable of supporting. The CFEE and dependent services have access to the least amount of personal data as possible.

It should be made clear, however, that even though the CFEE control plane (via UI/API/CLI) will not be processing sensitive data (e.g., HIPAA data), it is the responsibility of the client to ensure that that they use their CFEE responsibly, since all dependencies are managed and owned by the customers in their {{site.data.keyword.Bluemix_notm}} account. 

We recommend the following best practices:
*  Not to modify the dependent services created with a CFEE (Kubernetes, Cloud Object Storage, and Compose for PostgreSQL).
*  Updating and managing the CFEE through the CFEE service itself (user interface or command line interface), rather than through the Kubernetes service.

The Kubernetes cluster is used to hold the majority of the CFEE infrastructure, as well as all the applications running on the CFEE, since the Cloud Foundry cells are deployed on top of Kubernetes nodes. This cluster is owned and managed by the customer's account.

The Compose for PostgreSQL database is used by CFEE to hold metadata about organizations, spaces, users, and roles. If the CFEE instance is used as recommended, there will be no sensitive data exposed. However, if a client decides to name their organizations and spaces with personal or sensitive information about their customers, then the PostgreSQL database could contain HIPAA or other type of sensitive information.

The Cloud Object Storage instance is used by CFEE to hold an application's droplets, so that they can be deployed, stopped, started, etc. This means that the Cloud Object Storage instance is not running the application, just holding it's image. Therefore, if the Cloud Object Storage instance is used following best practices, it will not hold any HIPAA sensitive information. The customer has a responsibility to ensure no personal data is hardcoded into any of their application (test data, etc.).
