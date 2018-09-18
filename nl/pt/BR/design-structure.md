---

copyright:

  years: 2018
lastupdated: "2018-04-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Projete a estrutura de seu ambiente do  {{site.data.keyword.Bluemix_notm}}
{: #bpimplementation}

Em vez da metodologia tradicional estritamente definida de desenvolvimento, teste e produção, é possível implementar um ambiente no qual os desenvolvedores e os testadores podem colaborar com outros membros da equipe. Se você projetar a maneira que deseja desenvolver e entregar seus apps, crie espaços do {{site.data.keyword.Bluemix}} para cumprir essa metodologia. Em vez de projetar seu ambiente do nível de organização para baixo, considere projetar seu ambiente {{site.data.keyword.Bluemix_notm}} do nível de espaço para cima.

Considere a escala e o escopo dos apps que você planeja desenvolver e implementar. Um espaço do {{site.data.keyword.Bluemix_notm}} pode ser usado como um ambiente de desenvolvimento para um ou mais apps que estão conectados ou definidos de forma mais rígida. Além de um espaço de desenvolvimento, por exemplo, é possível criar espaços para teste de unidade, teste de desempenho e teste de integração. Espaços também podem ser definidos para construção, preparação e produção. Cada um dos espaços criados pode ser compartilhado com diferentes membros da equipe dentro da mesma organização.

Crie organizações do Cloud Foundry separadas quando você tiver pessoas trabalhando em diferentes áreas de negócios e onde suas atividades não se sobreponham. Se houver dois grupos independentes, a criação de uma organização para cada um define limites claros para a entrega e o gerenciamento de reprodutores e recursos da equipe. É possível definir uma API para se comunicar entre as organizações.

As organizações do Cloud Foundry podem ser criadas para corresponder à maneira como você deseja trabalhar em vez da estrutura dentro de uma empresa. Geralmente, as organizações da empresa podem mudar, mas o desenvolvimento e a manutenção de um aplicativo continuam independentemente. Projete seu ambiente do {{site.data.keyword.Bluemix_notm}} para o tempo de vida dos aplicativos e não na estrutura da organização da empresa.

O desenvolvimento e a implementação iterativos podem resultar em apps que se expandem rapidamente. Seu design do processo de entrega deve ser capaz de aumentar a capacidade de modo rápido e fácil. Você deseja desenvolvimento contínuo com uma taxa de implementação rápida. Ter os seus espaços de desenvolvimento e de produção na mesma organização do {{site.data.keyword.Bluemix_notm}} fornece acesso aos mesmos recursos. O gerenciamento de espaços diferentes dentro de uma única organização reduz a carga de trabalho de administração. A equipe de desenvolvimento, teste e operações poderá colaborar facilmente se eles estiverem trabalhando dentro da mesma organização do {{site.data.keyword.Bluemix_notm}}.

Implemente um padrão de nomenclatura para identificar claramente a organização e o uso de espaço. Por exemplo, você pode incluir o tipo de nuvem, a região geográfica, o tipo de uso (como desenvolvimento, teste, produção), o nome do aplicativo e o número da versão ou revisão. As organizações e os espaços podem então ser facilmente identificados para propósitos de administração e acesso.  

O número de espaços pode se multiplicar rapidamente devido ao desenvolvimento iterativo. É possível definir quantos espaços forem necessários dentro de uma organização. Se você planejar definir muitos espaços, poderá desejar criar um aplicativo para ajudar a gerenciar os espaços. Quando o número de espaços exceder sessenta, você talvez desejará considerar definir outra organização.

Permita que uma pessoa crie e gerencie uma organização, defina os espaços e conceda acesso ao membro da equipe. Uma segunda pessoa pode receber o mesmo acesso para manter o ambiente quando o gerenciador de organização está desativado.  

Identifique todas as pessoas que precisam de acesso a cada espaço e organização. Determine seu papel. O cargo de um membro da equipe determina sua autoridade. Por exemplo, um desenvolvedor sênior precisa da autoridade para visualizar e atualizar todo o ambiente de desenvolvimento do {{site.data.keyword.Bluemix_notm}}. No entanto, um desenvolvedor júnior é limitado quanto ao que ele pode visualizar e atualizar.
