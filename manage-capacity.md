---

copyright:
  years: 2018
lastupdated: "2018-08-15"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Resource usage

Administrators and developers can see how the resource capacity (memory and CPU) of an ICFEE is used by applications and cells. To monitor resource usage in an ICFEE environment:

1. Go to the [{{site.data.keyword.Bluemix_notm}} Cloud Foundry Environments dashboard](https://console.bluemix.net/dashboard/cloudfoundry?filter=cf_environments) and open the {{site.data.keyword.cfee_full_notm}} where you want to manage resource usage.
2. In the {{site.data.keyword.cfee_full_notm}} user interface, go to the **Resource Usage** entry in the left navigation pane to open the _Resource Usage_ page. Under the the _Resource Usage_ page you can either go to the _Applications_ or the _Cells_ sub-entries to open the corresponding pages.  The information displayed in the _Applications_ and _Cells_ pages can be considered two ways of breaking down resource usage:
   * The **Applicatons** page analyzes resource usage by applications aggregated across instances.  
   * The **Cells** page shows resource usage of application instances running on specific cells. The pattern of resource usage across cells can provide insights into capacity and load distribution.  For example, it may help identify problems with the load balancing of applications (e.g., large differences in the resources used by an application across cells) or resource usage approaching overall capacity (i.e., large percentages of resource usage in all cells).

**Note:** Resource usage data represents the usage of resources during the latest 5 minute collection cycle. Resource usage data can be refreshed by clicking **Refresh data** at the top of the page. 

## Applications
{: #usage_apps}

The Applications page has two sections:
1. Horizontal bar charts for memory and CPU showing:
   * *Total available* memory and CPU available in the ICFEE instance.
   * Memory and CPU used by *all the apps* in the ICFEE instance.
   * Memory and CPU used by the *selected apps* in the table below.

   To show the percentage of memory and CPU used by all the apps or those selected in the table, hover over the corresponding portion of the chart.  Hovering over the *all apps* portion of the chart shows the percentage of memory and CPU relative to the total available. Hovering over the *selected apps* portion of the chart shows the percentage of memory and CPU relative to the total available memory or CPU.

2. A table listing all the applications.  Each row in the table displays resource information for that application.  Expanding a row shows resource usage information for the various instances of that application.

  The first column in the table is a checkbox that determines if the corresponding application is to be included in the set of *Selected Apps* to be included in the chart at the top of the page. To include (or exlude) an application in the selected set, click on the correspondng checkbox.  When an application is selected or unselected for inclusion in the set, the graph is refreshed.  The _Selected Apps_ legend to the right of the bar chart indicates (in parenthesis) the number of applications currently select for inclusion in the graph.
 
  The following information is displayed as columns in the applications table:
   * **Application Name**: the name of the application or application instance. If the user does not have permission to access the application, the application GUID is displayed instead.
   * **Instances**: For an application it represents the number of running instances.  For an application instance (shown below the application name when the application row is expanded) it represents the name of the cell where the application instance runs.
   * **Total Memory-Physical**: MBs of physical memory used by all the instances of an application.  The physical memory used by an application equals the sum of the physical memory used by all the application's instances.
   * **Total Memory-Reserved**: MBs of memory reserved by all the instances of an application.  The memory reserved by an application equals the sum of the memory reserved by all the application's instances.
   * **Average CPU (% of cell)**: For application instances, the metric represents the average CPU **within the cell in which it runs**.  For an application, it represents CPU usage averaged acrossed its instance averages.
   * **Max CPU (% of cell)**: For application instances, the metric represents the maximum CPU used by that instance **within the cell in which it runs**.  For an application, it represents the highest of its instances maximum CPU usage.
   * **CPU (% of system)**: The percentage of total CPU available in the ICFEE used by an application and its instances.  The CPU used by an application equals the sum of CPU percentages used by all the application's instances.
   * **Average Requests**: The average number of incoming requests to an application during the latest data collection cycle.
   * **Organization**: The organization where the application is deployed. If the user is not a member of the organization, the organization GUID is displayed instead.
   
Expand an application row in the table to see the list of application instances and their corresponding resource usage metrics. 
  
### Filtering applications
You can use the filter the contents of the table through the **Applications** and **Organizations** filter dropdowns located above the table. 

Additionally, you can use the filter entry field above the table to show only applications maching the string you enter in the filter field.  The filter is reflected in both, the table and the chart above it.  
  
**Note:** The filters work independently of the table rows selected (through the checkbox in the first column table) for inclusion in the set of _Selected Apps_ included in the chart above. For example,  if there is a total of ten applications in the CFEE environment, and five of them are selected for inclusion in the chart, when you apply a filter that matches only one application instance, only that application instance will appear in the table.  Furthermore, the set of _Selected Apps_ will now include only that matching application, and the chart will be refreshed accordingly.  When you remove the filter, all ten applications will be shown again in the table, and the set of _Selected Apps_ will be reset to include all the apps.
  
  
## Cells
{: #usage_cells}

The Cells page has two sections:
1. Vertical bar charts showing:
   * *Total available* memory and CPU available in the ICFEE instance.
   * Memory and CPU used by the *All app instances* in the ICFEE instance.
   * Memory and CPU used by the *Selected app instances* in the ICFEE instance.
   * memory and CPU used by the *System* in the table below.  The system usage represents the resource used by the ICFEE service componentry plus application cache.

   To show the percentage of memory or CPU used by all the app instances or by the app instances selected in the table, hover over the corresponding portion of the chart.  Hovering over the chart bar shows the absolute memory or CPU available, the memory or CPU used by all the apps, and the memory or CPU used by system+cache.  It also shows the percentage of memory or CPU used by all apps and by system+cache relative to the total available.

2. A table listing all the cells and applications instances running in them.  Each row in the table displays resource information for that cell and application instance.  

  The first column in the table is a checkbox that determines if the corresponding application instance is to be included in the set of *Selected App instances* to be included in the chart at the top of the page. To include (or exlude) an application instance in the selected set, click on the correspondng checkbox.  When an application instance is selected or unselected for inclusion in the set, the graph is refreshed.
  
  The following information is displayed as columns in the table:
   * **Cell name**: The name of the cell.
   * **Application name**: The name of the application running on the cell. If the user does not have permission to access the application, the application GUID is displayed instead.
   * **Instances**: The number of the application instances running on the cell.
   * **Memory-Physical**: MBs of physical memory used by the application instance running in the cell. 
   * **Memory-Reserved**: MBs of memory reserved by the application instance running in the cell.
   * **CPU (% )**: The pertentage of total CPU available in the ICFEE used by the application instance running on the  cell.
  
### Filtering cells and app instances
You can use the filter the contents of the table through the **Cells** filter dropdown located above the table and selecting the cells to be displayed in the table.

Additionally, you can use the filter entry field above the table to show only applications instances maching the string you enter in the filter field.  The filter is reflected in both, the table and the chart above it.  
  
**Note:** The filters work independently of the table rows selected (through the checkbox in the first column table) for inclusion in the set of _Selected App Instances_ included in the chart above. For example,  if there is a total of ten application instances in the CFEE environment, and five of them are selected for inclusion in the chart, when you apply a filter that matches only one application instance, only that application instance will appear in the table.  Furthermore, the set of _Selected App Instances_ will now include only that app instance, and the chart will be refreshed accordingly.  When you remove the filter, all ten application instances will be shown again in the table, and the set of _Selected App Instances_  will be reset to include all app instances.
