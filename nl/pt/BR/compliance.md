---

copyright:
  years: 2018
lastupdated: "2018-10-19"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}


# Conformidade e regulamentação
{: #compliance}

O {{site.data.keyword.cfee_full}} (CFEE) é uma plataforma como serviço. Como tal, o cliente é livre para
usar a instância de serviço para qualquer coisa que ela seja capaz de suportar. O CFEE e os serviços dependentes têm
acesso à menor quantidade de dados pessoais possível.

Deve ficar claro, no entanto, que mesmo que o plano de controle do CFEE (via IU/API/CLI) não vá processar dados
sensíveis (por exemplo, dados de HIPAA), é responsabilidade do cliente assegurar o uso responsável do CFEE, já que todas as dependências são gerenciadas e de propriedade dos clientes na conta
do {{site.data.keyword.Bluemix_notm}}. 

Recomendamos as boas práticas a seguir:
*  Não modificar os serviços dependentes criados com um CFEE (Kubernetes, Cloud Object Storage e Compose for PostgreSQL).
*  Atualizar e gerenciar o CFEE por meio do próprio serviço do CFEE (interface com o usuário ou interface da
linha de comandos), em vez de por meio do serviço do Kubernetes.

O cluster do Kubernetes é usado para manter a maioria da infraestrutura do CFEE, bem como todos os aplicativos em
execução no CFEE, uma vez que as células do Cloud Foundry são implementadas na parte superior dos nós do Kubernetes. Esse
cluster pertence e é gerenciado pela conta SoftLayer do cliente.

O banco de dados Compose for PostgreSQL é usado pelo CFEE para manter os metadados sobre as organizações,
os espaços, os usuários e as funções. Se a instância do CFEE for usada como recomendado, não haverá dados sensíveis expostos. No entanto, se um cliente decidir nomear as organizações e os espaços com informações pessoais ou sensíveis sobre os
clientes, o banco de dados do PostgreSQL poderá conter informações do HIPAA ou outro tipo de informações sensíveis.

A instância do Cloud Object Storage é usada pelo CFEE para manter os droplets de um aplicativo, de modo que eles
possam ser implementados, interrompidos, iniciados, etc. Isso significa que a instância do Cloud Object Storage não está
executando o aplicativo, apenas mantendo a sua imagem. Portanto, se a instância do Cloud Object Storage for
usada seguindo as melhores práticas, ela não reterá nenhuma informação sensível do HIPAA. O cliente tem a
responsabilidade de assegurar que nenhum dado pessoal seja codificado permanentemente em nenhum de seus
aplicativos (dados de teste, etc.).
