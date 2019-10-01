---

copyright:
  years: 2019
lastupdated: "2019-09-01"
---

# Cloud Foundry Enterprise Environment on Virtual Private Cloud
{: #cfee-on-vpc}

You can provision a Cloud Foundry Enterprise environment into your Virtual Private Cloud (VPC).

Follow the instructions here to create your VPC. https://cloud.ibm.com/docs/vpc?topic=vpc-creating-a-vpc-using-the-ibm-cloud-console

## IAM Permission Prerequisites
{: #iam-prereq}
1. You must have Admin Platform permission on the VPC that you want to use.
1. You must have the same permissions as for provisioning on classic infrastructure. https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-permissions&locale=en-us

## VPC Prerequisites
{: #vpc-prereq}
To provision your CFEE in a VPC, you must have the following:
1. You must have Admin Platform permission on the VPC that you want to use.
1. VPCs with access to classic resources are currently not supported.
1. For each subnet that is provided for the CFEE, you must enable the public gateway.
1. You must have at least one subnet in your VPC.
1. You must have the same permissions as for provisioning on classic infrastructure. https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-permissions&locale=en-us

## Creating a VPC CFEE
{: #creating-vpc-cfee}
1. Go to the CFEE creation page
1. Select VPC infrastructure.
1. Choose your VPC.
1. Choose your Worker Zones and Subnets you want to use.
1. From there, you can follow the instructions for creating a regular CFEE here https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-create-environment&locale=en-us

## Limitations
{: #limitations}
1. VPC CFEEs currently do not support update.
1. VPC CFEEs currently do not support scaling.
1. VPC CFEEs currently do not support monitoring.
