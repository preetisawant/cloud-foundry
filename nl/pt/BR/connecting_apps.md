---

copyright:
  years: 2017, 2018
lastupdated: "2018-01-18"

---

{:shortdesc: .shortdesc}

# Gerenciando conexões
{: #connect_app}

É possível conectar um serviço a um aplicativo {{site.data.keyword.Bluemix}} existente ou novo na guia **Conexões** do painel de serviço. Conectar um serviço Cloud Foundry a um aplicativo Cloud Foundry cria uma ligação entre eles e é possível desvincular, incluir conexões adicionais ou excluir conexões na guia **Conexões**.

No entanto, quando você conecta uma instância de serviço que é gerenciada pelo {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) a um aplicativo Cloud Foundry, um alias do serviço gerenciado pelo IAM é automaticamente criado no espaço correspondente do Cloud Foundry com as informações de ligação que você especificou. Esse alias é representado como uma instância de serviço Cloud Foundry de seu serviço gerenciado pelo IAM.
{:shortdesc}

## O que é um alias?
{: #what_is_alias}

Um alias é uma conexão entre o seu serviço gerenciado pelo IAM em um grupo de recursos e um aplicativo Cloud Foundry dentro de uma organização ou um espaço. No console do {{site.data.keyword.Bluemix_notm}}, a conexão (alias) é representada como uma instância de serviço Cloud Foundry. É possível gerenciar seus alias modificando a instância de serviço que representa sua conexão.

Os aliases são como links simbólicos que contêm referências a recursos remotos e permitem a interoperabilidade e a reutilização de uma instância na plataforma. Por exemplo, é possível criar uma instância de um serviço em um grupo de recursos e, em seguida, reutilizá-la em qualquer região disponível do Cloud Foundry criando um alias em uma organização ou um espaço nessas regiões.

As regras a seguir se aplicam a aliases:

* Não há encargos extras para um alias, mas cada alias conta com relação à sua cota na organização do Cloud Foundry.
* É possível criar somente um alias por espaço do Cloud Foundry no console do {{site.data.keyword.Bluemix_notm}}. No entanto, mais de um alias por espaço pode ser criado usando o {{site.data.keyword.Bluemix_notm}} CLI. Para obter mais informações, consulte [Comandos para gerenciar recursos e grupos de recursos](/docs/cli/reference/bluemix_cli/bx_cli.html#commands-for-managing-resource-groups-and-resources).
* É possível criar múltiplas conexões entre seu serviço gerenciado pelo IAM e qualquer aplicativo Cloud Foundry em qualquer espaço, organização e região na mesma conta, se você tem a permissão.
* Múltiplas conexões feitas no mesmo espaço para diferentes apps Cloud Foundry de uma instância de serviço gerenciado pelo IAM usarão o mesmo alias.
* Desvincular uma instância de serviço gerenciado pelo IAM *não* excluirá a instância de serviço Cloud Foundry que representa o alias.
* Excluir o aplicativo Cloud Foundry ao qual sua instância de serviço gerenciado pelo IAM está conectada *não* excluirá a instância do Cloud Foundry que representa o alias.
* Excluir uma instância de serviço gerenciado pelo IAM *excluirá* a instância de serviço Cloud Foundry que representa o alias.

## Criando uma conexão (alias) entre um serviço gerenciado pelo IAM e um app Cloud Foundry
{: #creating_alias}

Para conectar sua instância de serviço gerenciado pelo IAM a um aplicativo Cloud Foundry:

1. Acesse seu painel.

2. Clique no nome do seu app para abrir a visualização de detalhes do app.

3. Clique em **Conectar existente** e escolha de seu app Cloud Foundry existente. Ou clique em **Criar conexão** para criar um app Cloud Foundry ao qual se conectar.

4. Especifique a **Função de acesso para conexão**. Este valor configura a função de acesso do serviço IAM. Para obter mais informações, veja [Acesso ao IAM](/docs/iam/users_roles.html#userroles).

5. Opcionalmente, é possível fornecer um **ID de serviço para conexão** permitindo que o IAM gere um valor exclusivo para você ou fornecendo um ID de serviço existente. Para obter mais informações, veja [Criando e gerenciando IDs de serviço](https://console.stage1.bluemix.net/docs/iam/serviceid.html#serviceids).

6. Clique em **Criar**.

## Visualizando um alias

Depois de criar uma conexão entre um serviço gerenciado pelo IAM e um app Cloud Foundry, o alias é exibido na guia **Conexões** do app Cloud Foundry conectado. Além disso, o alias é exibido como uma instância de serviço Cloud Foundry em execução em seu painel e contém uma guia **Conexões** somente quando você a abre.

1. Acesse seu painel.
2. Na tabela **Serviços do Cloud Foundry**, clique no nome da instância de serviço para abrir a visualização de detalhes do serviço. Se ele tiver somente uma guia **Conexões**, será um alias.

## Excluindo um alias

A maneira mais fácil de excluir o alias é excluir a instância de serviço gerenciado pelo IAM. No entanto, é possível manter sua instância de serviço gerenciado pelo IAM e excluir o alias diretamente.

1. Acesse seu painel.
2. Na tabela **Serviços do Cloud Foundry**, clique no nome da instância de serviço para abrir a visualização de detalhes do serviço. Se ele tiver somente uma guia **Conexões**, será um alias.
3. Exclua a instância.

## Criando uma conexão entre múltiplos serviços do Cloud Foundry
{: #cf}

Para obter mais detalhes sobre como ligar um serviço do Cloud Foundry a outro serviço do Cloud Foundry, veja [Usando serviços em outro serviço](../apps/reqnsi.html#add_service).
