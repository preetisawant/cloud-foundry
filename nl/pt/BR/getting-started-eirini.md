---

copyright:
  years: 2017, 2018
lastupdated: "2019-04-01"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Introdução à visualização técnica do Eirini
{: #getting-started-eirini}

O {{site.data.keyword.cfee_full}} (CFEE) é uma plataforma em nuvem para hospedar aplicativos e serviços na nuvem. O {{site.data.keyword.cfee_full_notm}} torna mais fácil escalar apps conforme o consumo cresce, simplificando o tempo de execução, o middleware e a infraestrutura para que você possa se concentrar em desenvolver apps.
{: shortdesc}

Este tutorial de introdução mostra como criar um {{site.data.keyword.cfee_full_notm}} por meio do plano de visualização técnica do Eirini, inclusão de usuários, criação de uma organização e espaços, implementação de apps e ligação desses apps a serviços.
Consulte [Projeto do Eirini](https://www.cloudfoundry.org/project-eirini/) para obter informações sobre o projeto de incubador do Eirini por meio do Cloud Foundry Foundation.

## Entendendo Permissões
{: #permissions}

Políticas de acesso corretas são necessárias antes da criação de instâncias do {{site.data.keyword.cfee_full_notm}}. Para obter mais informações, consulte [Permissões](https://cloud.ibm.com/docs/cloud-foundry/permissions.html).

## Etapa 1: Certifique-se de que a conta {{site.data.keyword.Bluemix_notm}} possa criar recursos de infraestrutura
{: #accountprep-environment}

As instâncias do CFEE são implementadas nos nós do trabalhador do Kubernetes por meio do Kubernetes Service.  [Prepare sua conta do IBM Cloud](https://cloud.ibm.com/docs/cloud-foundry/prepare-account.html)
para assegurar-se de que ela possa criar os recursos de infraestrutura necessários para uma instância do CFEE.

## Etapa 2: Criar sua instância do CFEE
{: #create-environment}

Antes de criar seu CFEE, certifique-se de estar na conta do {{site.data.keyword.Bluemix_notm}} em que
deseja criar o ambiente e ter as políticas de acesso necessárias (etapa 1 acima).

1.  Abra o [catálogo](https://cloud.ibm.com/catalog) do {{site.data.keyword.Bluemix_notm}}.

2.  Localize o serviço {{site.data.keyword.cfee_full_notm}} no catálogo e clique nele para abrir a página de visão geral para o serviço.  Essa primeira página fornece uma visão geral dos principais recursos do serviço. Clique em **Continue**.

3.  Configure a instância do CFEE a ser criada:
    * Selecione o plano de _Visualização técnica do Eirini_.
    * Insira um **Nome** para a instância do CFEE.
    * Selecione um **Grupo de recursos** sob o qual o ambiente está agrupado. Somente os grupos de recursos aos quais você tem acesso na conta do IBM Cloud atual serão listados no menu suspenso _Grupos de recursos_, o que significa que você precisa ter permissão para acessar pelo menos um grupo de recursos na conta para poder criar um CFEE.
    * Selecione a **Geografia** e **Localização** em que a instância de serviço deve
ser fornecida. Veja lista de [locais de provisionamento e os data centers disponíveis](https://cloud.ibm.com/docs/cloud-foundry/index.html#provisioning-targets){: new_window} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo") por geografia para o CFEE e serviços de apoio. 

4. As instâncias do CFEE são provisionadas em um cluster Kubernetes. As células do Cloud Foundry são provisionadas dentro de zonas do trabalhador no cluster Kubernetes. É possível configurar o local, o hardware e a criptografia do cluster:
    * Selecione o isolamento de hardware para o cluster Kubernetes:   
      * _Virtual-compartilhado_: os recursos de infraestrutura no cluster, como o hypervisor e o hardware físico, são distribuídos entre você e outros clientes IBM, mas cada nó do trabalhador é um único locatário para você.
      * _Virtual-dedicado_: os nós do trabalhador no cluster são hospedados na infraestrutura que é dedicada à sua conta.
    * Os dados no cluster são criptografados por padrão. Você tem a opção de desligar _Criptografar o disco local_.
    * Selecione a **Geografia** e a **Região** na qual o cluster Kubernetes será provisionado.
    * Selecione a **Zona** na qual os nós do trabalhador do Kubernetes serão implementados. As VLANs disponíveis são recuperadas automaticamente para as zonas selecionadas. Se nenhuma VLAN estiver disponível, elas serão criadas automaticamente.
    Iniciando no CFEE v2.2.0, as instâncias do CFEE podem operar atrás de uma **rede isolada**. É possível fornecer uma instância do CFEE em uma rede isolada, selecionando VLANs privadas na rede isolada. Assim que o CFEE for criado, os endereços IP para as instâncias do CFEE Compose for PostgreSQL e do Cloudant Object Storage, bem como para os balanceadores de carga de aplicativo ([ALBs](https://cloud.ibm.com/docs/containers/cs_ingress.html#private_ingress)) do cluster Kubernetes deverão ser roteados na rede isolada pelo administrador de rede para que o CFEE se torne operacional.
    
    Assim que o CFEE for criado, o cluster Kubernetes no qual o ambiente é provisionado aparecerá (como qualquer outro recurso em sua conta do IBM Cloud) no [painel](https://cloud.ibm.com/dashboard/apps/) do {{site.data.keyword.Bluemix_notm}}. Para obter mais informações, consulte [Documentação do Kubernetes Service](https://cloud.ibm.com/docs/containers/cs_why.html#cs_ov).

5.  Configure a capacidade do CFEE:
    * Selecione o **Número de células** para o CFEE. Estas são as células do aplicativo que hospedarão os aplicativos implementados no CFEE.  
    * Selecione o **Tamanho do nó**, que determina a capacidade das células do Cloud Foundry (CPU e memória).
    
    Além das células do aplicativo que você especifica acima, _Células do Plano de controle_ adicionais são criadas e reservadas para a operação e o controle da plataforma do Cloud Foundry em seu CFEE. 

    **Nota:** recomendamos que o VLAN Spanning seja ativado se os nós do trabalhador no cluster do Kubernetes forem provisionados em sub-redes diferentes.  Os nós do trabalhador em sub-redes diferentes poderão evitar a conectividade entre eles se o VLAN Spanning estiver desativado.  Veja a documentação do [VLAN Spanning](https://cloud.ibm.com/docs/containers/cs_subnets.html#vlan-spanning) para obter mais informações.
    
6.  Nos campos **Compose for PostgreSQL**, selecione uma das organizações públicas e, em seguida, selecione um dos espaços disponíveis nessa organização. A instância do Compose for PostgreSQL será provisionada no espaço selecionado. O Compose for PostgreSQL é uma dependência necessária do serviço CFEE.

    **Nota:** Em _Compose for PostgreSQL_ estão disponíveis para seleção apenas as organizações na localização em que você
pretende fornecer a instância do CFEE (etapa 4 acima) e às quais você tem acesso.  Dentro de uma organização específica, somente os espaços para os quais você tem acesso de _desenvolvedor_ estão disponíveis para seleção. 

7.  O **Resumo da ordem** no lado direito da página reflete o custo da instância do CFEE e os serviços auxiliares, juntamente com o total mensal estimado.

8.  Clique em **Criar**, que abre o painel do ambiente e indica o progresso da criação e o status.

**Nota:** após o início do processo de criação, uma linha da tabela para o CFEE
é mostrada no painel do {{site.data.keyword.Bluemix_notm}}, na _Lista de recursos_ e no
[painel Ambientes do Cloud Foundry](https://cloud.ibm.com/dashboard/cloudfoundry?filter=cf_environments).  O status na linha da tabela indica quando a criação está concluída.

O processo automatizado que cria o ambiente implementa a infraestrutura em um cluster do Kubernetes e a configura para torná-la pronta para uso. O processo leva de 90 a 120 minutos.

Depois que o CFEE for criado, você receberá múltiplos e-mails confirmando o fornecimento do CFEE e os serviços de
suporte, bem como e-mails notificando o status dos pedidos correspondentes.

Ao criar uma instância do CFEE, há três instâncias de serviço de suporte adicionais criadas na mesma conta do IBM Cloud. Essas instâncias de serviço de suporte são nomeadas após o nome da instância do CFEE. Portanto, a criação de um CFEE
resulta em um total de quatro instâncias de serviço criadas na conta do IBM Cloud:
* Instância do CFEE ("_cfeename_").
* Cluster Kubernetes ("_cfeename_-cluster"). O cluster fornece a infraestrutura na qual a instância do
CFEE é fornecida.
* Instância do Cloud Object Storage ("_cfeename_-cos"). A instância é usada para armazenar dados gerados
durante a criação de contêineres de aplicativo do CFEE (por exemplo, pacotes de aplicativos transferidos por upload,
buildpacks e executáveis compilados).
* Instância do Compose for PosgreSQL ("_cfeename_-postgres"). A instância é usada para armazenar dados do
Cloud Foundry na instância do CFEE (por exemplo, a implementação do aplicativo de auditoria e os eventos de início e
de encerramento e, ao mesmo tempo, manter os registros de participação do usuário, organizações, espaços, aplicativos e
conexões de serviço do CFEE). 

## Etapa 3: Criar organizações e espaços
{: #create-orgsandspaces}

Depois de criar o {{site.data.keyword.cfee_full_notm}}, consulte [Criando organizações e espaços](https://cloud.ibm.com/docs/cloud-foundry/orgs-spaces.html) para obter informações sobre como estruturar o ambiente criando organizações e espaços. Os apps em um {{site.data.keyword.cfee_full_notm}} têm o escopo definido em espaços específicos. Por sua vez, existe um espaço dentro de uma organização específica. Os membros de uma organização compartilham um plano de cota, apps, instâncias de serviços e domínios customizados.

Quando você criar uma organização, designará uma cota para ela. A cota define limites sobre os recursos (memória, cpu etc.) disponíveis para essa organização. É possível designar uma cota diferente em um momento posterior. Há um conjunto de cotas pré-configuradas disponíveis em cada CFEE, mas também é possível criar as suas próprias cotas customizadas na página **Cotas** da interface com o usuário do CFEE. É possível fazer uma cota customizada a cota _Padrão_ chamando a ação _Copiar para padrão_ no menu da cota, que copia os valores da cota customizada para a cota padrão.

**Nota:** a página _Organizações do Cloud Foundry_ disponível no menu **_Gerenciar > Conta > Organizações do Cloud Foundry_** localizado no cabeçalho superior do IBM Cloud é destinada exclusivamente para organizações públicas do IBM Cloud, **não para organizações do CFEE**. As organizações do CFEE são gerenciadas na página _Organizações_ de uma instância do CFEE.  Abra a interface com o usuário do CFEE e clique na página **_Organizações_** para criar e gerenciar organizações para esse CFEE.

## Etapa 4: Incluir usuários em organizações e espaços
{: #add-users}

[Inclua usuários](https://cloud.ibm.com/docs/cloud-foundry/add-users.html) nessas organizações e espaços sob designações de função específicas que controlam seu nível de acesso.  Para que os usuários possam ser incluídos como membros de organizações e espaços em um CFEE, esses usuários devem ter acesso anterior à instância do CFEE. Consulte  [ Permissões ](https://cloud.ibm.com/docs/cloud-foundry/permissions.html).

## Etapa 5: Implementar e visualizar aplicativos
{: #deploy-apps}

Quando você estiver pronto, será possível [implementar o app](https://console.bluemix.net/docs/cloud-foundry/deploy-apps.html) com a interface da linha de comandos do {{site.data.keyword.Bluemix_notm}}.  Visualize a lista de aplicativos implementados na interface com o usuário, seja no contexto de um espaço específico do CFEE ou globalmente em todas as instâncias do CFEE.  Também é possível iniciar, parar ou excluir aplicativos dessas visualizações.

## Etapa 6: Criar ou incluir instâncias de serviço do IBM Cloud em espaços do CFEE
{: #service-instances}

[Criar serviços](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#workingwith-services#creating-services-inspace) ou [Incluir serviços existentes](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#workingwith-services#adding-services-inspace) disponíveis na conta do IBM Cloud.  Depois que uma instância de serviço estiver disponível em um espaço do CFEE, será possível ligá-lo aos aplicativos CFEE implementados nesse espaço.

## Etapa 7: Ligar aplicativos às instâncias de serviço
{: #bind-apps}

[Ligue seu app](https://console.bluemix.net/docs/cloud-foundry/binding.html) a um alias da instância de serviço para usar as funções do serviço.

No [painel do Cloud Foundry](https://console.bluemix.net/dashboard/cloudfoundry/overview){: new_window} ![Ícone delink externo](../icons/launch-glyph.svg "Ícone de link externo"), é possível ver uma visualização consolidada de todos os aplicativos e serviços, tanto

*públicos* quanto *corporativos*.  Uma vez no painel do Cloud Foundry, clique em *Públicos* na área de janela de navegação à esquerda para ver os aplicativos públicos e os serviços disponíveis na conta do IBM Cloud.  Clique
em *Corporativo* para ver todos os ambientes do CFEE, os aplicativos implementados nos espaços do
CFEE e os serviços disponíveis para os espaços do CFEE.
{:tip}

## Etapa 8: Instale o Stratos Console para gerenciar aplicativos (opcional)
{: #install-stratos}

O Stratos Console é uma ferramenta baseada na web de software livre para trabalhar com o Cloud Foundry. O aplicativo Stratos Console pode ser instalado opcionalmente e usado em um ambiente específico do CFEE para gerenciar suas organizações, espaços e aplicativos.

Os usuários com as funções de administrador ou editor do IBM Cloud na instância do CFEE podem instalar o aplicativo Stratos Console nessa instância do CFEE.

Para instalar o aplicativo Stratos Console:

1. Abra a instância do CFEE na qual você deseja instalar o Stratos Console.
2. Clique em **Instalar o Stratos Console** na página de visão geral. O botão fica visível somente para usuários com permissões de administrador ou de editor para essa instância do CFEE.
3. No diálogo Instalar o Stratos Console, selecione uma opção de instalação. É possível instalar o aplicativo Stratos em
uma célula do Cloud Foundry ou no cluster Kubernetes. Selecione uma versão do Stratos Console e o número de instâncias do aplicativo a ser instalado. Se
você instalar o aplicativo Stratos Console em uma célula do Cloud Foundry, será solicitado que você forneça a organização
e o espaço nos quais o aplicativo será implementado.
4. Clique em **Instalar**.

O aplicativo leva cerca de 5 minutos para ser instalado. Quando a instalação estiver concluída, um botão **Stratos Console** aparecerá no lugar do botão _ Instalar o Stratos Console_ na página de visão geral. O botão _Stratos Console_ ativa o console e está disponível para todos os usuários com acesso à instância do CFEE. As designações de associação de organização e de espaço podem limitar o que um usuário pode ver e gerenciar no Stratos Console.

Para iniciar o console Stratos:

1. Abra a instância do CFEE na qual o Stratos Console foi instalado.
2. Clique em **Stratos Console** na página de visão geral.
3. O Stratos Console é aberto em uma guia do navegador separada. Quando você abre o console pela primeira vez, é solicitado que aceite dois avisos consecutivos por causa de certificados autoassinados.
4. Clique em  ** Login **  para abrir o console. Nenhuma credencial é necessária, uma vez que o aplicativo usa suas credenciais do {{site.data.keyword.Bluemix_notm}}.


## Recursos adicionais
{: #additional-resources}

É possível executar algumas tarefas de administração em um CFEE usando os comandos da CLI `ibmcloud CFEE`. Os comandos permitem obter as informações sobre uma instância do CFEE, bem como gerenciar suas organizações e espaços. Consulte [Referência de comando do CFEE da CLI do IBM Cloud](https://console.cloud.ibm.com/docs/cli/reference/ibmcloud/cli_cfee.html#ibmcloud_commands_cfee){: new_window}
![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo").

É possível localizar vídeos com discussões e demonstrações aprofundadas sobre vários tópicos do CFEE na [Lista de execução de vídeos do CFEE](https://ibm.biz/CFEE-Playlist){: new_window} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo").

Informações sobre a API do CFEE estão na [documentação da API](https://cloud.ibm.com/apidocs/cfaas){: new_window} do CFEE ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo").
