---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-12-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# O que há de novo no IBM Cloud Foundry Enterprise Environment

Este documento descreve o que há de novo em cada versão liberada até o momento do serviço do {{site.data.keyword.cfee_full_notm}}.


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
