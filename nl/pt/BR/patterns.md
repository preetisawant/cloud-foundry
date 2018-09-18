---

copyright:

  years: 2015, 2018
lastupdated: "2018-04-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Panorâmica estrutural
{: #patterns}

Para um projeto bem-sucedido, reserve um tempo para planejar e projetar quais recursos você precisa e quais são seus requisitos corporativos. Para ajudá-lo a começar, considere as perguntas a seguir:
{:shortdesc}

* Quantos e que tipo de apps você está desenvolvendo?
* Que serviços os apps precisam acessar?
* Quem colabora no processo de desenvolvimento e que função essa pessoa executa?
* Qual grau de isolamento é necessário para cada fase do projeto?
* A sua empresa fornece os recursos de infraestrutura?
* Como a sua empresa se comunica?
* Existe um padrão de nomenclatura que é possível implementar para identificar claramente a organização e o uso de espaço?

Como parte da decisão de qual tipo de ambiente de nuvem você precisa, planeje a estrutura de sua conta, organizações, espaços, recursos e membros da equipe.

Para a maioria das empresas, uma única conta do {{site.data.keyword.Bluemix_notm}} é suficiente. Para empresas maiores nas quais há mais de uma área de negócios, você pode desejar uma conta do {{site.data.keyword.Bluemix_notm}} para cada domínio de negócios. Por exemplo, dentro de uma grande corporação bancária, pode haver contas separadas para os setores varejista e comercial.

A tabela a seguir fornece um resumo de alguns dos elementos chave.

| Elemento   | Descrição |
|-----------|---------------|
|| Contém uma ou mais organizações. Deve-se ter uma conta Pay-As-You-Go para criar mais de uma organização. |
|| Pode possuir apenas uma conta. |
|| Pode incluir um ou mais gerenciadores de organização para delegar o gerenciamento da organização, que inclui as permissões de leitura e gravação para as organizações. |
|| Pode ser um membro da equipe em organizações e espaços em outras contas do {{site.data.keyword.Bluemix_notm}}. |
| Organização   | Contém um ou mais espaços. |
|| Contém um ou mais gerenciadores de organização. |
|| Contém um ou mais membros da equipe. Uma ou mais funções podem ser concedidas a cada membro da equipe. |
|| Os encargos de uso, que são gerados por um aplicativo implementado em um espaço, são relatados no nível de organização. |
| Espaço   | Contém um ou mais recursos. |
|| Contém um ou mais apps. |
|| Contém um ou mais gerenciadores de espaço. |
|| Contém um ou mais membros da equipe. Cada usuário já deve ser um membro da equipe na organização proprietária. Uma ou mais funções podem ser concedidas a cada membro da equipe. |
| Membro da equipe   | Pode ser incluído em uma ou mais organizações e espaços entre contas diferentes. |
|| Pode ter mais de uma função dentro da mesma organização, espaço ou ambos. |
{:caption="Tabela 1. Descrição dos elementos-chave" caption-side="top"}

