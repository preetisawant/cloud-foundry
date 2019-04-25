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

# Tutorial Introdução
{: #getting-started}

O {{site.data.keyword.cfee_full}} (CFEE) é uma plataforma em nuvem para hospedar aplicativos e serviços na nuvem. O {{site.data.keyword.cfee_full_notm}} torna mais fácil escalar apps conforme o consumo cresce, simplificando o tempo de execução, o middleware e a infraestrutura para que você possa se concentrar em desenvolver apps.
{: shortdesc}

Este tutorial de introdução mostra como criar um {{site.data.keyword.cfee_full_notm}}, incluir usuários, criar uma organização e espaços, implementar apps e ligar esses apps aos serviços.

**Nota:** as etapas a seguir são aplicáveis a CFEEs criados por meio do plano **Padrão**. Se esse CFEE foi criado por meio do plano de **Visualização técnica do Eirini**, siga **somente as etapas 1 a 6** e a etapa **11**. Os recursos descritos nas etapas 8 a 11 não são suportados no plano de _Visualização técnica do Eirini_. Consulte [Introdução à Visualização Técnica do Eirini](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-getting-started-eirini#getting-started-eirini).
O plano de _Visualização técnica do Eirini_ permite que você explore um CFEE usando o Kubernetes nativo como o planejador de contêiner (em vez de Diego). O planejador do Kubernetes é usado no CFEE para implementar e executar apps no tempo de execução do aplicativo do Cloud Foundry, incluir usuários, criar uma organização e espaços, implementar apps e ligar esses apps aos serviços. 

## Etapa 1: Criar a sua instância do CFEE
{: #create-environment}

É possível criar uma instância do {{site.data.keyword.cfee_full_notm}} (CFEE) por meio do catálogo do {{site.data.keyword.Bluemix_notm}}. Antes de criar a instância do CFEE, visite a documentação [Criar ambiente](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-create-environment#create-environment) para obter orientação sobre como preparar a sua conta do {{site.data.keyword.Bluemix_notm}}, assegurando as permissões corretas e as etapas para criar a instância do CFEE.


## Etapa 2: Criar as organizações e os espaços
{: #create-orgsandspaces}

Depois de criar o {{site.data.keyword.cfee_full_notm}}, consulte [Criando organizações e espaços](https://cloud.ibm.com/docs/cloud-foundry/orgs-spaces.html) para obter informações sobre como estruturar o ambiente criando organizações e espaços. Os apps em um {{site.data.keyword.cfee_full_notm}} têm o escopo definido em espaços específicos. Por sua vez, existe um espaço dentro de uma organização específica. Os membros de uma organização compartilham um plano de cota, apps, instâncias de serviços e domínios customizados.

Quando você criar uma organização, designará uma cota para ela. A cota define limites sobre os recursos (memória, cpu etc.) disponíveis para essa organização. É possível designar uma cota diferente em um momento posterior. Há um conjunto de cotas pré-configuradas disponíveis em cada CFEE, mas também é possível criar as suas próprias cotas customizadas na página **Cotas** da interface com o usuário do CFEE. É possível fazer uma cota customizada a cota _Padrão_ chamando a ação _Copiar para padrão_ no menu da cota, que copia os valores da cota customizada para a cota padrão.

**Nota:** a página _Organizações do Cloud Foundry_ disponível no menu **_Gerenciar > Conta > Organizações do Cloud Foundry_** localizado no cabeçalho superior do IBM Cloud é destinada exclusivamente para organizações públicas do IBM Cloud, **não para organizações do CFEE**. As organizações do CFEE são gerenciadas na página _Organizações_ de uma instância do CFEE.  Abra a interface com o usuário do CFEE e clique na página **_Organizações_** para criar e gerenciar organizações para esse CFEE.

## Etapa 3: Incluir usuários em organizações e espaços
{: #add-users}

[Inclua usuários](https://console.bluemix.net/docs/cloud-foundry/add-users.html) nessas organizações e espaços sob designações de função específicas que controlam seu nível de acesso.  Para que os usuários possam ser incluídos como membros de organizações e espaços em um CFEE, esses usuários devem ter acesso anterior à instância do CFEE. Consulte  [ Permissões ](https://console.bluemix.net/docs/cloud-foundry/permissions.html).

## Etapa 4: Implementar e visualizar aplicativos
{: #deploy-apps}

Quando você estiver pronto, será possível [implementar o app](https://cloud.ibm.com/docs/cloud-foundry/deploy-apps.html) com a interface da linha de comandos do {{site.data.keyword.Bluemix_notm}}.  Visualize a lista de aplicativos implementados na interface com o usuário, seja no contexto de um espaço específico do CFEE ou globalmente em todas as instâncias do CFEE.  Também é possível iniciar, parar ou excluir aplicativos dessas visualizações.

## Etapa 5: Criar ou incluir instâncias de serviço do IBM Cloud em espaços do CFEE
{: #service-instances}

[Criar serviços](https://cloud.ibm.com/docs/cloud-foundry/add-serv-inst.html#workingwith-services#creating-services-inspace) ou [Incluir serviços existentes](https://cloud.ibm.com/docs/cloud-foundry/add-serv-inst.html#workingwith-services#adding-services-inspace) disponíveis na conta do IBM Cloud.  Depois que uma instância de serviço estiver disponível em um espaço do CFEE, será possível ligá-lo aos aplicativos CFEE implementados nesse espaço.

## Etapa 6: Ligar aplicativos a instâncias de serviço
{: #bind-apps}

[Ligue seu app](https://cloud.ibm.com/docs/cloud-foundry/binding.html) a um alias da instância de serviço para usar as funções do serviço.

No [painel do Cloud Foundry](https://cloud.ibm.com/dashboard/cloudfoundry/overview){: new_window} ![Ícone delink externo](../icons/launch-glyph.svg "Ícone de link externo"), é possível ver uma visualização consolidada de todos os aplicativos e serviços, tanto

*públicos* quanto *corporativos*.  Uma vez no painel do Cloud Foundry, clique em *Públicos* na área de janela de navegação à esquerda para ver os aplicativos públicos e os serviços disponíveis na conta do IBM Cloud.  Clique
em *Corporativo* para ver todos os ambientes do CFEE, os aplicativos implementados nos espaços do
CFEE e os serviços disponíveis para os espaços do CFEE.
{:tip}

## Etapa 7: Ativar a auditoria e a persistência de criação de log (opcional)
{: #enable-auditingandlogging}

Ative o ambiente para os
[eventos de
auditoria](https://cloud.ibm.com/docs/cloud-foundry/auditing-logging.html#auditing-logging#auditing) e
[persistência de criação de log](https://cloud.ibm.com/docs/cloud-foundry/auditing-logging.html#logging).

## Etapa 8: Ativar ferramentas de monitoramento (opcional)
{: #enable-monitoring}

As ferramentas de monitoramento não são provisionadas automaticamente em instâncias do CFEE v2.2.0 ou mais recente. Os administradores do CFEE podem [ativar as ferramentas de monitoramento](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-monitoring) assim que a instância do CFEE for criada. O conjunto de ferramentas de monitoramento inclui o Prometheus, o Grafana e o Alertmanager.

## Etapa 9: Criar e proteger domínios do Cloud Foundry (opcional)
{: #create-domains}

Crie [domínios](https://cloud.ibm.com/docs/cloud-foundry/domains.html#domains) para todos os
aplicativos no CFEE (domínios compartilhados) ou para uma organização específica (domínios privados) e proteja-os com
os certificados SSL.

## Etapa 10: Configurar a ordem de priorização dos buildpacks do Cloud Foundry
{: #create-buildpacks}

Os buildpacks fornecem o suporte de tempo de execução para aplicativos implementados em um ambiente do Cloud Foundry, configurando automaticamente o tempo de execução para um aplicativo e manipulando as suas dependências.  O Cloud Foundry inclui um conjunto de buildpacks para linguagens e estruturas comuns. [Saiba mais](https://docs.cloudfoundry.org/buildpacks/) sobre buildpacks do Cloud Foundry.  

É possível criar e fazer upload de buildpacks customizados na página **Buildpacks** da interface com o usuário do CFEE. Os buildpacks têm uma posição ordinal na lista de prioridades. Durante a preparação de um aplicativo, o Cloud Foundry verifica a compatibilidade do aplicativo com relação ao conjunto de buildpacks, iniciando com o ranqueamento 1. As verificações de compatibilidade prosseguem pela lista de prioridades até que localizem um buildpack compatível. Assegure-se de que a sequência de prioridade do conjunto de buildpacks atenda às necessidades de suas equipes de desenvolvimento. É possível mudar o ranqueamento de um buildpack na sequência de prioridade arrastando e soltando o nome do buildpack em um ranqueamento diferente. Também é possível gerenciar buildpacks por meio do [CLI do Cloud Foundry](https://docs.cloudfoundry.org/adminguide/buildpacks.html).

## Etapa 11: Instale o Stratos Console para gerenciar aplicativos (opcional)
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
