---



copyright:

  years: 2018

lastupdated: "2018-11-09"



---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:tip: .tip}

# FAQ
{: #cfeefaq}

## Qual é a diferença entre o IBM Cloud Foundry Enterprise Environment (CFEE) e o Cloud Foundry público?
{: #cfee_diff}

É possível usar o {{site.data.keyword.cloud}} Foundry público para executar aplicativos nativos da
nuvem que estão usando o Cloud Foundry para configuração simples, ajuste de escala poderoso e gerenciamento de tráfego. 
Você também tem acesso fácil a todos os serviços do {{site.data.keyword.cloud}}.

É possível usar o {{site.data.keyword.cfee_full}} para tudo como você faria com o Cloud Foundry público,
mas também para criar e gerenciar ambientes isolados para hospedar os aplicativos do Cloud Foundry exclusivamente para a
sua empresa.


## Qual a diferença da nova oferta em relação às ofertas do IBM Cloud Foundry anteriores?
{: #cfOfferings_diff}

No que diz respeito aos diversos locatários públicos, a diferença mais notável certamente são as
propriedades de isolamento. Com relação à oferta de único locatário existente na infraestrutura do IBM Cloud,
as duas principais diferenças são a área de cobertura da infraestrutura reduzida (e, portanto, o custo) e o
modelo de integração de serviço em tal ambiente de único locatário.

## Onde posso localizar o serviço do CFEE?
{: #where}

É possível localizar e instanciar o serviço do {{site.data.keyword.cfee_full}} no
{{site.data.keyword.Bluemix_notm}} catálogo do
[](https://console.stage1.bluemix.net/catalog).

## Posso ter mais de um ambiente do CFEE dentro de um data center regional?
{: #multiple-cfees}

Sim, é possível criar quantas instâncias do CFEE on demand você desejar
[nessas
regiões](https://dev.console.test.cloud.ibm.com/docs/cloud-foundry/index.html#provisioning-targets){: new_window} ![Ícone
de link externo](../icons/launch-glyph.svg "Ícone de link externo").

## Terei que começar com alguma capacidade mínima?
{: #minimum-capacity}

Sim. A criação de uma instância do CFEE requer um mínimo de duas células do Cloud Foundry, cada uma delas com 4
núcleos de 16 GB de RAM, disco primário SSD de 25 GB, disco secundário SSD de 100 GB e velocidade de rede de 1000 Mbps.

## Qual é o IaaS subjacente no qual o CFEE é implementado?
{: #why-kubs}

O serviço do CFEE é executado em contêineres do Kubernetes, o que permite custos de infraestrutura mais baixos e
operações mais eficientes, uma vez que o Kubernetes é um IaaS muito inteligente que automatiza muitas atividades
operacionais. 

## Quais são as minhas opções de isolamento ao criar um CFEE?
{: #isolation}

Há duas opções de hardware no tipo de infraestrutura do Kubernetes na qual a instância do CFEE é implementada:
hardware _Virtual compartilhado_ ou _Virtual dedicado_. Com o hardware _Virtual compartilhado_, os nós do trabalhador (no qual o contêiner da plataforma Cloud Foundry é implementado) são
distribuídos entre você e outros clientes IBM. Com o _Virtual dedicado_, os nós do trabalhador são
hospedados no hardware que é dedicado exclusivamente à sua conta. Observe que, em ambos os casos (_Virtual compartilhado_ e _Virtual dedicado_, cada nó do trabalhador é um único locatário para o
cliente. Isso significa que as células do Cloud Foundry nas quais os aplicativos são executados não são compartilhadas
com outros clientes.

## Posso escalar a capacidade de um CFEE?
{: #scaling}

Sim, é possível aumentar ou diminuir a capacidade do CFEE conforme as suas necessidades mudam,
incluindo ou removendo as células do Cloud Foundry.

## Posso fazer upgrade do CFEE para uma nova versão? Como isso funciona?
{: #upgrading}
Sim. A interface com o usuário do CFEE o notifica quando há novas versões do CFEE. Você controla quando atualizar para uma
nova versão. A atualização de versão do CFEE é chamada pelos administradores do CFEE na interface com o usuário. As
atualizações de versão do CFEE podem empacotar novas versões de seus componentes ou serviços de suporte (por exemplo, Cloud
Foundry, Kubernetes, etc.). Atualize o plano de controle do CFEE primeiro e, em seguida, as células do Cloud Foundry. O
processo de atualização é otimizado para minimizar a interrupção.

## O que é necessário para criar uma instância do CFEE?
{: #create}

É possível localizar o serviço do CFEE listado no catálogo do {{site.data.keyword.Bluemix_notm}}. É
necessário ter uma conta do {{site.data.keyword.Bluemix_notm}} atualizada e as permissões para o
serviço do CFEE e seus serviços suportados (Kubernetes, Cloud Object Storage e Compose for PostgreSQL). Depois de ter
essas permissões, apenas forneça um nome para o ambiente e clique em _Criar_. A criação leva
aproximadamente 90 minutos.

## Posso usar os serviços do {{site.data.keyword.Bluemix_notm}} no CFEE?
{: #Services-ibmcloud}

Com certeza! Por serem integrados no {{site.data.keyword.Bluemix_notm}}, os desenvolvedores em um CFEE
podem criar instâncias de serviço do {{site.data.keyword.Bluemix_notm}} (ou usar instâncias existentes) e
ligá-las aos aplicativos implementados nos espaços do CFEE.

## Posso ter meus próprios serviços no CFEE?
{: #Services-ibmcloud}

Sim. Um administrador pode registrar um broker de serviço no CFEE e disponibilizar os planos de serviços
customizados para os usuários neste CFEE. O mercado local do MCFEE inclui os serviços do catálogo do
{{site.data.keyword.Bluemix_notm}} mais quaisquer atendimentos ao cliente gerenciados pelo broker de
serviço local do CFEE.

## Como controlar o acesso do usuário a um CFEE?
{: #Services}

Como qualquer outro serviço do {{site.data.keyword.Bluemix_notm}}, o acesso a um CFEE é controlado por meio
do _Identity & Access Management_ (IAM). A designação de políticas de acesso de usuário
(individualmente ou por meio de grupos de acesso) com funções específicas fornece a elas níveis específicos de acesso a um CFEE. 
Além do acesso ao serviço do CFEE, o acesso às organizações e espaços do Cloud Foundry no CFEE é controlado por meio da
associação e das funções do Cloud Foundry designadas aos usuários em organizações e espaços específicos.

