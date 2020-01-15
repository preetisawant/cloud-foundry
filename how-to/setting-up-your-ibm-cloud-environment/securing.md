---

copyright:
  years: 2020
lastupdated: "2020-01-14"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Securing your IBM Cloud Foundry Enterprise Environment
{: #securing-your-cfee}

IBM provides several configuration options you can use in order to secure your {{site.data.keyword.cfee_full_notm}} instance and the data contained therein.

Since CFEE is deployed on top of instances of other IBM Cloud services, most of these options are actually accessed by configuring those underlying instances.

## Encryption in Cloud Foundry
{: #cloud-foundry}

Cloud Foundry encrypts key fields stored in its databases (Cloud Controller DB, Diego DB, UAA DB).  {{site.data.keyword.cfee_full_notm}} generates a unique key for each instance which is used for this encryption.  Data stored within these databases is further encrypted by the underlying IBM Cloud Databases for PostgreSQL instance, see [below](#database) for more information.

## Securing your IBM Kubernetes Service cluster
{: #kubernetes-cluster}

To protect sensitive information in the underlying IBM Kubernetes Service cluster, please see the docs for securing your cluster [here](containers?topic=containers-encryption)

## Securing your IBM Cloud Object Storage instance
{: #cloud-object-storage}

IBM Cloud Object Storage provides a default level of encryption but also offers several options to allow customers to configure it in a way that works best for their design and standards.  You can read more about the encryption support in IBM Cloud Object Storage [here](services/cloud-object-storage?topic=cloud-object-storage-encryption).

## Securing your IBM Cloud Databases for PostgreSQL instance
{: #database}

IBM Cloud Databases for PostgreSQL encrypts all data in transit and at rest, including stored backups.  Much like IBM Cloud Object Storage, ICD for PostgreSQL offers an integration option with IBM Key Protect to let the customer control the encryption keys.  You can read about how to configure this [here](services/databases-for-postgresql?topic=cloud-databases-key-protect).
