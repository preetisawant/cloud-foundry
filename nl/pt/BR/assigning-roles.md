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

# Designar funções
{: #roles}

É possível conceder múltiplas funções para membros da equipe em uma conta do {{site.data.keyword.Bluemix_notm}}. Essas funções definem as permissões do usuário para gerenciar conta e recursos da organização:
é possível conceder [funções de usuário](/docs/iam/users_roles.html#userroles) para membros de uma organização. Essas funções definem o nível de acesso dentro da organização e restringem quem pode acessar um espaço e seus recursos. Por exemplo, é possível conceder aos usuários permissões diferentes para espaços diferentes.

## Proprietário da conta
{: #accountowner}

Independentemente se você projetar uma arquitetura de organização múltipla ou uma arquitetura de organização única, o proprietário da conta é o superusuário do ambiente de nuvem.

As tarefas principais do proprietário da conta incluem:

* Gerenciar os recursos da conta global.
* Criando organizações.
* Incluindo membros da equipe na conta.

O proprietário da conta também pode incluir um ou mais usuários como gerenciadores de uma organização, designando a esses usuários a função **Gerenciador**. Considere incluir dois usuários como gerenciadores de organização. O primeiro usuário age como o gerenciador principal da organização. O segundo usuário age como o gerenciador substituto, no caso, o gerenciador principal está indisponível.

## Funções de usuário
{: #userroles}

As funções de usuário definem as permissões que é possível designar a um membro da equipe em uma organização e definem o nível de acesso que um membro da equipe tem dentro da organização e cada espaço.

Em uma arquitetura de organização múltipla ou em uma arquitetura de organização única, defina os membros da equipe e as permissões que cada usuário requer para concluir seu trabalho:

1. Identifique o conjunto de usuários que requer acesso a uma organização.
2. Defina as permissões para cada membro da equipe na organização e em um espaço da organização.
3. Selecione a função que concede a um usuário as permissões que ele requer.

   * Gerente da organização
   * Auditor da organização
   * Gerenciador de faturamento da organização
   * Gerenciador de espaço
   * Desenvolvedor de Espaço
   * Auditor de espaço

### Gerente da organização
{: #bporgmgr}

As tarefas pelas quais um gerenciador de organização é responsável incluem criar espaços, distribuir a cota entre os espaços, convidar membros da equipe e, opcionalmente, conceder funções específicas a eles e definir domínios customizados.

### Auditor da organização
{: #bporgauditor}

Os membros da equipe com a função de **Auditor** da organização podem monitorar a cota, o uso de recursos e os membros da equipe para todos os espaços em uma organização.
Os auditores podem, então, relatar sobre a eficiência da organização e destacar quaisquer problemas potenciais.

* Ao adotar uma arquitetura de organização múltipla, você poderá desejar conceder a função de auditor para os mesmos membros da equipe para cada organização que faz parte da conta.
Em seguida, esses membros da equipe podem monitorar a cota em todas as organizações em seu ambiente de nuvem e obter uma visualização global da conta.
* Ao adotar uma arquitetura de organização única, conceda a função de auditor para os membros da equipe com a responsabilidade de monitorar o uso de cota e a eficiência geral
da organização.

### Gerenciador de faturamento da organização
{: #bporgbillingmgr}

Os membros da equipe com a função de **Gerenciador de faturamento** podem monitorar os custos de uma organização.

* Ao adotar uma arquitetura de organização múltipla, você pode desejar conceder a função de faturamento para o mesmo conjunto de membros da equipe para cada organização que faz parte da conta. Em seguida, esses membros da equipe podem monitorar o custo de cada organização e obter uma visualização global da conta.
* Em uma arquitetura de organização única, identifique os usuários que são responsáveis por monitorar o custo.

### Gerenciador de espaço
{: #bpspacemgr}

O **Gerenciador** de espaço é responsável por qualquer trabalho feito dentro do espaço que ele gerencia e controla. O gerenciador de espaço pode executar as tarefas a seguir:

* Monitorar a cota que é permitida para o espaço.
* Solicitar mais recursos para o gerenciador de organização.
* Notificar o gerenciador de organização dos recursos que não são necessários.
* Incluir membros da equipe no espaço com a função **Desenvolvedor**.
* Opcionalmente, designar a função de **Gerenciador** de espaço a um membro da equipe para agir como um gerenciador de espaço substituto na sua ausência.

### Desenvolvedor de Espaço
{: #bpspacedev}

Um desenvolvedor de espaço pode executar as tarefas a seguir:

* Gerenciar Cloud Foundry apps.
* Provisão e configure os serviços do  {{site.data.keyword.Bluemix_notm}} .
* Associar domínios a apps.

### Auditor de espaço
{: #bpspaceauditor}

Para cada espaço, você pode desejar conceder a função de **Auditor** de espaço para os mesmos membros da equipe com a função de **Auditor** da organização. Em sua empresa, essa função pode precisar ser concedida a um conjunto específico de usuários.

