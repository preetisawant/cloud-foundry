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

Antes de começar a criar e trabalhar com instâncias do serviço {{site.data.keyword.cfee_full}}, as permissões do administrador e do restante da equipe devem ser configuradas corretamente.

## Permissões necessárias para criar um novo ambiente
{: #perm-creating}

Para criar novas instâncias do serviço {{site.data.keyword.cfee_full_notm}}, os usuários deverão receber políticas de acesso pelo administrador da conta na qual a instância será criada:

* Acesso a pelo menos um grupo de recursos na conta do {{site.data.keyword.Bluemix}}. Os grupos de recursos permitem organizar recursos em agrupamentos customizados para facilitar o controle de acesso a esses recursos. Você será solicitado a fornecer um grupo de recursos ao criar uma nova instância de ambiente.

* Função de administrador ou de editor para o serviço {{site.data.keyword.cfee_full_notm}} no grupo de recursos ao qual o ambiente está designado. Os usuários com funções de administrador ou de editor no serviço {{site.data.keyword.cfee_full_notm}} podem criar e excluir ambientes. Mas somente os usuários com uma função de administração podem designar usuários a uma instância do {{site.data.keyword.cfee_full_notm}} ou mudar as funções que são designadas a usuários nessa instância.

* Função de administrador ou de editor para o serviço IBM Cloud Object Storage, que é uma dependência necessária do serviço CFEE. Uma instância do serviço IBM Cloud Object Storage é usada para armazenar dados gerados durante a criação de seus contêineres de aplicativos ICFEE (por exemplo, pacotes de aplicativos transferidos por upload, buildpacks e executáveis compilados).

* Uma instância do serviço Compose for PostgreSQL é uma dependência necessária do serviço CFEE. O Compose for PostgreSQL é usado para armazenar dados do Cloud Foundry em sua instância do CFEE (por exemplo, implementação do aplicativo de auditoria, eventos de início e parada; manter registros de participação do usuário do CFEE, organizações, espaços, aplicativos e conexões de serviço).  Essa instância do serviço Compose for PostgreSQL é implementada em uma organização pública do Cloud Foundry (não relacionada a organizações do CFEE). A organização pública do Cloud Foundry em que a instância do Compose for PostgresSQL é implementada tem um nome específico: **_cfee-`<accountId>`_**, em que "accountId" é o ID da conta do IBM Cloud em que o CFEE (junto com a instância de serviço do Compose for PostgreSQL) deve ser provisionado. A organização pública do Cloud Foundry é criada automaticamente quando o proprietário da conta cria uma instância do CFEE. A organização não é criada automaticamente quando um usuário que não é o proprietário da conta tenta criar a instância do CFEE (dessa forma, a tentativa de criação do CFEE falhará). Portanto, qualquer usuário da conta do IBM Cloud que cria instâncias do CFEE, mas não é o proprietário da conta, deve ser incluído na organização pública do Cloud Foundry **_cfee-`<accountId>`_** com uma **função de gerenciador**.   

   Para incluir um usuário da conta do IBM Cloud na organização pública _cfee-`<accountId>`_:
    * Acesse [**Gerenciar > Conta > Organizações do Cloud Foundry**](https://console.bluemix.net/account/organizations).
    * Clique na organização ** _ cfee-`<accountId>`_**.
    * Acesse a guia **Usuários** na parte superior da página.
    * Localize o usuário que precisa criar instâncias do CFEE e clique na caixa de seleção **Gerenciador** para esse usuário. Se o usuário que você deseja que seja capaz de criar instâncias do CFEE não estiver na lista, clique em **Incluir ou convidar usuário** acima da tabela para incluir ou convidar usuários para a organização **_cfee-`<accountId>`_**.

   **Nota**: embora a organização pública **_cfee-`<accountId>`_** seja criada implícita e automaticamente quando o proprietário da conta do IBM Cloud cria uma instância do CFEE, o proprietário da conta (e somente o proprietário da conta) pode criar a organização pública do Cloud Foundry manualmente, sem a necessidade de criar uma instância do CFEE. O proprietário da conta do IBM Cloud pode criar a organização pública _cfee-`<accountId>`_ manualmente na página **Gerenciar > Conta > Organizações do Cloud Foundry**. Se você for o proprietário da conta e criar a organização pública _cfee-`<accountId>`_, certifique-se de nomeá-la exatamente como _cfee-`<accountId>`_. Para localizar o ID da conta do IBM Cloud, acesse a página [**Gerenciar > Conta > Organizações do Cloud Foundry**](https://console.bluemix.net/account/organizations) e consulte a URL da página disponível em seu navegador. O ID da conta do IBM Cloud é o conjunto de valores alfanuméricos após o `=` na URL da página. Como alternativa, é possível acessar a página __Gerenciar > Conta > Usuários__ e passar o mouse sobre a dica de ferramenta à esquerda do nome da _Conta_ localizado no canto superior direito da página.
   
* Função de administrador ou de editor para o serviço {{site.data.keyword.Bluemix_notm}} Container no grupo de recursos ao qual o ambiente está designado. As instâncias do {{site.data.keyword.cfee_full_notm}} são implementadas na infraestrutura de cluster de contêiner, que é fornecida pelo serviço {{site.data.keyword.Bluemix_notm}} Container. Quando você cria uma instância do serviço {{site.data.keyword.cfee_full_notm}}, o serviço cria automaticamente um cluster do Kubernetes no qual o {{site.data.keyword.cfee_full_notm}} é implementado. O acesso ao serviço IBM Container, especificamente no grupo de recursos ao qual o ambiente está designado, é necessário para criar essa infraestrutura de cluster.

Para confirmar que você tem as políticas de acesso necessárias para criar uma instância do {{site.data.keyword.cfee_full_notm}}:
1. Acesse o menu [**Gerenciar > Conta > Usuários**](https://console.bluemix.net/iam/#/users) no cabeçalho do {{site.data.keyword.Bluemix_notm}} para abrir a página **Identidade e acesso**.
2. Na guia Políticas de acesso, clique no usuário que está criando o ambiente.
3. Confirme se as políticas de acesso para o usuário que está criando o ambiente são consistentes com as políticas descritas anteriormente.

A tela a seguir ilustra as políticas de acesso como elas apareceriam na página Identidade e acesso do {{site.data.keyword.Bluemix_notm}} que permitem que um usuário crie uma instância do {{site.data.keyword.cfee_full_notm}}.

![Access policies](img/AccessPolicies_Creator.png)

## Permissões necessárias para trabalhar com um ambiente
{: #perm-working}

Para trabalhar com uma instância do {{site.data.keyword.cfee_full_notm}}, os usuários devem:
1. Ser membros da conta do {{site.data.keyword.Bluemix_notm}} em que a instância do {{site.data.keyword.cfee_full_notm}} foi criada.
2. Ter as _Políticas de acesso_ a seguir concedidas a eles pelo administrador de conta (consulte a página _Identidade e acesso_ sob o menu [**Gerenciar > Conta > Usuários**](https://console.bluemix.net/iam/#/users) no cabeçalho do {{site.data.keyword.Bluemix_notm}} para verificar suas políticas de acesso de conta atuais):
  - Acesso a pelo menos um grupo de recursos na conta do {{site.data.keyword.Bluemix_notm}}. Os grupos de recursos permitem organizar recursos em agrupamentos customizados para facilitar o controle de acesso a esses recursos. Você será solicitado a fornecer um grupo de recursos ao criar uma nova instância de ambiente.
  - Os usuários devem ter acesso designado ao serviço {{site.data.keyword.cfee_full_notm}} no grupo de recursos sob o qual a instância do ambiente foi criada. O nível de acesso e controle que os usuários têm em uma instância do {{site.data.keyword.cfee_full_notm}} depende da função que é concedida na política de acesso:
     - Os usuários designados às funções de administrador ou editor podem criar organizações, designar gerenciadores para organizações e espaços, ter permissões completas para todas as organizações e os espaços dentro do ambiente e executar ações operacionais usando a API do Cloud Controller. A esses usuários é concedido automaticamente o _escopo cloud_controller.admin_ no _escopo User Account and Authentication_ do Cloud Foundry.
     - Os usuários designados a uma função de visualizador podem ver esse ambiente no painel principal do {{site.data.keyword.Bluemix_notm}} e podem abrir sua interface com o usuário. O acesso de usuários a organizações e espaços específicos no ambiente é controlado pelas funções específicas de organização e espaços que são designadas pelos gerenciadores dessas organizações e espaços. Para obter mais informações, consulte [Incluindo usuários em organizações](add-users.html).

A imagem ilustra as políticas de acesso mínimo (como elas apareceriam na página _Identidade e acesso_ do {{site.data.keyword.Bluemix_notm}}) necessárias para acessar um {{site.data.keyword.cfee_full_notm}}.

![Access policies](img/AccessPolicies_User.png)

