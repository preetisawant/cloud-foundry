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

# Operando em uma rede isolada
{: #isolated-network}


Iniciando com a versão 2.2.0, as instâncias do {{site.data.keyword.cfee_full}} (CFEE) podem operar dentro de redes isoladas que protegem o ambiente de ameaças externas. Você cria uma rede isolada por meio de VLANs privadas e um conjunto de mecanismos de controle para rotear, filtrar e proteger o tráfego dentro e fora dos recursos dentro do perímetro de rede. Redes isoladas são configuradas usando tecnologias como Virtual Router Appliances ([VRAs](https://cloud.ibm.com/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started-with-ibm-virtual-router-appliance#vlans-and-the-gateway-appliance-s-role)). 

**Nota:**As instâncias CFEE que operam em uma rede isolada exigiam que o cluster do CFEE kubernetes fosse atualizado para v1.13. A atualização do cluster Kubernetes v1.13 é independente da atualização do CFEE.

Uma instância do CFEE é provisionada em um cluster por meio do IBM Kubernetes Service. As células do Cloud Foundry do CFEE (em que os aplicativos são hospedados) são provisionadas nos nós do trabalhador do Cluster. Isso significa que o acesso às células e aplicativos do CFEE implica no acesso aos nós do trabalhador do cluster. 

Os nós do trabalhador contêm Balanceadores de cargas de aplicativo (ALBs) que distribuem a carga de trabalho dos aplicativos entre os nós do trabalhador. O CFEE v2.2.0 ativa os ALBs do Kubernetes em redes privadas e públicas. Isso significa que o CFEE v2.2.0 pode ser acessado a partir de redes públicas ou privadas.

## Gerenciamento do CFEE em uma rede isolada
{: #control-plan-access}

Na v2.2.0, o plano de gerenciamento do CFEE (o subsistema usado para fornecimento, atualizações e outras atividades de ciclo de vida) não depende diretamente dos ALBs ou nós do trabalhador para gerenciar uma instância do CFEE. Em vez disso, o plano de gerenciamento do CFEE usa a _conexão de VPN entre o mestre do Kubernetes e os nós do trabalhador_ para acessar a instância do CFEE e os seus recursos. Isso permite que o plano de gerenciamento controle a instância do CFEE.

Após você criar a sua instância do CFEE, o plano de gerenciamento criará um [ID de serviço do IAM](https://cloud.ibm.com/docs/overview/whats-new?topic=overview-whatsnew#identity-and-access-management-application-authentication-feature) em sua conta que ele fornecerá para o nó principal do IKS. O plano de gerenciamento do CFEE usa esse ID de serviço para acessar os trabalhadores do host do CFEE por meio do nó principal e de seu acesso à VPN para operações de fornecimento e gerenciamento subsequentes, incluindo a implementação do componente principal do Cloud Foundry do CFEE.

O diagrama abaixo descreve um CFEE instalado atrás de um perímetro de rede do VRA.   
![Isolamento de rede](img/CFEE_IsolatedNetwork.png "Diagrama descrevendo como um CFEE funciona em uma rede isolada.")

## Controlando o acesso às instâncias do CFEE em uma rede isolada
{: #oppening-access-points}

Os apps do CF em execução em uma instância do CFEE frequentemente precisam atingir fora da rede isolada por vários motivos. Por exemplo, um aplicativo pode precisar acessar um serviço de RESTful público ou fazer download de pacotes de registros públicos, como uma imagem do Docker, pacotes do NPM, módulos do Python etc. Portanto, é necessário configurar as suas regras de firewall para ativar as suas necessidades de acesso de rede específicas.

É possível controlar a conectividade de entrada / saída para / a partir de uma rede isolada, configurando as regras para protocolos, origens ou terminais de destino específicos. É possível criar e configurar esses usando mecanismos de controle na tecnologia específica usada para configurar o perímetro de rede (por exemplo, VRA). No entanto, a maneira mais simples de controlar isso é criando [Políticas de rede do Calico](https://docs.projectcalico.org/v3.4/reference/calicoctl/resources/globalnetworkpolicy) que definem regras de rede especificamente para o cluster Kubernetes do host. Consulte [Criando e aplicando políticas de rede do Calico](https://cloud.ibm.com/docs/containers?topic=containers-network_policies#adding_network_policies) para obter orientação passo a passo.

As regras de acesso à rede relacionadas a um CFEE isolado de rede podem ser dos tipos a seguir:

* **Acesso ao tráfego de entrada:** quando um cluster Kubernetes for instalado, ele configurará automaticamente e configurará uma [política do Calico padrão](https://cloud.ibm.com/docs/containers/cs_network_policy.html#default_policy) que permitirá o acesso de gerenciamento aos nós do trabalhador (hospedando a sua instância do CFEE nesse caso).

<br>
Regras do Calico **Padrão** para acessar os nós do trabalhador do **cluster Kubernetes**:

```
allow-node-port-dnat            1500    ibm.role == 'worker_public'                        
allow-vrrp                      1600    ibm.role == 'worker_public'                        
allow-icmp                      1700    ibm.role in { 'worker_public', 'master_public' }
allow-bigfix-port               1900    ibm.role in { 'worker_public', 'master_public' }
allow-sys-mgmt                  1950    ibm.role in { 'worker_public', 'master_public' }
```
{: codeblock}
<br />
Se você estiver usando uma implementação de perímetro de rede alternativa, será necessário configurar as mesmas políticas usando os mecanismos de controle correspondentes.
  
* **Acesso ao tráfego de saída:** o CFEE conta com uma série de serviços no IBM Cloud com terminais públicos. A sua rede isolada precisa permitir que a sua instância do CFEE atinja esses terminais. Eles estão listados abaixo junto com suas respectivas políticas Calico.

| Regra   | Descrição | Terminal |
|-----------|---------------|---------------|
| cfee-egress-allow-adminserver | Permite o acesso de saída para o plano de gerenciamento do CFEE | 169.46.2.150/32, 169.47.104.126/32, 161.156.68.46/32, 130.198.90.238/32, 169.46.66.254/32, 169.46.186.113/32, 161.156.66.118/32, 130.198.90.238/32|
| cfee-egress-allow-docker | Permite o acesso de saída para os registros do Docker | `registry-1.docker.io`, `docker.io`, `production.cloudflare.docker.com`|
| cfee-egress-allow-iks | Permite o acesso de saída para o plano de gerenciamento de cluster Kubernetes do CFEE | [Saiba mais](https://cloud.ibm.com/docs/containers?topic=containers-firewall#firewall)|
| cfee-egress-allow-internal  | Permite o acesso e o roteamento de saída para os endereços IP móveis do cluster Kubernetes do CFEE | É possível localizar os seus endereços móveis do cluster usando: `kubectl get cm -n kube-system ibm-cloud-provider-vlan-ip-config -o json` \`jq .data."reserved_public_ip"`, `kubectl get cm -n kube-system ibm-network-interfaces -o yaml`, `kubectl get svc --all-namespaces`|
| cfee-egress-allow-postgres | Permite o acesso de saída ao banco de dados do Compose for PostgreSQL do CFEE | É possível localizar o terminal por meio da instância do Compose da página de painel do `<cfee-name>-postgress` e na página _Acesso privado_ do CFEE. |
| cfee-egress-allow-rc | Permite o acesso de saída à plataforma IBM Cloud para ativar a organização do serviço | `resource-controller.cloud.ibm.com` |
| cfee-egress-allow-registry | Permite o acesso de saída para o IBM Cloud Container Registry | [Saiba mais](https://cloud.ibm.com/docs/containers?topic=containers-firewall#firewall) |
| cfee-egress-allow-logging | (opcional) Permite o tráfego de rede de saída dos nós do trabalhador do CFEE para os serviços do IBM Cloud Monitoring e do IBM Cloud Log Analysis | [Saiba mais](https://cloud.ibm.com/docs/containers?topic=containers-firewall#firewall_outbound) |
| cfee-egress-allow-helm-tiller | Permite o tráfego de rede de saída dos nós do trabalhador do CFEE para o registro de imagem do helm| Essa regra calico é para IPs do tiller do Helm, que precisa de acesso aos domínios `mage:gcr.io` e `storage.googleapis.com` para puxar a imagem do tiller do helm. |

<br>  
A regra de segurança de rede final (a mais **importante**) é aquela que nega todo o acesso ao tráfego de rede que não corresponde às políticas prévias.
<br>
Regra do calico para **negar todo o acesso de saída** (`cfee-egress-deny-all`):

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
Regra do calico para **negar todo o acesso de entrada** (`cfee-ingress-deny-all')
`):

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
Uma complexidade com o acesso de saída de redes isoladas é que alguns dos terminais de destino estão atrás de uma rede de _borda pública_, como Cloudflare ou Akamai. Nesse caso, pode ser necessário permitir potencialmente o acesso a centenas de endereços IP que mudem com frequência. É possível, opcionalmente, evitar essa situação **permitindo todo o acesso de saída** usando a regra do Calico a seguir (`cfee-egress-allow-all`):

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
  
No exemplo acima, todas as chamadas de HTTP e de HTTPS (todo o tráfego do TCP nas portas 443 e 80) provenientes dos nós do trabalhador do cluster do CFEE (“worker_public”) têm permissão para acesso de saída (“egresso”) à rede pública.

## Acesso privado por meio do plano de controle de gerenciamento
{: #private-access}

O gerenciamento de uma instância do CFEE em uma rede isolada requer acesso privado para a instância do CFEE pelo plano de controle de gerenciamento do CFEE. O acesso privado para a instância do CFEE pelo plano de controle de gerenciamento do CFEE é ativado por padrão. 

Os usuários com uma função de _Administração_ podem desativar o acesso privado pelo plano de controle de gerenciamento do CFEE. Observe que a desativação do acesso privado desativará o plano de controle CFEE a partir da recuperação de dados e do gerenciamento da instância CFEE (nem por meio da interface com o usuário, da CLI nem da API). Os administradores do CFEE podem desativar o acesso privado na página **Acesso privado** (visível apenas para administradores), localizada na interface com o usuário do CFEE. Uma vez na página, pressione **Desativar**.  

O acesso à rede isolada ocorre por meio de uma chave de API. Uma chave de API é fornecida por padrão. Um administrador do CFEE pode substituir a chave de API padrão por uma chave customizada. A ativação do acesso privado após ele ter sido desativado requer uma chave de API que precisa ser gerada nas *_Chaves de API do IBM Cloud_* (No cabeçalho da interface com o usuário do IBM Cloud, acesse _Gerenciar > Acessar (IAM) > Chaves de API do IBM Cloud_).

