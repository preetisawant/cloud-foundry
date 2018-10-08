---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-04-18"

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

* Acessos de _Visualização_ (ou superior) ao **grupo de recursos** **_Padrão_** na conta do {{site.data.keyword.Bluemix}}. Os grupos de recursos permitem organizar recursos em agrupamentos customizados para facilitar o controle de acesso a esses recursos. Você será solicitado a fornecer um grupo de recursos ao criar uma nova instância de ambiente. O acesso ao grupo de recursos _Padrão_ é necessário porque esse sempre é o grupo de recursos no qual o cluster do Kubernetes é necessário. Os usuários podem provisionar a instância do CFEE em um grupo de recursos diferente, mas o cluster do Kubernetes ainda será provisionado para o grupo de recursos _Padrão_. Se um usuário provisionar o CFEE em um grupo de usuários diferente, esses usuários necessitarão de acesso de visualizador nesse grupo de recursos.

* Função de administrador ou de editor para recursos do **serviço {{site.data.keyword.cfee_full_notm}}** no grupo de recursos ao qual o ambiente é designado. Os usuários com funções de administrador ou de editor no serviço {{site.data.keyword.cfee_full_notm}} podem criar e excluir ambientes. Mas somente os usuários com uma função de administração podem designar usuários a uma instância do {{site.data.keyword.cfee_full_notm}} ou mudar as funções que são designadas a usuários nessa instância.
   
* Função de administrador para os recursos do **Serviço do Kubernetes**. As instâncias do {{site.data.keyword.cfee_full_notm}} são implementadas na infraestrutura de cluster de contêiner, que é fornecida pelo serviço do Kubernetes. Quando você cria uma instância de serviço do {{site.data.keyword.cfee_full_notm}}, o serviço automaticamente cria um cluster do Kubernetes. O acesso ao Serviço do Kubernetes é necessário para criar essa infraestrutura de cluster. É possível definir o escopo do acesso à política do Serviço do Kubernetes para a região específica em que pretende provisionar a instância do CFEE ou definir o escopo do acesso a todas as regiões.

* Função de administrador ou de editor para o **serviço IBM Cloud Object Storage**, que é uma dependência obrigatória do serviço CFEE. Uma instância do serviço IBM Cloud Object Storage é usada para armazenar dados gerados durante a criação de seus contêineres de aplicativos ICFEE (por exemplo, pacotes de aplicativos transferidos por upload, buildpacks e executáveis compilados).

* Uma instância do serviço Compose for PostgreSQL é uma dependência necessária do serviço CFEE.  O Compose for PostgreSQL é usado para armazenar dados do Cloud Foundry em sua instância do CFEE (por exemplo, implementação do aplicativo de auditoria, eventos de início e parada; manter registros de participação do usuário do CFEE, organizações, espaços, aplicativos e conexões de serviço).  Essa instância do **serviço Compose for PostgreSQL** é implementada em um espaço dentro de uma organização pública do Cloud Foundry (não relacionada a organizações do CFEE) que você seleciona ao criar uma instância do {{site.data.keyword.cfee_full_notm}}. Isso significa que, quando você cria uma instância do {{site.data.keyword.cfee_full_notm}}, é necessário ter acesso de gerenciador a pelo menos uma organização no local em que pretende provisionar a instância do CFEE. Também é necessário acesso de desenvolvedor a pelo menos um espaço nessa organização. 

  Se você não for membro de pelo menos uma organização pública no local em que pretende criar uma instância do CFEE, peça a um administrador do IBM Cloud que o convide para uma. Se você tiver a função de administrador na conta, será possível incluir usuários em organizações públicas e espaços na conta executando o seguinte:

     * Acesse [**Gerenciar > Conta > Organizações Cloud Foundry**](https://console.bluemix.net/account/organizations) e clique em **Incluir uma organização** ou selecione uma organização existente.
     * Acesse a guia **Usuários** na parte superior da página da organização.
     * Localize o usuário que precisa criar instâncias do CFEE. Se o usuário para o qual você deseja poder criar instâncias CFEE não estiver na lista, clique em **Incluir ou convidar usuário** acima da tabela para incluir ou convidar usuários para a organização.
     * Acesse a guia **Espaços** na parte superior da página da organização.
     * Localize o espaço no qual a instância do serviço Compose for PostgreSQL seria provisionada e verifique a caixa de seleção da função de **Desenvolvedor**.

A tela a seguir ilustra as políticas de acesso como elas apareceriam na página Identidade e acesso do {{site.data.keyword.Bluemix_notm}} que permitem que um usuário crie uma instância do {{site.data.keyword.cfee_full_notm}}.

![Access policies](img/AccessPolicies_Creator.png)

Para confirmar que você tem as políticas de acesso necessárias para criar uma instância do {{site.data.keyword.cfee_full_notm}}:
1. Acesse o menu [**Gerenciar > Conta > Usuários**](https://console.bluemix.net/iam/#/users) no cabeçalho do {{site.data.keyword.Bluemix_notm}} para abrir a página **Identidade e acesso**.
2. Na guia Políticas de acesso, clique no usuário que está criando o ambiente para designar e visualizar as políticas de acesso para esse usuário.

## Permissões necessárias para trabalhar com um ambiente
{: #perm-working}

Para trabalhar com uma instância do {{site.data.keyword.cfee_full_notm}}, os usuários devem:
1. Ser membros da conta do {{site.data.keyword.Bluemix_notm}} em que a instância do {{site.data.keyword.cfee_full_notm}} foi criada.
2. ter recebido a concessão das _Políticas de acesso_ do IAM a seguir do administrador de conta (veja a página _Identidade e acesso_ no menu [**Gerenciar > Conta > Usuários**](https://console.bluemix.net/iam/#/users) no cabeçalho do {{site.data.keyword.Bluemix_notm}} para verificar suas atuais políticas de acesso da conta):

  - Acesso ao serviço do {{site.data.keyword.cfee_full_notm}} no grupo de recursos no qual a instância do ambiente foi criada. O nível de acesso e controle que os usuários têm em uma instância do {{site.data.keyword.cfee_full_notm}} depende da função que é concedida na política de acesso:
     - Os usuários designados às funções de administrador ou editor podem criar organizações, designar gerenciadores para organizações e espaços, ter permissões completas para todas as organizações e os espaços dentro do ambiente e executar ações operacionais usando a API do Cloud Controller. A esses usuários é concedido automaticamente o _escopo cloud_controller.admin_ no _escopo User Account and Authentication_ do Cloud Foundry.
     - Os usuários designados a uma função de visualizador podem ver esse ambiente no painel principal do {{site.data.keyword.Bluemix_notm}} e podem abrir sua interface com o usuário. O acesso de usuários a organizações e espaços específicos no ambiente é controlado pelas funções específicas de organização e espaços que são designadas pelos gerenciadores dessas organizações e espaços. Para obter mais informações, consulte [Incluindo usuários em organizações](add-users.html).

A imagem ilustra as políticas de acesso mínimo (como elas apareceriam na página _Identidade e acesso_ do {{site.data.keyword.Bluemix_notm}}) necessárias para acessar um {{site.data.keyword.cfee_full_notm}}.

![Access policies](img/AccessPolicies_User.png)

