---

copyright:
  years: 2018
lastupdated: "2018-08-15"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Uso de recursos

Os administradores e desenvolvedores podem ver como a capacidade do recurso (memória e CPU) de um CFEE é usada por aplicativos e células. Para monitorar o uso de recursos em um ambiente do CFEE:

1. Acesse o[Painel do {{site.data.keyword.Bluemix_notm}} Cloud Foundry Environments](https://console.bluemix.net/dashboard/cloudfoundry?filter=cf_environments) e abra o {{site.data.keyword.cfee_full_notm}} no qual você deseja gerenciar o uso de recursos.
2. Na interface com o usuário do {{site.data.keyword.cfee_full_notm}}, acesse a entrada **Uso de recursos** na área de janela de navegação à esquerda para abrir a página _Uso de recursos_. 
Na página _Uso de recurso_, é possível acessar as subentradas _Aplicativos_ ou _Células_ para abrir as páginas correspondentes. As informações exibidas nas páginas _Aplicativos_ e _Células_ podem ser consideradas duas maneiras de dividir o uso de recursos:
   * A página **Aplicativos** analisa o uso de recurso por aplicativos agregados nas instâncias.
   * A página **Células** mostra o uso de recursos de instâncias do aplicativo em execução em células específicas. O padrão de uso de recursos entre células pode fornecer insights sobre a capacidade e a distribuição de carga.  Por exemplo, isso pode ajudar a identificar problemas com o balanceamento de carga de aplicativos (por exemplo, grandes diferenças nos recursos usados por um aplicativo entre células) ou uso de recursos que se aproxima da capacidade geral (ou seja, grandes porcentagens de uso de recursos em todas as células).

**Nota:** os dados de uso de recursos representam o uso de recursos durante o ciclo de coleta dos últimos 5 minutos. Os dados de uso de recursos podem ser atualizados clicando em **Atualizar dados** na parte superior da página.

## Aplicativos
{: #usage_apps}

A página Aplicativos possui duas seções:
1. Gráficos de barras horizontais mostrando o uso das memórias física e reservada.
   * Memórias reservada e física usadas pelos **apps selecionados** na tabela abaixo.
   * Memórias reservada e física usadas por **todos os apps** na instância do CFEE.
   * Memória física usada pelo **sistema**, o que inclui a memória usada pelo plano de controle do Cloud Foundry e a memória do aplicativo armazenada em cache pelo plano de controle do Cloud Foundry.
   * **Total disponível** das memórias reservada e física na instância do CFEE.
   
   **Nota:** quando os aplicativos reservam mais memória do que há fisicamente disponível, um contorno vermelho pontilhado no gráfico de barras de memória reservada é mostrado para representar a quantia de memória sobrerreservada pelos aplicativos selecionados.

   Para mostrar a porcentagem de memória e CPU usada por todos os apps ou aqueles selecionados na tabela, passe o mouse sobre a parte correspondente do gráfico.  Passar o mouse sobre a parte *todos os apps* do gráfico mostra a porcentagem de memória e CPU relativa ao total disponível. Passar o mouse sobre a parte *apps selecionados* do gráfico mostra a porcentagem de memória e CPU relativa ao total de CPU ou memória.

2. Uma tabela que lista todos os aplicativos.  Cada linha na tabela exibe informações de recursos para esse aplicativo.  Expandir uma linha mostra informações de uso de recursos para as várias instâncias desse aplicativo.

  A primeira coluna na tabela é uma caixa de seleção que determina se o aplicativo correspondente deve ser incluído no conjunto de *Apps selecionados* a ser incluído no gráfico na parte superior da página. Para incluir (ou excluir) um aplicativo no conjunto selecionado, clique na caixa de seleção correspondente.  Quando um aplicativo é selecionado ou desmarcado para inclusão no conjunto, o gráfico é atualizado.  
A legenda _Aplicativos selecionados_ à direita do gráfico de barras indica (entre parênteses) o número
de aplicativos atualmente selecionados para inclusão no gráfico.

  As informações a seguir são exibidas como colunas na tabela de aplicativos:
   * **Nome do aplicativo**: o nome do aplicativo ou da instância do aplicativo. Se o usuário não tiver permissão para acessar o aplicativo, o GUID do aplicativo será exibido no lugar.
   * **Instâncias**: para um aplicativo, isso representa o número de instâncias em execução.  Para uma instância do aplicativo (mostrada abaixo do nome do aplicativo quando a linha do aplicativo é expandida), isso representa o nome da célula em que a instância do aplicativo é executada.
   * **Memória física total**: MBs de memória física usados por todas as instâncias de um aplicativo.  A memória física usada por um aplicativo é igual à soma da memória física usada por todas as instâncias do aplicativo.
   * **Memória reservada total**: MBs de memória reservados por todas as instâncias de um aplicativo.  A memória reservada por um aplicativo é igual à soma da memória reservada por todas as instâncias do aplicativo.
   * **Média de CPU (% da célula)**: para instâncias do aplicativo, a métrica representa a média de CPU **dentro da célula na qual ela é executada**.  Para um aplicativo, ela representa a média de uso de CPU entre suas médias da instância.
   * **Máximo de CPU (% da célula)**: para instâncias do aplicativo, a métrica representa o máximo de CPU usado por essa instância **dentro da célula na qual ela é executada**.  Para um aplicativo, ela representa o maior uso máximo de CPU de suas instâncias.
   * **CPU (% do sistema) **: a porcentagem do total de CPU disponível no CFEE usada por um aplicativo e suas instâncias.  A CPU usada por um aplicativo é igual à soma de porcentagens de CPU usadas por todas as instâncias do aplicativo.
   * **Solicitações**: o número de solicitações para um aplicativo durante o ciclo de coleta de dados mais recente (cinco minutos).
   * **Organização**: a organização na qual o aplicativo é implementado. Se o usuário não for um membro da organização, o GUID da organização será exibido no lugar.

Expanda uma linha do aplicativo na tabela para ver a lista de instâncias do aplicativo e suas métricas de uso de recursos correspondentes.

### Filtrando aplicativos
Filtre o conteúdo da tabela por meio dos menus suspensos de filtro **Aplicativos** e
**Organizações** localizados acima da tabela.

Além disso, é possível usar o campo de entrada de filtro acima da tabela para mostrar somente os aplicativos que correspondem à sequência que você insere no campo de filtro.  O filtro é refletido em ambos, na tabela e no gráfico acima dele.

**Nota:** os filtros funcionam independentemente das linhas da tabela selecionadas (por meio da caixa de seleção na primeira tabela de coluna) para inclusão no conjunto de _Apps selecionados_ incluído no gráfico acima. Por exemplo, se houver um total de dez aplicativos no ambiente do CFEE e cinco deles forem selecionados para inclusão no gráfico, quando você aplicar um filtro que corresponder a somente uma instância do aplicativo, somente essa instância do aplicativo aparecerá na tabela.  Além disso, o conjunto de _Apps selecionados_ agora incluirá somente esse aplicativo correspondente e o gráfico será atualizado de acordo.  Quando você remover o filtro, todos os dez aplicativos serão mostrados novamente na tabela e o conjunto de _Apps selecionados_ será reconfigurado para incluir todos os apps.


## Células
{: #usage_cells}

A página Células possui duas seções:
1. Gráficos de barras verticais mostrando:
   * Memória *total disponível* e CPU disponível na instância do CFEE.
   * Memória e CPU usadas pelas **Instâncias do app selecionadas** na instância do CFEE.
   * Memória e CPU usadas por **Todas as instâncias do app** na instância do CFEE.
   * Memória e CPU usadas pelo **Sistema** na tabela abaixo. O uso do sistema representa o recurso usado pelo componente de serviço CFEE mais o cache do aplicativo.
   * Total de memória e de CPU disponíveis na célula. O **Total de células** é igual ao total (memória ou CPU) disponível no nó do trabalho do Kubernetes (no qual a célula é provisionada) menos o que é usado pelo sistema.

   Para mostrar a porcentagem de memória ou CPU usada por todas as instâncias do app ou pelas instâncias do app selecionadas na tabela, passe o mouse sobre a parte correspondente do gráfico.  Passar o mouse sobre a barra de gráfico mostra a memória ou CPU absoluta disponível, a memória ou CPU usada por todos os apps e a memória ou CPU usada pelo sistema + cache.  Também mostra a porcentagem de memória ou CPU usada por todos os apps e pelo sistema + cache relativa ao total disponível.

2. Uma tabela listando todas as células e instâncias de aplicativos que estão em execução nelas.  Cada linha na tabela exibe informações de recurso para essa célula e instância do aplicativo.

  A primeira coluna na tabela é uma caixa de seleção que determina se a instância do aplicativo correspondente deve ser incluída no conjunto de *Instâncias do app selecionadas* a ser incluído no gráfico na parte superior da página. Para incluir (ou excluir) uma instância do aplicativo no conjunto selecionado, clique na caixa de seleção correspondente.  Quando uma instância do aplicativo é selecionada ou desmarcada para inclusão no conjunto, o gráfico é atualizado.

  As informações a seguir são exibidas como colunas na tabela:
   * **Nome da célula**: o nome da célula.
   * **Nome do aplicativo**: o nome do aplicativo em execução na célula. Se o usuário não tiver permissão para acessar o aplicativo, o GUID do aplicativo será exibido no lugar.
   * **Instâncias**: o número de instâncias do aplicativo em execução na célula.
   * **Memória física**: MBs de memória física usados pela instância do aplicativo em execução na célula.
   * **Memória reservada**: MBs de memória reservados pela instância do aplicativo em execução na célula.
   * **CPU (% )**: a porcentagem de total de CPU disponível no CFEE usado pela instância do aplicativo em execução na célula.

### Filtrando células e instâncias do aplicativo
É possível filtrar o conteúdo da tabela por meio do menu suspenso de filtro **Células** localizado
acima da tabela e selecionando as células a serem exibidas na tabela.

Além disso, é possível usar o campo de entrada de filtro acima da tabela para mostrar somente as instâncias de aplicativos que correspondem à sequência que você insere no campo de filtro.  O filtro é refletido em ambos, na tabela e no gráfico acima dele.

**Nota:** os filtros funcionam independentemente das linhas da tabela selecionadas (por meio da caixa de seleção na primeira tabela de coluna) para inclusão no conjunto de _Instâncias do app selecionadas_ incluídas no gráfico acima. Por exemplo, se houver um total de dez instâncias do aplicativo no ambiente do CFEE e cinco delas forem selecionadas para inclusão no gráfico, quando você aplicar um filtro que corresponde a somente uma instância do aplicativo, somente essa instância do aplicativo aparecerá na tabela.  Além disso, o conjunto de _Instâncias do app selecionadas_ agora incluirá somente essa instância do app e o gráfico será atualizado de acordo.  Quando você remover o filtro, todas as dez instâncias do aplicativo serão mostradas novamente na tabela e o conjunto de _Instâncias do app selecionadas_ será reconfigurado para incluir todas as instâncias do app.
