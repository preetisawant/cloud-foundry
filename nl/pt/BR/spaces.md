---

copyright:

  years: 2018
lastupdated: "2018-04-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Determinar seus Espaços
{: #determinespaces}

Em uma organização, os espaços fornecem um nível extra de cumprimento de limite e abstração.

Um espaço é uma área reservada na organização em que os usuários podem desenvolver e executar apps e serviços. É possível criar qualquer número de espaços em uma organização e controlar os usuários que têm acesso a um espaço. Consulte [Espaços](/docs/account/orgs_spaces.html#orgsspacesusers) para obter mais detalhes.

Se você planejar definir muitos espaços, poderá desejar criar um aplicativo para ajudar a gerenciar os espaços. Quando o número de espaços exceder sessenta, você talvez desejará considerar definir outra organização.

## Espaços para organização única versus diversas organizações
{: #spaceconsiderations}

Ao adotar uma arquitetura de organização única, o nível de segregação e abstração é fornecido pelos espaços definidos dentro da organização. Considere a orientação a seguir ao definir espaços:

* Defina um espaço para hospedar um serviço que requer fornecimento e configuração somente uma vez na organização.
* Defina os espaços com base no ciclo de vida de entrega.
  Por exemplo, é possível definir um ou mais espaços para apps que estão sendo desenvolvidos, um ou mais espaços para apps que estão na fase de teste e um ou mais
  espaços para aplicativos que estão em produção.
* Se o limite do ciclo de vida de entrega não for suficiente, será possível alcançar mais segregação definindo um ou mais espaços por LOB e fase de entrega.
* Identifique se será necessário aplicar limites para diferentes grupos de usuários.
  Por exemplo, seus desenvolvedores não podem desenvolver o aplicativo e testá-lo. Você requer um conjunto diferente de usuários para testar o aplicativo. Neste cenário, você cria dois espaços, um para os
  desenvolvedores do aplicativo e um para os testadores do aplicativo. Em seguida, conceda a cada conjunto de usuários acesso ao espaço correto.

Ao implementar uma arquitetura de organização múltipla, é possível segregar cada organização pelo LOB, o ciclo de vida de entrega ou ambos. Em seguida, é possível definir múltiplos espaços, que são baseados no número de apps ou projetos que são entregues pelo mesmo departamento na empresa. Considere a orientação a seguir ao planejar os espaços em uma organização:

* Defina um espaço para hospedar um serviço que requer fornecimento e configuração somente uma vez na organização.
* Defina um espaço por aplicativo, por grupo de apps relacionados ou para um projeto específico.
* Se for necessário impingir limites para diferentes usuários, defina um espaço para cada conjunto de usuários. Quando uma função de desenvolvedor é concedida a um usuário em um espaço, esse usuário tem acesso total a quaisquer recursos (e serviços {{site.data.keyword.Bluemix_notm}}) que são provisionados e estão em execução nesse espaço. Quando você precisar impingir maior segurança para evitar que os usuários controlem todos os recursos, considere definir espaços diferentes. Dentro de qualquer um desses espaços, é possível provisionar serviços do {{site.data.keyword.Bluemix_notm}} que são usados pelos apps em execução nesse espaço.

## Nomenclatura de espaço, restrições e gerenciamento
{: #spaceadmin}

Para definir os diferentes espaços para sua organização em nuvem, considere a orientação a seguir:

* Definir e impingir uma convenção de nomenclatura. Por exemplo, defina uma convenção de nomenclatura na qual o nome do espaço inclua informações sobre onde a organização está localizada e o tipo de nuvem. É possível mudar o nome de um espaço após sua criação. Se um nome de espaço for alterado, notifique todos os membros da equipe do espaço sobre a mudança.
* Defina as restrições que se aplicam ao espaço. Por exemplo, defina o tipo de app que pode ser desenvolvido, gerenciado e implementado em cada espaço.
* Identifique o gerente do espaço. Você talvez deseje delegar a administração do espaço para mais de uma pessoa.
