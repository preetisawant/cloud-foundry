---

copyright:

  years: 2018
lastupdated: "2018-04-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Assign roles
{: #roles}

You can grant multiple roles to team members in an {{site.data.keyword.Bluemix_notm}} account. These roles define the permissions of the user to manage account and organization resources:
You can grant [user roles](/docs/iam/users_roles.html#userroles) to members of an organization. These roles define the level of access within the organization, and restrict who can access a space and its resources. For example, you can grant users different permissions to different spaces.

## Account owner
{: #accountowner}

Whether you design a multi-organization architecture or a single-organization architecture, the account owner is the super user of the cloud environment.

The account owner core tasks include:

* Managing the resources of the global account.
* Creating organizations.
* Adding team members to the account.

The account owner can also add one or more users as managers of an organization by assigning these users the **Manager** role. Consider adding two users as organization managers. The first user acts as the principal manager of the organization. The second user acts as the deputy manager, in case, the principal manager is unavailable.

## User roles
{: #userroles}

User roles define the permissions that you can assign to a team member in an organization and define the level of access that a team member has within the organization and each space.

In a multi-organization architecture or in a single-organization architecture, define the team members and the permissions that each user requires to complete their work:

1. Identify the set of users that requires access to an organization.
2. Define the permissions for each team member in the organization and in a space of the organization.
3. Select the role that grants a user the permissions they require.

   * Organization manager
   * Organization auditor
   * Organization billing manager
   * Space manager
   * Space developer
   * Space auditor

### Organization manager
{: #bporgmgr}

The tasks that an organization manager is responsible for includes creating spaces, distributing the quota between the spaces, inviting team members and optionally granting them specific roles, and defining custom domains.

### Organization auditor
{: #bporgauditor}

The team members with the organization **Auditor** role can monitor the quota, the resource usage, and the team members for all of the spaces in an organization.
The auditors can then report on the organization efficiency and highlight any potential problems.

* When you adopt a multi-organization architecture, you might want to grant the auditor role to the same team members for every organization that is part of the account.
Then, these team members can monitor the quota across all of the organizations in your cloud environment and obtain a global view of the account.
* When you adopt a single-organization architecture, grant the auditor role to the team members with the responsibility for monitoring the quota usage and overall efficiency
of the organization.

### Organization billing manager
{: #bporgbillingmgr}

The team members with the **Billing Manager** role can monitor the costs of an organization.

* When you adopt a multi-organization architecture, you might want to grant the billing role to the same set of team members for every organization that is part of the account. Then, these team members can then monitor the cost of each organization and obtain a global view of the account.
* In a single-organization architecture, identify the users that are responsible for monitoring the cost.

### Space manager
{: #bpspacemgr}

The space **Manager** is responsible for any work that is done within the space that they manage and control. The space manager can perform the following tasks:

* Monitoring the quota that is allocated to the space.
* Requesting more resources to the organization manager.
* Notifying the organization manager of resources that are not required.
* Adding team members to the space with the **Developer** role.
* Optionally, assigning the space **Manager** role to a team member to act as a deputy space manager in their absence.

### Space developer
{: #bpspacedev}

A space developer can do the following tasks:

* Manage Cloud Foundry apps.
* Provision and configure {{site.data.keyword.Bluemix_notm}} services.
* Associate domains to apps.

### Space auditor
{: #bpspaceauditor}

For every space, you might want to grant the space **Auditor** role to the same team members with the organization **Auditor** role. In your enterprise, this role might have to be granted to a specific set of users.

