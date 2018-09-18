---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-12"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Tutorial Introdução
{: #getting-started}

{{site.data.keyword.cfee_full}} é uma plataforma de nuvem para hospedar apps e serviços na nuvem. O {{site.data.keyword.cfee_full_notm}} torna mais fácil escalar apps conforme o consumo cresce, simplificando o tempo de execução, o middleware e a infraestrutura para que você possa se concentrar em desenvolver apps.
{: shortdesc}

Este tutorial de introdução mostra como criar um {{site.data.keyword.cfee_full_notm}}, incluir usuários, criar uma organização e espaços, implementar apps e ligar esses apps aos serviços.

## Entendendo Permissões
{: #permissions}

Para trabalhar com instâncias do {{site.data.keyword.cfee_full_notm}}, os usuários do serviço devem ter as permissões corretas. Para obter mais informações, consulte  [ Permissões ](/docs/cloud-foundry/permissions.html).

## Etapa 1: assegurando-se de que a conta do {{site.data.keyword.Bluemix_notm}} possa criar recursos de infraestrutura
{: #accountprep-environment}

As instâncias do CFEE são implementadas em recursos de infraestrutura, que são nós do trabalhador do Kubernetes do serviço IBM Container. [Prepare sua conta do IBM Cloud](/docs/cloud-foundry/prepare-account.html) para assegurar que ela possa criar os recursos de infraestrutura necessários para uma instância do CFEE.

## Etapa 2: criando a sua instância do CFEE
{: #creating-environment}

Antes de criar seu CFEE, certifique-se de estar na conta do {{site.data.keyword.Bluemix_notm}} IBM Cloud em que você deseja criar o ambiente e de ter as políticas de acesso necessárias (conforme a etapa 1 acima).

1. Abra o  {{site.data.keyword.Bluemix_notm}}  [ catálogo ](https://console.bluemix.net/catalog).
2. Localize o serviço {{site.data.keyword.cfee_full_notm}} no catálogo e clique nele para abrir a página de visão geral para o serviço.
3. A primeira página da página de criação fornece uma visão geral dos recursos principais do serviço. Clique em **Continue**.
4. Configure a instância a ser criada, fornecendo o seguinte:
    * Selecione um plano (a disponibilidade do plano pode ser restrita durante o Beta).
    * Insira um **Nome** para a instância de serviço.
    * Selecione um **Local** no qual a instância de serviço deve ser provisionada.
    * Selecione o **Número de células** para o ambiente do Cloud Foundry.
    * Selecione o **Tipo de máquina**, que determina o tamanho das células do Cloud Foundry (CPU e memória).
    * Selecione um **Grupo de recursos** sob o qual o ambiente está agrupado. Somente os grupos de recursos aos quais você tem acesso na conta do IBM Cloud atual serão listados no menu suspenso _Grupos de recursos_, o que significa que você precisa ter permissão para acessar pelo menos um grupo de recursos na conta para poder criar um CFEE.
5. Opcionalmente, abra a seção **Infraestrutura** para ver as propriedades do cluster Kubernetes que suporta a instância do CFEE. Observe que o **Número de nós do trabalhador** é igual ao número de células mais 2 (dois dos nós do trabalhador do Kubernetes provisionados suportam o plano de controle do CFEE).
6. O **Resumo da ordem** no lado direito da página reflete o custo da instância do CFEE e o total estimado.
7. Clique em **Criar**, que abre o painel do ambiente e indica o progresso da criação e o status.
8. Depois que o fornecimento tiver iniciado, o ambiente será mostrado no painel do {{site.data.keyword.Bluemix_notm}}, bem como no [painel Ambientes do Cloud Foundry](https://console.bluemix.net/dashboard/cloudfoundry?filter=cf_environments). O status indica quando o fornecimento é concluído.

O processo automatizado que cria o ambiente implementa a infraestrutura em um cluster do Kubernetes e a configura para torná-la pronta para uso. O processo leva de 90 a 120 minutos.

**Nota:** o cluster do Kubernetes no qual o ambiente é implementado aparece no [painel](https://console.bluemix.net/dashboard/apps/) do {{site.data.keyword.Bluemix_notm}}. Para obter mais informações, consulte [Documentação do {{site.data.keyword.Bluemix_notm}} Container Service](/docs/containers/cs_why.html#cs_ov).

## Etapa 3: Criando Organizações e Espaços

Depois de criar o {{site.data.keyword.cfee_full_notm}}, consulte [Criando organizações e espaços](/docs/cloud-foundry/orgs-spaces.html) para obter informações sobre como estruturar o ambiente criando organizações e espaços. Os apps em um {{site.data.keyword.cfee_full_notm}} têm o escopo definido em espaços específicos. Por sua vez, existe um espaço dentro de uma organização específica. Os membros de uma organização compartilham um plano de cota, apps, instâncias de serviços e domínios customizados.

**Nota:** a página _Organizações do Cloud Foundry_ disponível no menu **_Gerenciar > Conta > Organizações do Cloud Foundry_** localizado no cabeçalho superior do IBM Cloud é destinada exclusivamente para organizações públicas do IBM Cloud, **não para organizações do CFEE**. As organizações do CFEE são gerenciadas na página _Organizações_ de uma instância do CFEE. Abra a interface com o usuário do CFEE e clique na página **_Organizações_** para criar e gerenciar organizações para esse CFEE.

## Etapa 4: incluindo usuários em organizações e espaços

[Inclua usuários](/docs/cloud-foundry/add-users.html) nessas organizações e espaços sob designações de função específicas que controlam seu nível de acesso. Para que os usuários possam ser incluídos como membros de organizações e espaços em um CFEE, esses usuários devem ter acesso anterior à instância do CFEE. Consulte  [ Permissões ](/docs/cloud-foundry/permissions.html).

## Etapa 5: Implementando e visualizando aplicativos

Quando você estiver pronto, será possível [implementar o app](/docs/cloud-foundry/deploy-apps.html) com a interface da linha de comandos do {{site.data.keyword.Bluemix_notm}}. Visualize a lista de aplicativos implementados na interface com o usuário, seja no contexto de um espaço específico do CFEE ou globalmente em todas as instâncias do CFEE. Também é possível iniciar, parar ou excluir aplicativos dessas visualizações.

## Etapa 6: criando instâncias de serviço e aliases

Crie [aliases de serviço](/docs/cloud-foundry/add-serv-inst.html) de instâncias de serviço disponíveis na conta do IBM Cloud para alavancá-las em seus aplicativos CFEE.

## Etapa 7: ligando aplicativos a instâncias de serviço

[Ligue seu app](/docs/cloud-foundry/binding.html) a um alias da instância de serviço para usar as funções do serviço.

## Etapa 8: instalando o Stratos Console para gerenciar aplicativos (opcional)

O Stratos Console é uma ferramenta baseada na web de software livre para trabalhar com o Cloud Foundry. O aplicativo Stratos Console pode ser instalado opcionalmente e usado em um ambiente específico do CFEE para gerenciar suas organizações, espaços e aplicativos.

Os usuários com as funções de administrador ou editor do IBM Cloud na instância do CFEE podem instalar o aplicativo Stratos Console nessa instância do CFEE.

Para instalar o aplicativo Stratos Console:

1. Abra a instância do CFEE na qual você deseja instalar o Stratos Console.
2. Clique em **Instalar o Stratos Console** na página de visão geral. O botão fica visível somente para usuários com permissões de administrador ou de editor para essa instância do CFEE.
3. No diálogo Instalar o Stratos Console, selecione uma opção de instalação. É possível instalar o aplicativo Stratos Console no plano de controle do CFEE ou em uma das células. Selecione uma versão do Stratos Console e o número de instâncias do aplicativo a ser instalado. Se você instalar o aplicativo Stratos Console em uma célula, será solicitado que forneça a organização e o espaço no qual implementar o aplicativo.
4. Clique em **Instalar**.

O aplicativo leva cerca de 5 minutos para ser instalado. Quando a instalação estiver concluída, um botão **Stratos Console** aparecerá no lugar do botão _ Instalar o Stratos Console_ na página de visão geral. O botão _Stratos Console_ ativa o console e está disponível para todos os usuários com acesso à instância do CFEE. As designações de associação de organização e de espaço podem limitar o que um usuário pode ver e gerenciar no Stratos Console.

Para iniciar o console Stratos:

1. Abra a instância do CFEE na qual o Stratos Console foi instalado.
2. Clique em **Stratos Console** na página de visão geral.
3. O Stratos Console é aberto em uma guia do navegador separada. Quando você abre o console pela primeira vez, é solicitado que aceite dois avisos consecutivos por causa de certificados autoassinados.
4. Clique em  ** Login **  para abrir o console. Nenhuma credencial é necessária, uma vez que o aplicativo usa suas credenciais do {{site.data.keyword.Bluemix_notm}}.

O que é possível ver e gerenciar é limitado por sua associação de organizações e de espaço e funções.
