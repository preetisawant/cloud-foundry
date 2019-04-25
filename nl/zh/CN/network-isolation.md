---

copyright:
  years: 2017, 2018
lastupdated: "2019-04-02"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 在隔离网络中运行
{: #isolated-network}


从 V2.2.0 开始，{{site.data.keyword.cfee_full}} (CFEE) 实例可以在保护环境免受外部威胁的隔离网络中运行。您可以通过专用 VLAN 和一组控制机制来创建隔离网络，以路由、过滤和保护流入和流出网络周界内资源的流量。隔离网络使用虚拟路由器设备 ([VRA](https://cloud.ibm.com/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started-with-ibm-virtual-router-appliance#vlans-and-the-gateway-appliance-s-role)) 等技术进行设置。 

**注：**在隔离网络中运行的 CFEE 实例需要将 CFEE kubernetes 集群更新为 V1.13。更新 Kubernetes 集群 V1.13 独立于 CFEE 更新。

CFEE 实例是从 IBM Kubernetes 服务供应到集群中的。CFEE 的 Cloud Foundry 单元（托管应用程序的位置）供应到集群的工作程序节点中。这意味着，访问 CFEE 单元和应用程序需要访问集群工作程序节点。 

工作程序节点包含用于在工作程序节点之间分配应用程序工作负载的应用程序负载均衡器 (ALB)。CFEE V2.2.0 支持在专用和公用网络中使用 Kubernetes ALB。这意味着 CFEE V2.2.0 可以从公用或专用网络进行访问。

## 隔离网络中的 CFEE 管理
{: #control-plan-access}

在 V2.2.0 中，CFEE 管理平面（用于供应、更新和其他生命周期活动的子系统）不直接依赖于 ALB 或工作程序节点来管理 CFEE 实例。相反，CFEE 管理平面使用 _Kubernetes 主节点和工作程序节点之间的 VPN 连接_来访问 CFEE 实例及其资源。这使管理平面能够控制 CFEE 实例。

创建 CFEE 实例后，管理平面会在您的帐户中创建提供给 IKS 主节点的 [IAM 服务标识](https://cloud.ibm.com/docs/overview/whats-new?topic=overview-whatsnew#identity-and-access-management-application-authentication-feature)。CFEE 管理平面使用此服务标识通过主节点及其 VPN 访问来访问 CFEE 主机工作程序，以进行后续供应和管理操作，包括部署 CFEE 的主 Cloud Foundry 组件。

下图描述了 VRA 网络周界后面安装的 CFEE。   
![网络隔离](img/CFEE_IsolatedNetwork.png "此图描述了 CFEE 在隔离网络中的工作方式。")

## 控制对隔离网络中 CFEE 实例的访问
{: #oppening-access-points}

由于各种原因，CFEE 实例中运行的 CF 应用程序经常需要访问隔离网络外部的内容。例如，应用程序可能需要访问公共 RESTful 服务或从公共注册表下载包，如 Docker 映像、NPM 包、Python 模块等。因此，您需要配置防火墙规则以启用特定网络访问需求。

您可以通过配置特定协议、源或目标端点的规则来控制与隔离网络的入站/出站连接。您可以使用用于设置网络周界（例如 VRA）的特定技术中的控制机制来创建和配置这些规则。但是，控制此情况的最简单方法是创建 [Calico 网络策略](https://docs.projectcalico.org/v3.4/reference/calicoctl/resources/globalnetworkpolicy)，以专门为主机 Kubernetes 集群定义网络规则。请参阅[创建和应用 Calico 网络策略](https://cloud.ibm.com/docs/containers?topic=containers-network_policies#adding_network_policies)以获取逐步指导信息。

与网络隔离的 CFEE 相关的网络访问规则可以是以下类型：

* **入站流量访问权：**安装了 Kubernetes 集群时，它会自动设置和配置[缺省 Calico 策略](https://cloud.ibm.com/docs/containers/cs_network_policy.html#default_policy)，以允许对工作程序节点（在此情况下托管 CFEE 实例）的管理访问。

<br>
用于访问 **Kubernetes 集群**工作程序节点的**缺省** Calico 规则：

```
allow-node-port-dnat            1500    ibm.role == 'worker_public'                        
allow-vrrp                      1600    ibm.role == 'worker_public'                        
allow-icmp                      1700    ibm.role in { 'worker_public', 'master_public' }
allow-bigfix-port               1900    ibm.role in { 'worker_public', 'master_public' }
allow-sys-mgmt                  1950    ibm.role in { 'worker_public', 'master_public' }
```
{: codeblock}
<br />
如果要使用备用网络周界实现，那么需要使用相应的控制机制来设置相同的策略。
  
* **出站流量访问权：**CFEE 依赖于 IBM Cloud 中具有公共端点的多个服务。您的隔离网络需要允许 CFEE 实例访问这些端点。下面列出了这些端点及其相应的 Calico 策略。

| 规则   | 描述 | 端点  |
|-----------|---------------|---------------|
| cfee-egress-allow-adminserver | 允许对 CFEE 管理平面进行出站访问 | 169.46.2.150/32, 169.47.104.126/32,     161.156.68.46/32, 130.198.90.238/32, 169.46.66.254/32, 169.46.186.113/32, 161.156.66.118/32, 130.198.90.238/32|
| cfee-egress-allow-docker | 允许对 Docker 注册表进行出站访问 | `registry-1.docker.io`, `docker.io`, `production.cloudflare.docker.com`|
| cfee-egress-allow-iks | 允许对 CFEE Kubernetes 集群管理平面进行出站访问 | [了解更多](https://cloud.ibm.com/docs/containers?topic=containers-firewall#firewall)|
| cfee-egress-allow-internal  | 允许出站访问和路由到 CFEE 的 Kubernetes 集群可移植 IP 地址 | 您可以使用 `kubectl get cm -n kube-system ibm-cloud-provider-vlan-ip-config -o json` \`jq .data 来查找集群可移植地址。"reserved_public_ip"`, `kubectl get cm -n kube-system ibm-network-interfaces -o yaml`, `kubectl get svc --all-namespaces`|
| cfee-egress-allow-postgres | 允许对 CFEE 的 Compose for PostgreSQL 数据库进行出站访问 | 您可以在 Compose 实例 `<cfee-name>-postgress` 的仪表板页面和 CFEE 的_专用访问权_页面中中找到该端点。|
| cfee-egress-allow-rc | 允许对 IBM Cloud 平台进行出站访问以启用服务联合 | `resource-controller.cloud.ibm.com` |
| cfee-egress-allow-registry | 允许对 IBM Cloud Container 注册表进行出站访问 | [了解更多](https://cloud.ibm.com/docs/containers?topic=containers-firewall#firewall) |
| cfee-egress-allow-logging | （可选）允许从 CFEE 工作程序节点到 IBM Cloud Monitoring 和 IBM Cloud Log Analysis 服务的出站网络流量 | [了解更多](https://cloud.ibm.com/docs/containers?topic=containers-firewall#firewall_outbound) |
| cfee-egress-allow-helm-tiller | 允许从 CFEE 工作程序节点到 helm 映像注册表的出站网络流量| 此 calico 规则适用于 Helm tiller 的 IP，tiller 需要访问 `mage:gcr.io` 和 `storage.googleapis.com` 域以拉取 Helm tiller 映像。|

<br>  
最终网络安全规则（最**重要**的规则）是针对与先前策略不匹配的所有网络流量拒绝所有访问权的规则。
<br>
**拒绝所有出站访问** 的 Calico 规则 (`cfee-egress-deny-all`)：

```
apiVersion: projectcalico.org/v3
kind: GlobalNetworkPolicy
metadata:
  name: cfee-egress-deny-all
spec:
  applyOnForward: true
  egress:
  - action: Deny
    destination: {}
    source: {}
  order: 3000
  selector: ibm.role in { 'worker_public' }
  types:
- Egress
```
{: codeblock}

<br>
**拒绝所有入站访问**的 Calico 规则 (`cfee-ingress-deny-all')`):

```
apiVersion: projectcalico.org/v3
kind: GlobalNetworkPolicy
metadata:
  name: cfee-ingress-deny-all
spec:
  applyOnForward: true
  ingress:
  - action: Deny
    destination: {}
    source: {}
  order: 4000
  selector: ibm.role=='worker_public'
  types:
- Ingress
```
{: codeblock}
<br>  
来自隔离网络的出站访问有一个复杂因素是，某些目标端点位于_公用边缘_网络（如 Cloudflare 或 Akamai）后面。在这种情况下，您可能需要允许访问经常更改的数百个 IP 地址。使用以下 Calico 规则 (`cfee-egress-allow-all`)，可以选择通过**允许所有出站访问**来避免此情况：

```
apiVersion: projectcalico.org/v3
kind: GlobalNetworkPolicy
metadata:
   name: cfee-egress-allow-http
    spec:
   egress:
   - action: Allow
     destination:
       ports:
       - 443
       - 80
     protocol: TCP
     source: {}
   order: 1611
   selector: ibm.role in { 'worker_public' }
   applyOnForward: true
   types:
   - Egress
```
{: codeblock}
  
在以上示例中，来自 CFEE 集群工作程序节点（“worker_public”）的所有 HTTP 和 HTTPS 调用（端口 443 和 80 上的所有 TCP 流量）都被允许出站（“egress”）访问公用网络。

## 管理控制平面中的专用访问权
{: #private-access}

在隔离网络中管理 CFEE 实例需要由 CFEE 管理控制平面对 CFEE 实例进行专用访问。缺省情况下，已启用 CFEE 管理控制平面对 CFEE 实例的专用访问。 

具有_管理_角色的用户可以禁用 CFEE 管理控制平面的专用访问。请注意，禁用专用访问将禁止 CFEE 控制平面检索数据和管理 CFEE 实例（无论是通过用户界面、CLI 还是 API）。CFEE 管理员可以在 CFEE 用户界面中的**专用访问权**页面（仅对管理员可见）中禁用专用访问权。进入该页面后，按**禁用**。  

对隔离网络的访问是通过 API 密钥进行的。缺省情况下，提供了 API 密钥。CFEE 管理员可以将缺省 API 密钥替换为定制密钥。要在禁用专用访问权之后将其启用，必须获取需要在 *_IBM Cloud API 密钥_*中生成的 API 密钥（在 IBM Cloud 用户界面标题中，转至_管理 > 访问 (IAM) > IBM Cloud API 密钥_）。

