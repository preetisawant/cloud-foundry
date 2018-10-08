---

copyright:
  years: 2018
lastupdated: "2018-09-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Trabalhando com Serviços
{: #workingwith-services}

Os aplicativos implementados em um {{site.data.keyword.cfee_full_notm}} podem ser ligados a dois tipos de instâncias de serviço:
1. Instâncias de serviço público criadas por meio do catálogo do {{site.data.keyword.Bluemix}} e disponíveis na conta do {{site.data.keyword.Bluemix}}.  
As instâncias de serviço público disponíveis na conta do {{site.data.keyword.Bluemix}} não podem estar disponíveis, por si só, para ambientes CFEE.  Para que uma instância de serviço público (disponível na conta do {{site.data.keyword.Bluemix}}) fique disponível para espaços em um ambiente do CFEE, elas precisam ser incluídas especificamente no espaço do CFEE de destino. Depois que a instância de serviço do {{site.data.keyword.Bluemix}} for incluída no espaço do CFEE, ela poderá ser ligada a aplicativos nesse espaço do CFEE. Isso permite que os desenvolvedores usem o vasto catálogo de serviços do {{site.data.keyword.Bluemix}} em seus aplicativos implementados em ambientes do CFEE, ao mesmo tempo em que permite o controle de acesso a esses serviços do {{site.data.keyword.Bluemix}}.

   Além de incluir instâncias de serviço existentes do {{site.data.keyword.Bluemix}} em um espaço do CFEE, é possível criar uma nova instância de serviço do {{site.data.keyword.Bluemix}} dentro de um espaço do CFEE, o que também a inclui automaticamente nesse espaço do CFEE.

2. Instâncias de serviço gerenciadas por um broker de serviço do Cloud Foundry local (local para o CFEE). Estas, por sua vez, podem ser de dois tipos:
   *  2a. Uma instância de uma oferta de serviços criada por meio do marketplace do Cloud Foundry da instância atual do {{site.data.keyword.cfee_full_notm}}. Esse tipo de instância de serviço requer um broker de serviço registrado disponível no ambiente. Um broker de serviço mostra um catálogo de ofertas de serviços e planos, assim como permite a criação, remoção, ligação e desvinculação de instâncias dessas ofertas de serviços. Consulte [Gerenciando brokers de serviço](https://docs.cloudfoundry.org/services/managing-service-brokers.html) na documentação do Cloud Foundry para obter mais informações.
   * 2b. Uma instância de serviço fornecida pelo usuário. A criação desse tipo é suportada por meio da CLI, mas não por meio da interface com o usuário. No entanto, as instâncias de serviço fornecidas pelo usuário serão listadas na interface com o usuário.
   

## Visualizando instâncias de serviço do {{site.data.keyword.Bluemix_notm}} em todos os ambientes do CFEE
{: #viewing-services_across}

Acesse o [painel de serviços do Cloud Foundry](https://console.bluemix.net/dashboard/cloudfoundry/services) para ter uma visualização consolidada de todas as instâncias de serviço do {{site.data.keyword.Bluemix_notm}} (às quais você tem acesso) na conta do {{site.data.keyword.Bluemix_notm}} e ver quais foram incluídas em quais espaços do CFEE.

Essa visualização mostra todos os aliases do {{site.data.keyword.Bluemix_notm}} disponíveis na conta e indica quais deles foram incluídos (com alias) em quais espaços do CFEE. Expanda uma instância de serviço para mostrar os espaços do CFEE nos quais ela foi incluída. É possível expandi-las ainda mais para ver os aplicativos nos espaços do CFEE aos quais tais instâncias de serviço foram ligadas.   

Nessa visualização, também é possível ligar os aplicativos implementados aos espaços do CFEE nos quais essas instâncias de serviço foram incluídas. Acesse o menu localizado na extremidade direita da linha da tabela para o serviço correspondente (disponível para um espaço do CFEE específico) e selecione **Ligar aos aplicativos**.

## Incluindo instâncias de serviço existentes do {{site.data.keyword.Bluemix_notm}} em um espaço do CFEE
{: #adding-services_inspace}

É possível ligar uma instância de serviço do {{site.data.keyword.Bluemix_notm}} aos aplicativos implementados em um espaço do CFEE. Antes que uma instância de serviço do IBM Cloud possa ser ligada ao aplicativo implementado no CFEE, ela deverá ser incluída no espaço do CFEE no qual o aplicativo está implementado. As seguintes condições são necessárias antes de ser possível incluir uma instância de serviço do {{site.data.keyword.Bluemix_notm}} em um Espaço do CFEE:
* O serviço do {{site.data.keyword.Bluemix_notm}} deve estar disponível na mesma conta do {{site.data.keyword.Bluemix_notm}} na qual a instância do CFEE reside.
* Deve-se ter acesso à instância de serviço do {{site.data.keyword.Bluemix_notm}} em si. Para obter mais informações, consulte a página Identidade e acesso sob o menu **Gerenciar > Usuários** no cabeçalho do {{site.data.keyword.Bluemix_notm}} para verificar as suas políticas de acesso de conta atuais.

Para incluir uma instância de serviço existente do {{site.data.keyword.Bluemix_notm}} em um espaço do CFEE:
1. Acesse o [painel de serviços do Cloud Foundry](https://console.bluemix.net/dashboard/cloudfoundry/services).  
2. Localize a instância de serviço do {{site.data.keyword.Bluemix_notm}} na lista e chame o menu na extremidade direita da linha da tabela correspondente.
3. Selecione  ** Incluir serviço **.
4. No diálogo _Incluir serviço_, selecione o CFEE, a organização e o espaço nos quais você deseja incluir o serviço e clique em **Incluir**.
5. Expanda o serviço de destino do {{site.data.keyword.Bluemix_notm}} para localizar o novo CFEE no qual o serviço foi incluído.


Como alternativa, é possível incluir a instância de serviço do {{site.data.keyword.Bluemix_notm}} dentro do espaço do CFEE no qual você deseja incluí-la:
1. Em seu [painel](https://console.bluemix.net/dashboard) do {{site.data.keyword.Bluemix_notm}} ou no [painel de serviço do Cloud Foundry](https://console.bluemix.net/dashboard/cloudfoundry/services), localize o ambiente do Cloud Foundry Enterprise que hospeda o seu aplicativo.
2. Acesse **Organizações** na área de janela de navegação e abra a organização e o espaço nos quais o aplicativo está localizado.
3. Acesse a guia **Espaços** e localize o espaço que contém o aplicativo.
4. Na página de espaço de destino, acesse a guia **Serviços** e clique em **Incluir serviço**. Isso abrirá o diálogo __Incluir serviço__. A página lista as instâncias de serviços disponíveis na conta do {{site.data.keyword.Bluemix_notm}}.
5. Localize e selecione uma instância de serviço disponível que deseja incluir no espaço do CFEE. 
6. A instância de serviço será incluída na lista de serviços disponíveis no espaço do CFEE.

   **Nota:** ao incluir um serviço do {{site.data.keyword.Bluemix_notm}} em um espaço do CFEE, um alias para essa instância de serviço é criado nesse espaço. Ao **Remover** a instância de serviço de um espaço do CFEE (no menu localizado na extremidade direita da linha da instância de serviço correspondente na tabela), o serviço não é excluído da conta pública. A ação simplesmente o remove da conta específica do CFEE e ele não fica mais disponível para ligação a aplicativos nesse espaço do CFEE. Além disso, ao excluir a própria instância de serviço da conta do {{site.data.keyword.Bluemix_notm}}, o serviço não ficará mais disponível para nenhum espaço do CFEE. 

## Criando instâncias de serviço do {{site.data.keyword.Bluemix_notm}} em uma IU de espaço do CFEE
{: #creating-services_inspace}
É possível criar instâncias de serviço do {{site.data.keyword.Bluemix_notm}} dentro de um espaço do CFEE. A criação de uma instância de serviço do {{site.data.keyword.Bluemix_notm}} resulta no seguinte:
* A instância de serviço do {{site.data.keyword.Bluemix_notm}} é criada no IBM Cloud.  Isso é equivalente a criar a instância de serviço no [catálogo](https://console.bluemix.net/catalog) do {{site.data.keyword.Bluemix_notm}}.
* A instância de serviço do {{site.data.keyword.Bluemix_notm}} é incluída (com alias) no espaço do CFEE no qual a ação de criação foi iniciada.


Para criar uma instância de serviço dentro de um espaço do CFEE:
1. Na página de espaço de destino, acesse a guia **Serviços** e clique em **Criar serviço**.  Isso abrirá a visualização **Mercado** para o {{site.data.keyword.cfee_full_notm}}. A visualização lista ofertas de serviços de duas origens (veja a coluna __Origem__):
   * Ofertas do catálogo do {{site.data.keyword.Bluemix_notm}}.
   * Ofertas do  {{site.data.keyword.cfee_full_notm}}  marketplace local.
5. Localize e selecione uma oferta de serviço disponível que você deseja instanciar. 
6. Dependendo da origem da oferta de serviços (catálogo do IBM Cloud ou mercado do CFEE local), tome uma das seguintes ações:
   * Se a oferta de serviços selecionada for uma oferta de catálogo do {{site.data.keyword.Bluemix_notm}}, você verá um botão para **Continuar** na página de criação da oferta de serviços do IBM Cloud. Essa é a mesma página disponível no catálogo do {{site.data.keyword.Bluemix_notm}}. Nessa página, você fornece o nome da nova instância de serviço, a região, o plano e outras propriedades obrigatórias para criar o serviço no IBM Cloud. Depois de criar a instância de serviço, ela será criada no IBM Cloud e automaticamente incluída no espaço atual do CFEE.
   * Se a oferta de serviços selecionada for fornecida no catálogo local do CFEE, você verá um botão para **Criar** a instância de serviço. Você será solicitado a fornecer uma organização e um espaço no CFEE atual no qual a instância de serviço será criada.

## Criando instâncias de serviço do {{site.data.keyword.Bluemix_notm}} em um espaço do CFEE usando a CLI
{: #creating-services_cli}

É possível criar uma instância de serviço por meio da CLI de um espaço em um CFEE. A criação de um serviço por meio da CLI em um espaço do CFEE é equivalente a criá-lo em uma IU nesse espaço. Ou seja, a criação de um serviço tem o resultado duplo a seguir:
* A instância de serviço do {{site.data.keyword.Bluemix_notm}} é criada no IBM Cloud. Isso é equivalente a criar a instância de serviço no [catálogo](https://console.bluemix.net/catalog) do {{site.data.keyword.Bluemix_notm}}.
* A instância de serviço do {{site.data.keyword.Bluemix_notm}} é incluída (com alias) no espaço do CFEE no qual a ação de criação foi iniciada.

A diferença entre a criação de uma instância de serviço em um espaço do CFEE versus a criação da CLI está no ciclo de vida da instância de serviço criada. Quando você cria a instância de serviço na IU de espaço do CFEE, o ciclo de vida da instância de serviço criada é controlado na própria instância de serviço na conta do {{site.data.keyword.Bluemix_notm}}. Isso significa que as atualizações no plano de serviço são controladas na instância na conta do {{site.data.keyword.Bluemix_notm}}, não no espaço do CFEE. Como alternativa, se a instância de serviço for criada na CLI, o ciclo de vida do serviço será controlado no espaço do CFEE (o serviço é atualizado no espaço do CFEE).

As instâncias de serviço criadas na CLI também são exibidas na IU e são indicadas por um ` * ` próximo ao nome da instância de serviço.

Para criar instâncias de serviço usando a CLI, siga as etapas a seguir:

1. Faça download e instale a interface da linha de comandos do {{site.data.keyword.Bluemix}} (caso ainda não o tenha feito). [Download da CLI do Cloud Foundry](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html){: new_window} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo").

2. Acesse a página Visão geral do {{site.data.keyword.cfee_full}} e localize o terminal de API do ambiente.

3. Na interface da linha de comandos, configure o terminal de API para o terminal do ambiente do CFEE:

  ```
  cf api <api_enpoint>
  ```
  {: pre}

4. Efetue login no ambiente do CFEE:

  ```
  cf login -u <username> -o <org_name> -s <space_name>
  ```
  {: pre}

  Se você estiver usando um ID federado, use a opção `-sso`:

  ```
  cf login -o <org_name> -s <space_name> -sso
  ```
  {: pre}
  
5. Crie o serviço:
  
  ```
  cf create-service SERVICE PLAN SERVICE_INSTANCE -c '{"name":"value","name":"value"}'
  ```
  {: pre}

  Opcionalmente, é possível fornecer um arquivo contendo parâmetros em um objeto JSON válido necessário para criar um serviço específico.
  O caminho para o arquivo de parâmetros pode ser um caminho absoluto ou relativo para um arquivo:
  
  ```
  cf create-service SERVICE PLAN SERVICE_INSTANCE -c PATH_TO_FILE
  ```
  {: pre}
   
  A seguir está um exemplo de um objeto JSON válido:
   
  ```
   {
      "cluster_nodes": {
         "count": 5,
         "memory_mb": 1024
      }
   }
  ```
  {: pre}
  
   Para obter ajuda para criar um serviço na CLI, emita o seguinte:
  
  ```
  cf cs -help
  ```
  Veja [Gerenciando instâncias de serviço com a CLI cf](https://docs.cloudfoundry.org/devguide/services/managing-services.html){: new_window} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo") na documentação do Cloud Foundry para obter mais informações.
  
## Ligando serviços a aplicativos
{: #bind_services}

É possível ligar uma instância de serviço a um aplicativo implementado em um CFEE no [painel de serviços do Cloud Foundry](https://console.bluemix.net/dashboard/cloudfoundry/services) ou na guia Serviços de uma página de espaço do CFEE.  

Para ligar uma instância de serviço a um aplicativo no [painel de serviços do Cloud Foundry](https://console.bluemix.net/dashboard/cloudfoundry/services):
1. Acesse o [painel de serviços do Cloud Foundry](https://console.bluemix.net/dashboard/cloudfoundry/services) para ter uma visualização consolidada de todas as instâncias de serviço do {{site.data.keyword.Bluemix_notm}} disponíveis para você na conta do {{site.data.keyword.Bluemix_notm}}. A visualização também é destinada a mostrar quais instâncias de serviços do {{site.data.keyword.Bluemix_notm}} estão disponíveis (com alias) em quais espaços do CFEE. É possível expandir uma instância de serviço para mostrar os espaços do CFEE nos quais ela foi incluída. É possível expandi-las ainda mais para ver os aplicativos nos espaços do CFEE aos quais tais instâncias de serviço foram ligadas. 
2. Localize a instância de serviço do {{site.data.keyword.Bluemix_notm}} que você deseja ligar.
3. Expanda a visualização correspondente para ver todos os espaços do CFEE nos quais essa instância de serviço foi incluída. Se essa instância de serviço não tiver sido incluída no espaço do CFEE no qual o aplicativo está implementado, selecione **Incluir** no menu na extremidade direita da linha para tornar a instância de serviço disponível no espaço do CFEE de destino.
4. Acesse o menu localizado na extremidade direita da linha correspondente ao CFEE/espaço no qual a instância de serviço está disponível e selecione **Ligar aplicativo**.
5. No diálogo __Ligar aplicativo__, selecione o aplicativo que você deseja ligar.
6. O aplicativo agora está ligado à instância de serviço no espaço do CFEE no qual o aplicativo está implementado. É possível expandir a linha para a linha correspondente na tabela para ver os aplicativos ligados no espaço do CFEE.


Para ligar um aplicativo a uma instância de serviço na página __Serviços__ de um espaço do CFEE:

1. Abra a interface com o usuário do CFEE na qual o aplicativo está implementado.
2. Acesse **Organizações** na área de janela de navegação à esquerda e abra a organização e o espaço nos quais o aplicativo está implementado.
3. Acesse a guia **Espaços** e localize o espaço que contém o aplicativo.
4. Na página de espaço de destino, acesse a guia **Serviços**.
5. Na tabela de **Instâncias de serviço**, acesse o menu __Ações__ na extremidade direita da linha correspondente à instância de serviço que deseja ligar e selecione **Ligar**.
6. Selecione o aplicativo que você deseja ligar à instância de serviço.

Para desvincular um aplicativo de uma instância de serviço:

1. Na guia **Serviços** do espaço, expanda a instância de serviço de destino para mostrar os apps que estão ligados a ela.
2. Acesse o menu Ações em uma linha do aplicativo e selecione **Desvincular serviço**.

Veja [Ligar uma instância de serviço](https://docs.cloudfoundry.org/devguide/services/application-binding.html){: new_window} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo") na documentação do Cloud Foundry para obter mais informações sobre como ligar aplicativos usando a CLI.


