---

copyright:
  years: 2018
lastupdated: "2018-04-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Adding users to organizations and spaces
{: #adding_users}

Members of an organization with a manager role can add members to that organization. Before users can be added to an organization, they must have at least viewer role to both the {{site.data.keyword.cfee_full}} service and the resource group to which the {{site.data.keyword.cfee_full_notm}} instance belongs. These permissions are set in the _Identity & Access_ page under the **Manage > Users** in the {{site.data.keyword.Bluemix}} header.

To add users as members of an organization in an {{site.data.keyword.cfee_full_notm}} instance:

1. Go to the **Organizations** entry in the navigation pane. Locate the organization where you want to add a member. Go to the _Actions_ menu in the table row, and select **Add member**. Alternatively, you can click the organization to open the organization's page, go to the **Members** tab, and click **Add member**.
2. In the _Add member_ window, find the user, select an **Organization role**, and click **Add**.

**Note:** If you intend to add a user who was recently invited to your {{site.data.keyword.Bluemix_notm}} account, it can take several minutes for that user to be recognized in the window where you add users to an organization or space. If the user is not recognized when you enter the user name, enter the user's email address and press the plus (+) icon to add the user.

Only space managers (or managers of the parent organization) can add members to a space. To add users as members of a space in an organization in an {{site.data.keyword.cfee_full_notm}} instance:

1. Go to the **Organizations** entry in the navigation pane, locate the organization where the target space is located, and click it to open the organization's page.
2. In the organization's page, go to the **Spaces** tab.
3. Locate the target space in the spaces table, go the _Actions_ menu in the table row, and select **Add member**. Alternatively, you can click the target space in the table to open the space's page, and click **Add member**.
4. In the _Add member_ window, find the user, select a **Space role**, and click **Add**.

**Note**: Organization managers can add members directly to a space without adding them first to the parent organization. When an organization manager adds members to a space, those members also become members of the parent organization.