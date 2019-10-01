---

copyright:
  years: 2019
lastupdated: "2019-09-01"
---

# Cloud Foundry Enterprise Environment on Virtual Private Cloud
{: #cfee-on-vpc}

You can provision an IBM Cloud Foundry Enterprise environment into your IBM Virtual Private Cloud (VPC).

## VPC Prerequisites
{: #vpc-prereq}
Before creating or configuring your VPC, ensure that your VPC meets the following criteria:
1. VPCs with access to classic resources are currently not supported.
1. For each subnet that is provided for the CFEE, you must enable the public gateway.
1. You must have at least one subnet in your VPC.

Follow the instructions [here to create your VPC](https://cloud.ibm.com/docs/vpc-on-classic?topic=vpc-on-classic-getting-started).

## IAM Permission Prerequisites
{: #iam-prereq}
Before provisioning CFEE into your VPC, ensure that you have the following IBM Cloud IAM access policies:
1. You must have [https://cloud.ibm.com/docs/vpc-on-classic?topic=vpc-on-classic-managing-user-permissions-for-vpc-resources](Administrator platform role for VPC Infrastructure).
1. You must have the same permissions as for [provisioning on classic infrastructure](cloud-foundry-permissions), excluding the Softlayer permissions.

## Creating a VPC CFEE
{: #creating-vpc-cfee}
1. Go to the CFEE creation page
1. Select VPC infrastructure.
1. Choose your VPC.
1. Choose your Worker Zones and Subnets you want to use.
1. From there, you can follow the instructions for creating a regular CFEE [here](cloud-foundry-create-environment).

## Limitations
{: #limitations}
1. VPC CFEEs currently do not support update.
1. VPC CFEEs currently do not support scaling.
1. VPC CFEEs currently do not support monitoring.
