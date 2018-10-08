---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-07-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Sobre o {{site.data.keyword.cfee_full_notm}}
{: #about}

Com o {{site.data.keyword.cfee_full}} (CFEE), é possível instanciar plataformas Cloud Foundry múltiplas, isoladas e de classificação corporativa sob demanda. As instâncias do serviço {{site.data.keyword.Bluemix_notm}} Foundry Enterprise são executadas dentro de sua própria conta no {{site.data.keyword.Bluemix_notm}}. O ambiente é implementado em hardware isolado (clusters do Kubernetes). Você tem controle total sobre o ambiente, incluindo controle de acesso, gerenciamento da capacidade, gerenciamento de mudanças, monitoramento e serviços.
{:shortdesc}

O {{site.data.keyword.cfee_full}} está atualmente em sua fase beta e nós estamos em busca de feedback! Para começar, crie sua própria instância do {{site.data.keyword.cfee_full}} em [https://console.bluemix.net/cfadmin/create](https://console.bluemix.net/cfadmin/create) e [solicite acesso](http://ibm.biz/cfee-forum-signup) ao [Fórum de Slack do IBM CFEE](https://ibm-cfee.slack.com) para compartilhar seu feedback, fazer perguntas e se envolver com a equipe do produto.
{:tip}

Para um projeto bem-sucedido, reserve um tempo para planejar e projetar quais recursos você precisa e quais são seus requisitos corporativos. Para ajudá-lo a começar, considere as perguntas a seguir:

* Quantos e que tipo de apps você está desenvolvendo?
* Que serviços os apps precisam acessar?
* Quem colabora no processo de desenvolvimento e que função essa pessoa executa?
* Qual grau de isolamento é necessário para cada fase do projeto?
* A sua empresa fornece os recursos de infraestrutura?
* Como a sua empresa se comunica?
* Existe um padrão de nomenclatura que é possível implementar para identificar claramente a organização e o uso de espaço?

Como parte da decisão de qual tipo de ambiente de nuvem você precisa, planeje a estrutura de sua conta, organizações, espaços, recursos e membros da equipe.

Uma única conta do {{site.data.keyword.Bluemix_notm}} é suficiente para a maioria das organizações. Se a sua organização tiver mais de uma área de negócios, será possível criar uma conta do {{site.data.keyword.Bluemix_notm}} separada para cada domínio de negócios, por exemplo, uma grande corporação bancária pode criar contas separadas para os setores varejista e comercial.

A tabela a seguir fornece um resumo de alguns dos elementos chave.

| Elemento   | Descrição |
|-----------|---------------|
| Conta do IBM Cloud | As instâncias do CFEE são criadas sob uma conta específica do IBM Cloud, tornando-as disponíveis para os usuários nessa conta de acordo com as funções e políticas de acesso definidas para esses usuários. |
|| A conta sob a qual as instâncias do CFEE são criadas deve ser Pré-paga ou um tipo de conta de Assinatura (não uma conta para Teste).  |
| CFEE | Serviço IBM Cloud Foundry Enterprise Environment para hospedar aplicativos. |
|| Está disponível no catálogo do IBM Cloud. |
| Instância do CFEE | Uma instância do serviço IBM Cloud Foundry Enterprise Environment criada sob uma conta do IBM Cloud por um usuário em com uma função de administrador ou editor nessa conta. |
|| Pode haver múltiplas instâncias do CFEE em uma Conta do IBM Cloud. |
|| Pode ter uma ou mais organizações. |
| Organização | Inclui um ou mais espaços. |
|| Inclui um ou mais gerenciadores de org. |
|| Inclui um ou mais membros da equipe. Uma ou mais funções podem ser concedidas a cada membro da equipe. |
|| Os encargos de uso, que são gerados por um aplicativo implementado em um espaço, são relatados no nível de organização. |
| Espaço | Inclui um ou mais recursos. |
|| Inclui um ou mais apps. |
|| Inclui um ou mais gerenciadores de espaço. |
|| Inclui um ou mais membros da equipe. Cada usuário já deve ser um membro da equipe na organização proprietária. Uma ou mais funções podem ser concedidas a cada membro da equipe. |
| Membro da equipe | Pode ser incluído em uma ou mais organizações e espaços entre contas diferentes. |
|| Pode ter mais de uma função dentro da mesma organização, espaço ou ambos. |
| Alias de serviço | Um alias de uma instância de serviço no IBM Cloud. |
|| Permite que os desenvolvedores liguem instâncias de serviço existentes disponíveis em sua conta do IBM Cloud a seus aplicativos implementados em um espaço dentro de um CFEE.|
{:caption="Tabela 1. Descrição dos elementos-chave" caption-side="top"}

## Destinos de provisionamento para CFEE e serviços de apoio
{: #provisioning-targets}

A seguir estão as geografias, os locais e os data centers nos quais o serviço CFEE e os serviços dependentes (serviço Kubernetes, os serviços Compose for PostgreSQL e Cloud Object Storage) estão disponíveis para provisionamento:

|  ** Geografia **  &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;| **Instância do CFEE e cluster do Kubernetes** | **Cloud Object Storage** | **Compose for PostgreSQL (Região CF)** |
|----------------------------------------|-------------------|-------------------|-------------------|
|América do Norte | Montreal (mon01) | us-geo | us-east |
|América do Norte | Toronto (tor01) | us-geo| us-east |
|América do Norte | Washington DC (wdc04) | us-geo | us-east |
|América do Norte | Washington DC (wdc06) | us-geo | us-east | 
|América do Norte | Washington DC (wdc07) | us-geo | us-east |
|América do Norte | Dallas (das10) | us-geo | us-south |
|América do Norte | Dallas (das12) | us-geo | us-south |
|América do Norte | Dallas (das13) | us-geo |us-south |
|América do Norte | San Jose (sjc03) | us-geo | us-south |
|América do Norte | San Jose (sjc04) | us-geo | us-south |
|América do Sul &nbsp; &nbsp;| São Paulo (sao01) |  us-geo | us-south |
|Europa | Londres (lon02) | eu-geo | eu-gb |
|Europa | Londres (lon04) | eu-geo | eu-gb |
|Europa | Londres (lon06) | eu-geo | eu-gb | 
|Europa | Amsterdã (ams03) | eu-geo | eu-de |
|Europa | Oslo (osl01) |eu-geo | eu-de | 
|Europa | Paris (par01) | eu-geo | eu-de |
|Europa | Frankfurt (fra02) | eu-geo | eu-de |
|Europa | Frankfurt (fra04) | eu-geo | eu-de | 
|Europa | Frankfurt (fra05) |  eu-geo | eu-de |
|Ásia Pacífico | Melbourne (mel01) | ap-geo | au-syd |
|Ásia Pacífico | Sydney (syd01) | ap-geo | au-syd |
|Ásia Pacífico | Sydney (syd04) | ap-geo | au-syd | 
|Ásia Pacífico | Hong Kong (hkg02) | ap-geo | au-syd |
|Ásia Pacífico | Hong Kong (seo01) | ap-geo | au-syd |
|Ásia Pacífico | Cingapura (sng01) | ap-geo | au-syd |
|Ásia Pacífico | Tóquio (gok02) | ap-geo | au-syd |
|Ásia Pacífico | Tóquio (gok04) | ap-geo | au-syd |
|Ásia Pacífico | Tóquio (gok05) | ap-geo | au-syd |

{: caption="Tabela 2. Destinos de provisionamento para CFEE e serviços de apoio" caption-side="top"}



Por **exemplo**, o serviço CFEE pode ser provisionado em três data centers na Europa: Amsterdã (um data center), Frankfurt (três data centers), Londres (três data centers), Oslo (um data center) e Paris (um data center). Se o CFEE for provisionado em Frankfurt, a instância de serviço do Cloud Object Store será implementada na região _eu-geo_ e a instância de serviço do Compose for PostgreSQL será implementada na região pública do Cloud Foundry _eu-de_.

