---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-11-16"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Permissões
{: #permissions}

Antes de os usuários começarem a criar e trabalhar com instâncias do serviço do {{site.data.keyword.cfee_full}}, suas permissões devem ser configuradas corretamente por um administrador da conta na qual a instância deve ser criada. 

## Permissões necessárias para criar um novo ambiente
{: #perm-creating}

Para criar novas instâncias do serviço do CFEE, os usuários devem ter políticas de acesso concedidas por um administrador de conta, não somente para o próprio serviço CFEE, mas também para os serviços de apoio que também são criados automaticamente quando o CFEE é criado.

As políticas de acesso do Identity & Access Management (IAM) a seguir são necessárias para que os usuários possam criar uma instância do {{site.data.keyword.cfee_full_notm}}:

* Acessos de _Visualização_ (ou superior) ao **grupo de recursos** **_Padrão_** na conta do {{site.data.keyword.Bluemix}}. Os grupos de recursos permitem organizar recursos em agrupamentos customizados para facilitar o controle de acesso a esses recursos. Você será solicitado a fornecer um grupo de recursos ao criar uma nova instância de ambiente. O acesso ao grupo de recursos _Padrão_ é necessário porque esse sempre é o grupo de recursos no qual o cluster do Kubernetes é necessário.  Os usuários podem provisionar a instância do CFEE em um grupo de recursos diferente, mas o cluster do Kubernetes ainda será provisionado para o grupo de recursos _Padrão_.  Se um usuário provisionar o CFEE em um grupo de usuários diferente, esses usuários necessitarão de acesso de visualizador nesse grupo de recursos.

* Função de _administrador_ ou de _editor_ para os recursos do **serviço {{site.data.keyword.cfee_full_notm}}**. 
No grupo de recursos ao qual o ambiente está designado. Os usuários com funções de administrador ou de editor no serviço {{site.data.keyword.cfee_full_notm}} podem criar e excluir ambientes. Mas somente os usuários com uma função de administração podem designar usuários a uma instância do {{site.data.keyword.cfee_full_notm}} ou mudar as funções que são designadas a usuários nessa instância.
   
* Função de _administrador_ para os recursos do **serviço do Kubernetes**. As instâncias do {{site.data.keyword.cfee_full_notm}} são implementadas na infraestrutura de cluster de contêiner, que é fornecida pelo serviço do Kubernetes. Quando você cria uma instância de serviço do {{site.data.keyword.cfee_full_notm}}, o serviço automaticamente cria um cluster do Kubernetes. O acesso ao Serviço do Kubernetes é necessário para criar essa infraestrutura de cluster. É possível definir o escopo do acesso à política do Serviço do Kubernetes para a região específica em que pretende provisionar a instância do CFEE ou definir o escopo do acesso a todas as regiões.

* A função de plataforma de _administrador_ ou do _editor_ e a função de acesso de
serviço do gerenciador para o **serviço IBM Cloud Object Storage**, que é uma dependência
necessária do serviço do CFEE. Uma instância do serviço IBM Cloud Object Storage é usada para armazenar dados gerados durante a criação de seus contêineres de aplicativos ICFEE (por exemplo, pacotes de aplicativos transferidos por upload, buildpacks e executáveis compilados).

* Uma instância do serviço Compose for PostgreSQL é uma dependência necessária do serviço CFEE.  O Compose for PostgreSQL é usado para armazenar dados do Cloud Foundry em sua instância do CFEE (por exemplo, implementação do aplicativo de auditoria, eventos de início e parada; manter registros de participação do usuário do CFEE, organizações, espaços, aplicativos e conexões de serviço).  Essa instância do **serviço Compose for PostgreSQL** é implementada em um espaço dentro de uma organização pública do Cloud Foundry (não relacionada a organizações do CFEE) que você seleciona ao criar uma instância do {{site.data.keyword.cfee_full_notm}}.  Isso
significa que, ao criar uma instância do {{site.data.keyword.cfee_full_notm}}, é necessário ter acesso de
_gerenciador_ para pelo menos uma organização na localização em que pretende fornecer a instância do CFEE. Também
é necessário o acesso de _desenvolvedor_ para pelo menos um espaço nessa organização. 

  Se você não for membro de pelo menos uma organização pública no local em que pretende criar uma instância do CFEE, peça a um administrador do IBM Cloud que o convide para uma. Se você tiver a função de administrador na conta, será possível incluir usuários em organizações públicas e espaços na conta executando o seguinte:

     * Acesse [**Gerenciar > Conta > Organizações Cloud Foundry**](https://console.bluemix.net/account/organizations) e clique em **Incluir uma organização** ou selecione uma organização existente.
     * Acesse a guia **Usuários** na parte superior da página da organização.
     * Localize o usuário que precisa criar instâncias do CFEE. Se o usuário para o qual você deseja poder criar instâncias CFEE não estiver na lista, clique em **Incluir ou convidar usuário** acima da tabela para incluir ou convidar usuários para a organização.
     * Acesse a guia **Espaços** na parte superior da página da organização.
     * Localize o espaço no qual a instância do serviço Compose for PostgreSQL seria provisionada e verifique a caixa de seleção da função de **Desenvolvedor**.

A tela a seguir ilustra as políticas de acesso como elas apareceriam na página Identidade e acesso do {{site.data.keyword.Bluemix_notm}} que permitem que um usuário crie uma instância do {{site.data.keyword.cfee_full_notm}}.

![Access policies](img/AccessPolicies_Creator.png)

É possível conceder permissões de usuário usando a linha de comandos do {{site.data.keyword.Bluemix}}.
Também é possível definir uma política de acesso para um usuário especificando os parâmetros da política (isto é,
serviços, funções, regiões, etc.) em um arquivo formatado JSON que é chamado pelo comando que cria a política. Consulte
[Designando
uma política do IAM usando a linha de comandos](https://console.bluemix.net/docs/services/cloud-monitoring/security/assign_policy.html#assign_policy_commandline) para obter mais informações ou emita ibmcloud iam -help na linha de comandos. Observe
que isso requer a instalação da
[CLI do IBM Cloud](https://console.bluemix.net/docs/cli/reference/ibmcloud/download_cli.html#install_use).
{:tip}

Para confirmar que você tem as políticas de acesso necessárias para criar uma instância do {{site.data.keyword.cfee_full_notm}}:
1. Acesse o menu [**Gerenciar > Conta > Usuários**](https://console.bluemix.net/iam/#/users) no cabeçalho do {{site.data.keyword.Bluemix_notm}} para abrir a página **Identidade e acesso**.
2. Na guia Políticas de acesso, clique no usuário que está criando o ambiente para designar e visualizar as políticas de acesso para esse usuário.

Para obter mais informações sobre o gerenciamento de usuários e o acesso no {{site.data.keyword.Bluemix}},
incluindo como organizar um conjunto de usuários e IDs de serviço para facilitar a designação de acesso a múltiplos
usuários por vez, consulte
[Gerenciando os usuários e o acesso](https://console.bluemix.net/docs/iam/iamusermanage.html#iamusermanage).

### Expedindo a configuração de permissões para criar um ambiente usando a CLI
{: #permcli-creating}

É possível expedir a configuração de permissões para criar as instâncias do CFEE por meio de `ibmcloud
cfee create-permission-set`. O comando permite que um administrador do CFEE configure em um comando único as
políticas de acesso necessárias para criar uma instância do CFEE e todos os seus serviços auxiliares. 

O comando configura as permissões para um _Grupo de acesso_ do IAM e inclui um usuário neste
_Grupo de acesso_. O administrador que está emitindo o comando pode incluir nele um _Grupo de
acesso_ existente. Se nenhum _Grupo de acesso_ for fornecido, um
_cfee-provision-access-group_ padrão será criado automaticamente.

```
ibmcloud cfee create-permission-set USER_NAME [-ag, --access-group GROUP_NAME] [--output TYPE]
```
{: pre}

O comando configura as políticas de acesso a seguir para o usuário de destino:

*  Funções de editor para os serviços Cloud Object Storage e CFEE na conta do IBM Cloud atual.
*  Função de administrador para o serviço do Kubernetes na conta do IBM Cloud atual.
*  Função de desenvolvedor para o espaço atual na organização atual para fornecimento do Compose for
PostgreSQL.

Para obter mais detalhes sobre o comando, emita o seguinte:

```
cfee create-permission-set -help
```
{: pre}

É possível usar o `ibmcloud cfee create-permission-get` para localizar ou validar as
políticas de acesso estabelecidas para um usuário:

```
ibmcloud cfee provision-permission-get USER_NAME [-ag, --access-group GROUP_NAME] [--output TYPE]
```
{: pre}

## Permissões necessárias para trabalhar com um ambiente
{: #perm-working}

Para trabalhar com uma instância do {{site.data.keyword.cfee_full_notm}}, os usuários devem:
1. Ser membros da conta do {{site.data.keyword.Bluemix_notm}} em que a instância do {{site.data.keyword.cfee_full_notm}} foi criada.
2. ter recebido a concessão das _Políticas de acesso_ do IAM a seguir do administrador de conta (veja a página _Identidade e acesso_ no menu [**Gerenciar > Conta > Usuários**](https://console.bluemix.net/iam/#/users) no cabeçalho do {{site.data.keyword.Bluemix_notm}} para verificar suas atuais políticas de acesso da conta):

    Todos os usuários precisam de acesso de _visualizador_ ou superior para a instância do
{{site.data.keyword.cfee_full_notm}} no grupo de recursos sob o qual a instância do ambiente foi criada. O nível de acesso e controle que os usuários têm em uma instância do {{site.data.keyword.cfee_full_notm}} depende da função que é concedida na política de acesso:
  - Os usuários com as funções de _administrador_ ou do _editor_ designadas podem
criar organizações, designar gerenciadores para organizações e espaços, ter permissões integrais para todas as
organizações e espaços no ambiente e executar as ações operacionais por meio da API do Cloud Controller. A esses usuários é concedido automaticamente o _escopo cloud_controller.admin_ no _escopo User Account and Authentication_ do Cloud Foundry.
  - Os usuários com a função de _visualizador_ para um CFEE podem vê-lo listado no painel
principal do {{site.data.keyword.Bluemix_notm}} e abrir a sua interface com o usuário. O acesso de usuários a organizações e espaços específicos no ambiente é controlado pelas funções específicas de organização e espaços que são designadas pelos gerenciadores dessas organizações e espaços. Para obter mais informações, consulte [Incluindo usuários em organizações](add-users.html).

     **Nota:** o acesso de _visualizador_ ao grupo de recursos sob o qual
uma instância do CFEE está agrupada não é, por si só, suficiente para tornar o CFEE visível a um usuário. Os usuários
precisam de acesso explícito à instância do CFEE (com a função de visualizador ou superior) para ter visibilidade
nessa instância.

  - Os usuários precisam da função de _editor_ ou superior para que um serviço do
{{site.data.keyword.Bluemix_notm}} possa **ligar** uma instância desse serviço
a um aplicativo implementado em um espaço do CFEE.

  - Os usuários precisam da função de _editor_ ou superior para uma instância do CFEE e a função de
_operador_ ou superior para o cluster do Kubernetes no qual o CFEE é fornecido para poderem **atualizar o CFEE para uma nova versão**.

  - Os usuários precisam da função de _administrador_ para uma instância do CFEE e a função de
_operador_ ou superior para o cluster do Kubernetes no qual o CFEE é fornecido para poderem
**mudar a capacidade** de um CFEE (incluindo ou removendo células).

