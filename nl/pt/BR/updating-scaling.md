---

copyright:

  years: 2018
lastupdated: "2018-12-19"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Atualização e ajuste de escala
{: #update-scale}

Atualize a instância de serviço do {{site.data.keyword.cfee_full_notm}} para a versão mais recente
para obter as funções e correções mais recentes do CFEE. As atualizações do CFEE podem incluir novas versões dos
serviços de suporte do Cloud Foundry e do CFEE (Kubernetes, Cloud Object Storage ou Compose for PostgreSQL). No entanto,
nem todas as atualizações do CFEE incluirão uma nova versão dos serviços de suporte do Cloud Foundry e do CFEE.

As atualizações de versão do CFEE são feitas no plano de controle que contém os componentes do CFEE e nas células. Também é possível escalar a capacidade da instância do CFEE incluindo ou excluindo células do aplicativo.

**Nota:** durante uma atualização de versão ou enquanto as células estiverem sendo incluídas ou
excluídas, algumas métricas (por exemplo, memória e CPU) mostradas nas páginas _Visão geral_, _Uso de
recurso_ e _Atualização e ajuste de escala_ podem não estar disponíveis.

## Atualizando a versão do CFEE
{: #update}

Os usuários precisam das permissões a seguir para poderem atualizar uma instância do CFEE para uma nova versão:
   * Função de _editor_ ou superior para uma instância do CFEE.
   * Função de _operador_ ou superior para o cluster do Kubernetes no qual o CFEE é
fornecido.

A atualização da versão do CFEE da instância do CFEE é um processo em duas etapas. Primeiro, atualize o plano de
controle que hospeda os componentes do CFEE. Em seguida, atualize as células que hospedam os aplicativos.

As regras e restrições a seguir se aplicam ao atualizar um CFEE para uma nova versão:
* O plano de controle deve ser atualizado primeiro. Assim que o plano de controle tiver sido atualizado, as
células poderão ser atualizadas.
* As células do aplicativo podem ser atualizadas apenas para a versão do plano de controle.  Ou seja, as células
do plano de controle podem estar em um nível de versão do CFEE mais alto do que as células do aplicativo, mas não
vice-versa.

Para atualizar a versão do CFEE da instância do CFEE:
1. Acesse o painel do
[{{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/dashboard/apps/) e abra o
{{site.data.keyword.cfee_full_notm}} que deseja atualizar.
2. No {{site.data.keyword.cfee_full_notm}}, acesse a entrada **Células** na área
de janela de navegação para abrir a página de células.
3. (opcional) Na tabela _Plano de controle_, é possível expandir a linha para ver os nós do
trabalhador no plano de controle.
4. Clique em **Atualizar**.
5. No diálogo Atualizar _Plano de controle_, selecione uma das versões disponíveis do CFEE e clique em
**Atualizar**. A atualização leva cerca de 45 minutos. A descrição da versão detalha as versões dos
componentes incluídos no pacote de versão do CFEE selecionado, juntamente com um link para o documento _O que há
de novo_ que descreve o conteúdo entregue nessa versão.
6. A coluna _Status dos nós_ mostra o progresso da atualização. Após a conclusão da atualização, a coluna _Versão_ refletirá a nova versão do CFEE.
7. Assim que a atualização das células do plano de controle estiver concluída, localize a tabela _Células_ e clique em **Atualizar**.
8. No diálogo _Atualizar plano de controle_, selecione a versão do CFEE e clique em *Atualizar*. Há
apenas uma versão disponível para a atualização das células porque elas podem ser atualizadas somente
para a versão do plano de controle. Uma única ação de atualização atualiza todas as células.
9. As células são atualizadas sequencialmente. A coluna _Status dos nós_ indica o progresso da
atualização de cada célula. Conforme as células são atualizadas, a nova versão é refletida na coluna _Versão_.

## Interrupções durante a atualização da versão
{: #update-disruption}

A atualização do plano de controle do Cloud Foundry não é interrompida.  No entanto, a atualização das células do
Cloud Foundry para uma nova versão do CFEE pode interromper a operação do ambiente do CFEE.  A atualização é executada
uma célula por vez, de modo que as instâncias do aplicativo em execução em uma célula são trazidas de volta assim que a atualização é concluída enquanto as outras células permanecem inativas durante a atualização. No entanto, alguns
aplicativos e serviços em execução no CFEE podem ficar indisponíveis sob algumas circunstâncias. Por exemplo, se o CFEE
tiver duas células do Cloud Foundry para capacidade total, um aplicativo com apenas uma instância ficará inativo
enquanto a versão estiver sendo atualizada porque a instância do aplicativo não pode ser movida para outra célula durante
a atualização da célula e, consequentemente, o aplicativo estará indisponível.  Mesmo com três células e três instâncias
por aplicativo, pode haver uma interrupção temporária na disponibilidade do aplicativo durante uma atualização de versão.

Durante a atualização da versão, pode haver uma discrepância nas métricas da memória e da CPU relatadas nos
medidores dos nós de célula mostradas na página _Visão geral_ do CFEE (que são geradas pelo cluster do Kubernetes) e as
mesmas métricas mostradas no painel _Nós_ no Grafana (que são geradas no nível do sistema operacional).

O status dos componentes do CFEE enquanto a atualização está em andamento será refletido na página Verificação de
funcionamento.  O reinício leva aproximadamente 45 minutos.

## Política de suporte e ciclo de versão
{: #version-cycle}

O serviço do Cloud Foundry Enterprise Environment geralmente libera uma nova versão regularmente. A versão do
serviço segue o formato de versão semântica _**Major.Minor.Patch**_ (https://semver.org/)

A versão _secundária_ é incrementada regularmente (em geral, mensalmente). A versão _principal_ também é incrementada, mas com menos frequência, geralmente quando há uma mudança
significativa.  A atualização para uma versão _principal_ pode resultar em alguma interrupção durante o
upgrade. As _correções_ entregam uma correção e são aplicadas à versão disponível mais recente. 

Para evitar tempo de inatividade do sistema, as instâncias do CFEE têm permissão para atualizar somente até duas
versões _principais_ à frente da versão atual. Usando o exemplo anterior, se a versão atual da instância
do CFEE fosse 3.1.2 e a versão de destino fosse 7.0.0, a instância do CFEE precisaria ser atualizada primeiro para a versão
5.x.x e, em seguida, para a versão de destino 7.0.0.

Os novos recursos e aprimoramentos para os recursos existentes entregues regularmente se tornam disponíveis
apenas na versão mais recente. As correções críticas são entregues na liberação mais recente somente nas três
versões _principais_ mais recentes (a versão mais recente e as duas versões anteriores). Por exemplo, se as
versões 4.x.x, 3.x.x e 2.x.x estiverem disponíveis, as versões 1.x.x não serão suportadas (ou seja, as correções não
serão entregues para as versões 1.x.x).  

As correções são entregues na versão disponível mais recente de uma determinada versão _principal_. Por
exemplo, se uma instância do CFEE estiver executando a versão 3.1.2, mas a versão mais recente disponível na
_principal_ 3.x.x for a versão 3.3.4, quaisquer correções serão entregues no código base da versão 3.3.x, o que
significa que a correção será entregue em uma (nova) versão 3.3.5. A instância do CFEE com a versão 3.1.2 precisaria ser
atualizada para a versão 3.3.5 para receber a nova correção (ou seja, atualizar apenas para a versão 3.3.4 não
resolve o problema corrigido na correção, que é entregue apenas na versão 3.3.5).

## Ajuste de escala da infraestrutura do CFEE
{: #scale}

Os usuários precisam das permissões a seguir para serem capazes de incluir ou remover as células do Cloud Foundry
para uma instância do CFEE:
* Função de _administrador_ ou superior para uma instância do CFEE.
* Função de _operador_ ou superior para o cluster do Kubernetes no qual o CFEE é
fornecido.

Para incluir as células do aplicativo na instância do CFEE:
1. Acesse o painel do
[{{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/dashboard/apps/) e abra o
{{site.data.keyword.cfee_full_notm}} no qual deseja incluir as células.
2. Clique em **Incluir célula** ao lado da tabela _Células_, que
abre a página _Incluir células do Cloud Foundry_.
3. Na página _Incluir células do Cloud Foundry_, selecione o número de células a incluir. A página
também mostra a geografia e a localização da instância do CFEE na qual as células serão incluídas. Ela também mostra o
número atual de células e a capacidade das células a serem incluídas (que é a mesma capacidade das células atuais). A
área de janela direita da página mostra o custo estimado das células incluídas juntamente com o novo custo
total estimado do ambiente.
4. Clique em **Incluir célula**.  
5. Acesse a página _Nós_. Uma nova linha é incluída na tabela _Células_ para cada
novo nó. A coluna _Status do nó_ indica o progresso de inclusão e implementação da célula no ambiente
do CFEE.
