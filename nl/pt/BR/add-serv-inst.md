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

# Criando e Visualizando Instâncias de Serviço
{: #creating-services}

Os aplicativos implementados em um {{site.data.keyword.cfee_full_notm}} podem ser ligados a dois tipos de instâncias de serviço:
1. Instâncias de serviço gerenciadas por um broker de serviço do Cloud Foundry local (local para o CFEE). Estas, por sua vez, podem ser de dois tipos:
   *  1a. Uma instância de uma oferta de serviços criada por meio do marketplace do Cloud Foundry da instância atual do {{site.data.keyword.cfee_full_notm}}. Esse tipo de instância de serviço requer um broker de serviço registrado disponível no ambiente. Um broker de serviço mostra um catálogo de ofertas de serviços e planos, assim como permite a criação, remoção, ligação e desvinculação de instâncias dessas ofertas de serviços. Consulte [Gerenciando brokers de serviço](https://docs.cloudfoundry.org/services/managing-service-brokers.html) na documentação do Cloud Foundry para obter mais informações.
   * 1b. Uma instância de serviço fornecida pelo usuário. A criação desse tipo é suportada por meio da CLI, mas não por meio da interface com o usuário. No entanto, as instâncias de serviço fornecidas pelo usuário serão listadas na interface com o usuário.
2. Instâncias de serviço público criadas por meio do catálogo do {{site.data.keyword.Bluemix}} e disponíveis na conta do {{site.data.keyword.Bluemix}}.
As instâncias de serviço público disponíveis na conta do {{site.data.keyword.Bluemix}} não podem estar disponíveis, por si só, para ambientes CFEE. Para que uma instância de serviço público (disponível na conta do {{site.data.keyword.Bluemix}}) se torne disponível para espaços em um ambiente do CFEE, um alias para a instância de serviço deve ser criado no espaço do CFEE de destino. O alias funciona como uma referência para a instância de serviço público real. Depois que o alias do serviço é criado em um espaço do CFEE, ele pode ser ligado a aplicativos nesse CFEE. O aliasing de serviço permite que os desenvolvedores aproveitem o vasto catálogo de serviços do {{site.data.keyword.Bluemix}} em seus aplicativos implementados em ambientes do CFEE.


## Criando e visualizando aliases do serviço em um espaço do CFEE
{: #creating-services_inspace}

Um alias para uma instância de serviço público existente disponível em sua conta do IBM Cloud permite que você ligue essa instância de serviço aos aplicativos implementados em um espaço do CFEE. A criação de um alias para uma instância de serviço existente do {{site.data.keyword.Bluemix_notm}} requer acesso de usuário à instância em si. Para obter mais informações, consulte a página Identidade e acesso sob o menu **Gerenciar > Usuários** no cabeçalho do {{site.data.keyword.Bluemix_notm}} para verificar as suas políticas de acesso de conta atuais.

Para criar um alias de instância de serviço em um espaço em um CFEE:

1. Em seu painel do {{site.data.keyword.Bluemix_notm}}, localize o ambiente do Cloud Foundry Enterprise que hospeda seu aplicativo.
2. Acesse **Organizações** na área de janela de navegação e abra a organização e o espaço nos quais o aplicativo está localizado.
3. Acesse a guia **Espaços** e localize o espaço que contém o aplicativo.
4. Na página de espaço de destino, acesse a guia **Serviços** e clique em **Criar serviço**. Isso abrirá a página **Catálogo** para o {{site.data.keyword.cfee_full_notm}}. A página lista as ofertas de serviços de duas origens (veja a coluna _Origem_):
   * Ofertas do catálogo do IBM Cloud.
   * Ofertas do  {{site.data.keyword.cfee_full_notm}}  marketplace local.
5. Localize e selecione uma oferta de serviço disponível que você deseja instanciar.
6. Dependendo da origem da oferta de serviços (IBM Cloud ou CFEE local), continue com um dos seguintes:
   * **Continue** com a página de criação da oferta de serviços do IBM Cloud para fornecer o nome da nova instância de serviço, região, plano e outras propriedades necessárias para criar o serviço no IBM Cloud. Após você clicar em *Criar*, a instância de serviço será criada no IBM Cloud. Além disso, um alias dessa instância de serviço será criado no {{site.data.keyword.cfee_full_notm}}. O alias estará disponível para ligação com os aplicativos no {{site.data.keyword.cfee_full_notm}}.
   **Nota:** ao criar um {{site.data.keyword.Bluemix_notm}} nesse modo, além de criar uma instância pública disponível para usuários na conta do IBM Cloud, um alias para essa instância de serviço é criado no {{site.data.keyword.cfee_full_notm}} por meio do qual ele foi criado.
   * **Crie** a instância de serviço no marketplace do Cloud Foundry local. Isso abrirá um diálogo no qual você fornece o nome da nova instância de serviço e o plano. Depois de clicar em *Criar*, a instância de serviço será criada no {{site.data.keyword.cfee_full_notm}} e estará disponível para ligação com aplicativos no {{site.data.keyword.cfee_full_notm}}.

Após a instância de serviço ser criada, a instância de serviço (se ela for criada no marketplace do Cloud Foundry local) ou o alias (se a instância de serviço foi criada por meio do catálogo do IBM Cloud) será listado sob a guia **Serviços**.


## Criando e visualizando aliases de serviço em todos os ambientes do CFEE no painel do Cloud Foundry global
{: #creating-services_across}

É possível ver uma visualização consolidada de todos os aliases de instância de serviço (em todas as instâncias do CFEE) no painel do Cloud Foundry global.

1. Clique no ícone de Menu ![Verificação de conta](img/HamburgerMenu.png "Captura de tela que mostra o ícone de menu") > **Cloud Foundry** para abrir o painel do Cloud Foundry.
2. Clique em **Corporativo > Serviços** na área de janela de navegação esquerda.
A tabela na visualização mostra as informações a seguir:

| Elemento   | Descrição |
|-----------|---------------|
| Alias de Serviço | O nome do alias da instância de serviço. |
| Instância de serviço | A instância de serviço público do IBM Cloud na qual o alias é criado. |
| Oferta | A oferta de serviços do catálogo do IBM Cloud na qual a instância de serviço foi criada. |
| CFEE | O  {{site.data.keyword.cfee_full}}  onde o alias reside. |
| Organização | A organização na instância do CFEE na qual o alias reside. |
| Espaço | O espaço dentro da organização na instância do CFEE na qual o alias reside. |
{:caption="Tabela 1. Descrição dos elementos-chave" caption-side="top"}

É possível executar as ações a seguir nessa visualização:
* Classifique os itens na tabela por qualquer uma das propriedades exibidas como colunas da tabela.
* Ligue os aplicativos a um alias específico acessando o menu overflow do alias localizado na extrema direita da linha.
* Expanda um alias (linha) para ver todos os aplicativos ligados a esse alias.
* Inicie, pare aplicativos acessando o menu overflow do aplicativo do alias localizado na extrema direita da linha.
* Navegue até um CFEE, uma organização do CFEE ou um espaço do CFEE clicando no link com o CFEE, a organização ou o espaço correspondente.

Para criar um alias de serviço no painel global do Cloud Foundry:
1. Clique no botão **Criar alias do serviço** na parte superior da página. Isso abrirá o diálogo _Criar alias do serviço_. O diálogo lista todas as instâncias de serviço público disponíveis na conta atual do IBM Cloud.
2. Selecione uma das instâncias de serviço público.
3. Clique em **Criar**. Depois de criado, o novo alias da instância de serviço será incluído na lista.
O alias do serviço também aparecerá na lista de serviços no espaço do CFEE, no qual ele pode ser ligado a aplicativos nesse espaço (CFEE > Organizações > Espaço > Serviços).


