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

# Criando um ambiente
{: #create-environment}

## Pré-requisito
* Assegure-se de que você esteja na conta do {{site.data.keyword.Bluemix_notm}} na qual deseja criar o ambiente.
* Assegure-se de que você tenha as [permissões](https://cloud.ibm.com/catalog/docs/cloud-foundry/permissions.html) corretas antes de criar instâncias do {{site.data.keyword.cfee_full_notm}}. 
* [Prepare a sua conta do IBM Cloud](https://cloud.ibm.com/docs/cloud-foundry/prepare-account.html) para assegurar que ela possa criar os recursos de infraestrutura necessários para uma instância do CFEE (as instâncias do CFEE são implementadas nos nós do trabalhador do Kubernetes por meio do Kubernetes Service).  

## Criando uma instância do CFEE
1.  Abra o [catálogo](https://cloud.ibm.com/catalog) do {{site.data.keyword.Bluemix_notm}}.

2.  Localize o serviço {{site.data.keyword.cfee_full_notm}} no catálogo e clique nele para abrir a página de visão geral para o serviço.  Essa primeira página fornece uma visão geral dos principais recursos do serviço. Clique em **Continue**.

3.  Configure a instância do CFEE a ser criada:
    * Selecione um plano. Consulte a seção [Visualização técnica do Eirini](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-create-environment#create-environment#eirini) para obter uma descrição das limitações desse plano.
    * Insira um **Nome** para a instância do CFEE.
    * Selecione um **Grupo de recursos** sob o qual o ambiente está agrupado. Somente os grupos de recursos aos quais você tem acesso na conta do IBM Cloud atual serão listados no menu suspenso _Grupos de recursos_, o que significa que você precisa ter permissão para acessar pelo menos um grupo de recursos na conta para poder criar um CFEE.
    * Selecione a **Geografia** e **Localização** em que a instância de serviço deve
ser fornecida. Veja lista de [locais de provisionamento e os data centers disponíveis](https://cloud.ibm.com/catalog/docs/cloud-foundry/index.html#provisioning-targets){: new_window} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo") por geografia para o CFEE e serviços de apoio. 

4. As instâncias do CFEE são provisionadas em um cluster Kubernetes. As células do Cloud Foundry são provisionadas dentro de zonas do trabalhador no cluster Kubernetes. É possível configurar o local, o hardware e a criptografia do cluster:
    * Selecione o isolamento de hardware para o cluster Kubernetes:   
      * _Virtual-compartilhado_: os recursos de infraestrutura no cluster, como o hypervisor e o hardware físico, são distribuídos entre você e outros clientes IBM, mas cada nó do trabalhador é um único locatário para você.
      * _Virtual-dedicado_: os nós do trabalhador no cluster são hospedados na infraestrutura que é dedicada à sua conta.
    * Os dados no cluster são criptografados por padrão. Você tem a opção de desligar _Criptografar o disco local_.
    * Selecione a **Geografia** e a **Região** na qual o cluster Kubernetes será provisionado.
    * Selecione as **Zonas** em que os nós do trabalhador do Kubernetes serão implementados. Você tem a opção de provisionar os nós do trabalhador na mesma zona (**Zona única**) ou em múltiplas zonas (**Múltiplas zonas**).  **Observe** que a criação de um CFEE de múltiplas zonas requer [Ampliação de VLAN](https://cloud.ibm.com/docs/containers?topic=containers-subnets#vlan-spanning), que também será suportada quando a conta do {{site.data.keyword.Bluemix_notm}} for [ativada por VRF](https://cloud.ibm.com/docs/infrastructure/direct-link/vrf-on-ibm-cloud.html#overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud).
    
    As VLANs disponíveis são recuperadas automaticamente para as zonas selecionadas. Se nenhuma VLAN estiver disponível, elas serão criadas automaticamente.
    
    **Nota: fornecimento de uma rede isolada:** é possível destinar VLANs em uma rede isolada. Quando a instância do CFEE for criada em uma rede isolada, as políticas na rede isolada (por exemplo, políticas do calico ou regras do VRA) deverão permitir que TODO o acesso de saída da instância do CFEE para o CFEE seja provisionado com sucesso. Assim que o CFEE for criado, as restrições de acesso de saída poderão ser restabelecidas, exceto para o acesso de saída a determinados serviços e microsserviços no IBM Cloud. Consulte a documentação [Operando em uma rede isolada](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-isolated-network#isolated-network) para obter mais informações.
    
    Assim que o CFEE for criado, o cluster Kubernetes no qual o ambiente é provisionado aparecerá (como qualquer outro recurso em sua conta do IBM Cloud) no [painel do ](https://https://cloud.ibm.com/catalog/dashboard/apps/){{site.data.keyword.Bluemix_notm}}. Para obter mais informações, consulte [Documentação do Kubernetes Service](https://https://cloud.ibm.com/catalog/docs/containers/cs_why.html#cs_ov).

5.  Configure a capacidade do CFEE:
    * Selecione o **Número de células** para o CFEE. Estas são as células do aplicativo que hospedarão os aplicativos implementados no CFEE.  
    * Selecione o **Tamanho do nó**, que determina a capacidade das células do Cloud Foundry (CPU e memória).
    
    Além das células do aplicativo que você especifica acima, _Células do Plano de controle_ adicionais são criadas e reservadas para a operação e o controle da plataforma do Cloud Foundry em seu CFEE. 

    **Nota:** recomendamos que o VLAN Spanning seja ativado se os nós do trabalhador no cluster do Kubernetes forem provisionados em sub-redes diferentes.  Os nós do trabalhador em sub-redes diferentes poderão evitar a conectividade entre eles se o VLAN Spanning estiver desativado.  Veja a documentação do [VLAN Spanning](https://cloud.ibm.com/catalog/docs/containers/cs_subnets.html#vlan-spanning) para obter mais informações.

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

## O plano de visualização técnica do Eirini
{: #eirini}

 O plano de Visualização técnica do Eirini permite que você explore um CFEE usando o Kubernetes nativo como o planejador de contêiner (em vez de Diego). O planejador do Kubernetes é usado no CFEE para implementar e executar apps no tempo de execução do aplicativo do Cloud Foundry, incluir usuários, criar uma organização e espaços, implementar apps e ligar esses apps aos serviços.Consulte a documentação do [projeto Eirini](https://www.cloudfoundry.org/project-eirini/)para obter informações adicionais sobre o projeto incubador Eirini a partir do Cloud Foundry Foundation.
 As limitações a seguir se aplicam às instâncias do CFEE criadas por meio do plano de Visualização técnica do Eirini:
 
* Kubernetes com `containerd`não é suportado. Somente versões do Kubernetes são suportadas que usam o Docker em vez de `containerd`. A versão mais recente do IBM Container Service (IKS) que suporta o Docker é a v1.10.
* O Cloud Foundry SSH não é suportado.
* `cf push` de imagens do Docker não é suportado.
* A preparação nativa do Eirini do Kubernetes não é suportada. As instâncias do CFEE criadas por meio do plano de visualização técnica do Eirini usam o Eirini para executar apps, mas não para prepará-los. As células do Diego ainda são usadas para preparar apps.
* A reinicialização de instâncias de app específicas (`cf restart-app-instance`) não é suportada.

 
