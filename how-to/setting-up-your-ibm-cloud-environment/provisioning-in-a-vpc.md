---

copyright:
  years: 2019
lastupdated: "2019-09-01"
---

# CFEE on IBM Virtual Private Cloud (VPC)
{: #cfee-on-vpc}

You can provision IBM Cloud Foundry Enterprise Environment into your IBM Virtual Private Cloud (VPC).

VPC allows you to create your own space in the IBM Cloud, to run an isolated environment within the public cloud. VPC gives you the security of a private cloud, with the agility and ease of a public cloud. IBM Cloud Foundry Enterprise Environment fully exploits this capability, and allows you to host your applications with the highest level of network security and isolation possible. Full information about VPC, how this technology works, and how it is enabled, can be found in the [VPC documentation](https://cloud.ibm.com/docs/vpc-on-classic?topic=vpc-on-classic-about)

Follow the instructions [here to create your VPC](https://cloud.ibm.com/docs/vpc-on-classic?topic=vpc-on-classic-getting-started).

## IAM Permission Prerequisites
{: #iam-prereq}
Before provisioning CFEE into your VPC, ensure that you have the following IBM Cloud IAM access policies:
1. You must have [Administrator platform role for VPC Infrastructure](https://cloud.ibm.com/docs/vpc-on-classic?topic=vpc-on-classic-managing-user-permissions-for-vpc-resource).
1. You must have the same permissions as for [provisioning on classic infrastructure](cloud-foundry-permissions).

## Creating a VPC CFEE
{: #creating-vpc-cfee}
1. Create your VPC as [detailed here](https://cloud.ibm.com/docs/vpc-on-classic?topic=vpc-on-classic-getting-started).
1. Go to the CFEE [creation page](https://dev.console.cloud.ibm.com/cfadmin/create).
1. Select VPC infrastructure you just created.
1. Choose your VPC.
1. Choose your Worker Zones and Subnets you want to use.
1. From there, you can follow the instructions for creating a regular CFEE [here](cloud-foundry-create-environment).

## Limitations
{: #limitations}
There are several limitations detailed in the [release notes for v5.0.0](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-what-s-new-in-ibm-cloud-foundry-enterprise-environment#v500)
