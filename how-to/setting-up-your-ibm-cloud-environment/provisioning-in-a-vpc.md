---



copyright:

  years: 2019

lastupdated: "2019-08-12"



---

You can provision a Cloud Foundry Enterprise environment into your Virtual Private Cloud (VPC).

Follow the instructions here to create your VPC. https://cloud.ibm.com/docs/vpc?topic=vpc-creating-a-vpc-using-the-ibm-cloud-console

# Permission Prerequisites
1. You must have Admin Platform permission on the VPC that you want to use. #TODO link to the iam docs on it
1. You must have the same permissions as for provisioning on classic infrastructure. https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-permissions&locale=en-us
# TODO screenshot of permissions example

# VPC Prerequisites
To provision your CFEE in a VPC, you must have the following:
1. You must have Admin Platform permission on the VPC that you want to use. #TODO link to the iam docs on it
1. VPCs with access to classic resources are currently not supported. #TODO remove this when we support it
1. For each subnet that is provided for the CFEE, you must enable the public gateway. #TODO Change to a warning that, if theres no public gateway, you need to be able to route to specific endpoints
1. You must have at least one subnet in your VPC.
1. You must have the same permissions as for provisioning on classic infrastructure. https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-permissions&locale=en-us

# Creating a VPC CFEE
1. Go to the CFEE creation page #TODO link
1. Select VPC infrastructure.
1. Choose your VPC.
1. Choose your Worker Zones and Subnets you want to use.
1. From there, you can follow the instructions for creating a regular CFEE here https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-create-environment&locale=en-us

# Limitations
1. VPC CFEEs currently do not support update.
1. VPC CFEEs currently do not support scaling.
1. VPC CFEEs currently do not support monitoring.

# TODO
Make the naming consistent with other services
Are these links setup properly?
Fix other TODOs
