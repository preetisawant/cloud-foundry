---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-04-01"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# O que há de novo no IBM Cloud Foundry Enterprise Environment

Este documento descreve o que há de novo em cada versão liberada até o momento do serviço do {{site.data.keyword.cfee_full_notm}}.

## Versão 2.2.0
{: #v220}

_Data de liberação:_ 04/01/2019

O CFEE v2.2.0 inclui as versões a seguir de seus componentes constituintes:
* Cloud Foundry: v2.7.1.15.5
* API do Cloud Foundry: v2.115.0
* Buildpacks do CFEE: v0.1.5
* Serviço do IBM Kubernetes: nenhuma atualização de versão fornecida. **Importante:** recomendamos que você atualize o cluster Kubernetes do CFEE para a v1.13 antes de atualizar para o CFEE v2.2.0 (necessário quando a instância do CFEE operar em uma rede isolada).

As mudanças a seguir foram liberadas na versão 2.2.0 do serviço do {{site.data.keyword.cfee_full_notm}} (CFEE). Para atualizar a versão do seu CFEE, acesse a página **Atualizações e ajuste de escala** na interface com o usuário do CFEE e clique em **Atualizar**:

* Nova opção para **criar** uma instância do CFEE em um cluster Kubernetes **de múltiplas zonas**. As instâncias do CFEE criadas em um cluster de múltiplas zonas distribuem instâncias do aplicativo, não apenas entre os nós do trabalhador dentro de um data center, mas também ao longo de data centers, tornando os seus aplicativos mais resilientes com relação a indisponibilidades de infraestrutura. Além disso, os CFEEs de múltiplas zonas podem ser **escalados** incluindo células adicionais ou removendo as existentes das zonas atuais. Observe que não é possível incluir ou remover zonas de um CFEE de várias zonas uma vez que a instância CFEE é criada.
* As instâncias do CFEE v2.2.0 podem agora [operar dentro de uma **rede isolada**](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-isolated-network#isolated-network). Observe que se a instância do CFEE for implementada em VLANs por meio de uma rede isolada, alguns terminais (endereços IP) [deverão ser identificados e roteados adequadamente](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-isolated-network#oppening-access-points) para que a instância do CFEE se torne operacional. Uma instância do CFEE requer um cluster Kubernetes v1.13 para operar em uma rede isolada.
* Novo recurso para ligar aplicativos (implementados em um espaço do CFEE) em instâncias de serviço por meio da rede interna da IBM. O recurso permite que os serviços que suportam o IBM Cloud Service Endpoint sejam consumidos sem acessar a Internet pública.
* Ferramentas de **monitoramento**:
    * As ferramentas de monitoramento (Prometheus, Grafana e Alertmanager) não serão mais provisionadas por padrão quando você criar um CFEE.  No CFEE v2.2.0, as ferramentas de monitoramento são fornecidas apenas quando explicitamente ativadas pelos administradores do CFEE.  Além disso, quando ativadas, as ferramentas de monitoramento não serão mais provisionadas nos nós do trabalhador do plano de controle do CFEE. Elas serão provisionadas em seus próprios nós do trabalhador, fora do plano de controle. Para ativar e fornecer ferramentas de monitoramento, acesse a página _Monitoramento_ do CFEE (na área de janela de navegação esquerda) e clique em **Ativar monitoramento**. 
    * Quando você atualizar um CFEE existente para a versão 2.2.0, as ferramentas de monitoramento existentes serão excluídas do plano de controle. Qualquer configuração customizada existente das ferramentas de monitoramento será perdida. 
    *  Novo recurso para substituir a [Configuração do Alertmanager](https://prometheus.io/docs/alerting/configuration/) padrão por uma configuração customizada que permite customizar a manipulação, o agrupamento e o roteamento de notificação de alertas. Na página _Monitoramento_ você poderá _Fazer download_ do arquivo de configuração padrão e _Fazer upload_ de um arquivo de configuração por meio de seu sistema de arquivos local. Consulte para obter um [exemplo](https://github.com/prometheus/alertmanager/blob/master/doc/examples/simple.yml) de um arquivo de configuração.
* Novo recurso para identificar instâncias CFEE na {{site.data.keyword.Bluemix_notm}}[_Lista de Recursos_](https://cloud.ibm.com/resources)e na interface com o usuário do CFEE.
* Melhorias gerais para a experiência do usuário do {{site.data.keyword.Bluemix_notm}} [**painel do Cloud Foundry**](https://cloud.ibm.com/dashboard/cloudfoundry/overview). O _painel do Cloud Foundry_ mostra visualizações globais de instâncias do CFEE, aplicativos e serviços públicos com alias nos espaços do CFEE. 

**Nota:** um novo plano **de Visualização técnica do Eirini** está disponível ao criar uma nova instância do CFEE. O plano é independente da v2.2.0 descrita acima, que se aplica somente ao plano _Padrão_. O plano de Visualização técnica do Eirini permite que você explore um CFEE usando o Kubernetes nativo como o planejador de contêiner (em vez de Diego). Consulte [Introdução à Visualização técnica do Eirini](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-getting-started-eirini#getting-started-eirini) para obter mais informações.

Veja uma demonstração do que há de novo no CFEE v2.1.0 neste [breve vídeo](https://ibm.biz/CFEE-V220){: new_window} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo").


## Versão 2.1.1
{: #v211}

_Data de liberação:_ 20/03/2019

As mudanças a seguir foram liberadas na versão 2.1.1 do serviço do {{site.data.keyword.cfee_full_notm}} (CFEE). Para
atualizar a versão do CFEE, acesse a página _Atualizações e ajuste de escala_ na interface com o
usuário do CFEE:

* Problemas resolvidos que impedem o fornecimento bem-sucedido. 


## Versão 2.1.0
{: #v210}

_Data de liberação:_ 20/02/2019

**Nota:** é possível atualizar somente para esta versão da versão **2.0.2**. Atualize para a versão 2.0.2 antes de atualizar para a versão v2.1.0.

As mudanças a seguir foram liberadas na versão 2.1.0 do serviço do {{site.data.keyword.cfee_full_notm}} (CFEE). Para atualizar a versão do seu CFEE, acesse a página **Atualizações e ajuste de escala** na interface com o usuário do CFEE e clique em **Atualizar**:

* Novo recurso de auto-scaling que escalará automaticamente instâncias do aplicativo do Cloud Foundry com base em regras customizadas. O auto-scaling é acessível por meio da CLI e por meio do console do Stratos. O console do Stratos pode ser instalado opcionalmente e ativado por meio da página _Visão geral_ na interface com o usuário do CFEE. Na página _Aplicativos_ do console do Stratos, selecione um aplicativo e procure a guia **Auto-Scaling**. Clique em *Criar política* para ativar o editor de auto-scaling para definir a política de ajuste de escala para o aplicativo de destino.
  Consulte a [documentação de auto-caling](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-autoscale_cloud_foundry_apps#autoscale_cloud_foundry_apps)para obter informações adicionais.
* Novo recurso para gerenciar buildapcks por meio da interface com o usuário do CFEE, incluindo o posicionamento de arrastar e soltar de um buildpack na lista de prioridades. O recurso está disponível na nova página **Buildpacks**da interface com o usuário do CFEE (não no console Stratos). Na liberação, apenas os arquivos zip do buildpack de 1 MB em tamanho (ou menores) podem ser incluídos ou atualizados por meio da interface com o usuário. É possível fazer upload de arquivos zip do buildpack maiores que 1 MB usando os comandos `cf create-buildpack` e `cf update-buildpack`. 
* Novo recurso para gerenciar cotas da organização por meio da interface com o usuário, incluindo a visualização de quais organizações estão usando uma cota específica. O recurso está disponível na nova página **Cotas** da interface com o usuário do CFEE (não no console do Stratos). É possível criar novas cotas e editar as existentes. Também é possível atualizar os valores da cota padrão com os valores de qualquer cota existente, chamando a **Cópia para padrão** no menu da cota.
* Uma nova página **Introdução** na interface com o usuário orienta os usuários para as tarefas mais importantes para configurar e usar o ambiente.
* **Tags** podem ser incluídas em uma instância do CFEE na lista de recursos do IBM Cloud. Tags incluídas na lista de recursos também aparecerão no cabeçalho da página de visão geral do CFEE.
* **Cloud Foundry** versão 2.7.21.
* Console do **Stratos** versão 2.3.0, que inclui uma correção de segurança. Observe que simplesmente atualizar a versão do CFEE não atualizará a versão do console do Stratos. É necessário excluir e reinstalar o console do Stratos (na página de Visão geral do CFEE), que seleciona automaticamente a versão do console do Stratos mais recente.
* Os usuários podem navegar para a página **cluster** Kubernetes do CFEE por meio do menu overflow na página de visão geral do CFEE.

**Nota:**Se você atualizar para CFEE v2.1.0 a partir de uma versão v2.0.x, a atualização ocorrirá com uma única ação de _Atualização_que atualiza automaticamente ambos, o plano de controle e as células em sequência. Se você atualizar por meio de uma versão v1.x.x, a atualização exigirá duas ações _Atualizar_ separadas, uma para atualizar o plano de controle (primeiro) e uma para atualizar as células.

Veja uma demonstração do que há de novo no CFEE v2.1.0 neste [breve vídeo](https://ibm.biz/CFEE-V210){: new_window} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo").


## Versão 2.0.2
{: #v202}

_Data de Liberação:_2019-02-08

As mudanças a seguir foram liberadas na versão 2.0.2 do serviço do {{site.data.keyword.cfee_full_notm}} (CFEE). Para
atualizar a versão do CFEE, acesse a página _Atualizações e ajuste de escala_ na interface com o
usuário do CFEE:

* Problemas resolvidos que impedem atualizações de versão bem-sucedidas. Esta versão é um pré-requisito para atualizar para a versão **2.1.0**.


## Versão 2.0.1
{: #v201}

_Data de liberação:_ 10/01/2019

As mudanças a seguir foram liberadas na versão 2.0.1 do serviço {{site.data.keyword.cfee_full_notm}} (CFEE). Para
atualizar a versão do CFEE, acesse a página _Atualizações e ajuste de escala_ na interface com o
usuário do CFEE:

* Problema resolvido que impedia que domínios customizados funcionassem adequadamente.
* Problema resolvido da indisponibilidade das métricas da organização durante a recuperação de novas métricas.


## Versão 2.0.0
{: #v200}

_Data de liberação:_ 13/12/2018

As mudanças a seguir foram liberadas na versão 2.0.0 do serviço {{site.data.keyword.cfee_full_notm}} (CFEE). Para
atualizar a versão do CFEE, acesse a página _Atualizações e ajuste de escala_ na interface com o
usuário do CFEE:

* Resiliência de atualização de versão do CFEE melhorada.
* Melhorias para a disponibilidade operacional e a resiliência das instâncias do CFEE.
* Certificados do lado do cliente para acesso mais seguro aos aplicativos, permitindo que o servidor conceda acesso ao
aplicativo apenas a clientes certificados.
* Quando uma instância do CFEE é criada, o cluster Kubernetes de suporte e a instância de serviço do Cloud Object
Storage são agora criados no mesmo grupo de recursos que a instância de serviço do CFEE (em vez de no grupo de
recursos "Padrão").
* Correção de segurança.
* Aprimoramentos para a CLI `ibmcloud cfee`:
    * Novos comandos para criar uma instância de serviço do IBM Cloud por meio de um espaço do CFEE e incluí-la nesse espaço do
CFEE (`ibmcloud cfee service-create`, `ibmcloud cfee service-alias-create`).
    * Novos comandos para ajustar a escala de capacidade de um CFEE (`ibmcloud cfee scale-up`, `ibmcloud cfee scale-down`).
    * Melhorias no comando para gerenciar instâncias do CFEE (`ibmcloud cfee environments`).
    
      Atualize a CLI ibmcloud (`ibmcloud update`) para acessar esses aprimoramentos de comando e emita `ibmcloud cfee -help` para obter mais detalhes.
      
**Nota**: a atualização de uma instância do CFEE para a versão 2.0.0 requer apenas uma única ação de _atualização_ que atualiza ambos, o plano de controle e as células. Nenhuma
atualização separada é necessária para o plano de controle e as células do CFEE.


## Versão 1.1.2
{: #v112}

_Data de liberação:_ 07/12/2018

As mudanças a seguir foram liberadas na versão 1.1.2 do serviço {{site.data.keyword.cfee_full_notm}}:
* Novos data centers em Chennai (che01) e Milão (mil01) estão agora disponíveis para fornecimento das instâncias do CFEE.
* Correção de segurança.

## Versão 1.1.1
{: #v111}

_Data de liberação:_ 28/11/2018

As mudanças a seguir foram liberadas na versão 1.1.1 do serviço {{site.data.keyword.cfee_full_notm}}:
* Correção de segurança.
   
## Versão 1.1.0
{: #v110}

_Data de liberação:_16/11/2018

As mudanças a seguir foram liberadas na versão 1.1.0 do serviço do {{site.data.keyword.cfee_full_notm}}:

* Novos recursos:
   * As instâncias do CFEE podem ser fornecidas em nós do trabalhador do Kubernetes
[virtuais/dedicados](https://console.bluemix.net/docs/containers/cs_clusters.html#clusters#clusters_ui_standard)
hospedados na infraestrutura dedicada à sua conta do IBM Cloud.
   * Um novo data center em Tóquio (tok05) está disponível para o fornecimento de instâncias do CFEE.
   * [Atualizando](https://console.bluemix.net/docs/cloud-foundry/updating-scaling.html#update-scale#update) uma instância do CFEE para uma nova versão.
   * [Ajuste
de escala](https://console.bluemix.net/docs/cloud-foundry/updating-scaling.html#update-scale#scale) da capacidade de uma instância do CFEE incluindo ou excluindo células do Cloud Foundry.
   * Atividades de
[auditoria](https://console.bluemix.net/docs/cloud-foundry/auditing-logging.html#auditing-logging#auditing)
do Cloud Foundry por meio da integração com uma instância de serviço do IBM Cloud Activity Tracker automaticamente
configurada.
   * Persistência dos
[eventos de
log](https://console.bluemix.net/docs/cloud-foundry/auditing-logging.html#auditing-logging#logging) do Cloud Foundry por meio de uma instância de serviço do IBM Cloud Log Analysis automaticamente
configurada.
   * Visualização de verificação de funcionamento que indica o status operacional dos componentes do CFEE.
   * Novos comandos para executar ações relacionadas ao CFEE na interface da linha de comandos (CLI):
     * Os comandos `ibmcloud cfee create`, `ibmcloud cfee create-locations` e
`ibmcloud cfee create-status` para criar instâncias do CFEE por meio da interface da linha de
comandos, obter uma lista de data centers disponíveis em que um CFEE possa ser fornecido e verificar o
status de fornecimento de um CFEE sendo criado.
     * Os comandos `ibmcloud cfee create-permission-get` e `ibmcloud cfee
create-permission-set` [](https://console.bluemix.net/docs/cloud-foundry/permissions.html#permissions#permcli-creating)
para recuperar e configurar as permissões necessárias para criar instâncias do CFEE. Os comandos agregam e simplificam a configuração
das permissões para o serviço do CFEE e para os serviços de suporte necessários.
     * O comando `ibmcloud catalog blacklist` para simplificar o
[controle
de visibilidade](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#workingwith-services#service_visibility) dos serviços do IBM Cloud para usuários em uma conta do IBM Cloud.

* Problemas resolvidos:
   *  Problema resolvido: erro intermitente ao acessar as métricas de célula
<br/>   
Consulte uma demonstração do que há de novo no CFEE v1.1.0 neste [breve
vídeo](https://ibm.biz/CFEE-V110){: new_window} ![Ícone
de link externo](../icons/launch-glyph.svg "Ícone de link externo").  Também é possível localizar outros vídeos sobre vários tópicos do CFEE na
[lista de execução de vídeos do CFEE](https://ibm.biz/CFEE-Playlist){: new_window}
![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo").
