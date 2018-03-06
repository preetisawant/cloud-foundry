---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2017-12-14"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Criando apps Cloud Foundry
{: #creating_cloud_foundry_apps}

Com o {{site.data.keyword.Bluemix}}, é possível criar seu app no console do {{site.data.keyword.Bluemix_notm}}. Em seguida, é possível decidir continuar a usar o console, usar a interface da linha de comandos cf ou usar o {{site.data.keyword.jazzhub_title}} para desenvolver, rastrear, planejar e implementar seu app.
{:shortdesc}

Ao criar um app no {{site.data.keyword.Bluemix_notm}}, é possível começar com um iniciador. Um *iniciador* é um modelo
que inclui serviços predefinidos e código do aplicativo que é configurado
com um buildpack específico. Há
dois tipos de iniciadores: modelos e tempos de execução.

Um *modelo* é um contêiner para um
aplicativo e
seu ambiente de tempo de execução associado e serviços predefinidos para
um domínio específico. Por exemplo, o
modelo Nuvem para dispositivo móvel inclui um tempo de execução do
Node.js, bem
como Dados móveis, Segurança do dispositivo móvel e Envio por push. Ele também inclui um
SDK e aplicativos de amostra para começar a desenvolver apps móveis que acessam esses serviços.

Um *tempo de execução* é o conjunto
de recursos usado para executar um aplicativo. O {{site.data.keyword.Bluemix_notm}} fornece
ambientes de tempo de execução como contêineres para diferentes tipos de aplicativos. Os ambientes de tempo de execução são integrados como buildpacks no
{{site.data.keyword.Bluemix_notm}}, são
automaticamente configurados para uso e requerem pouca ou nenhuma manutenção.

Para iniciar a criação de seu aplicativo, execute as etapas a seguir:
  1. Clique em **Catálogo** na barra de ferramentas do IBM Cloud.
  2. Clique em **Apps Cloud Foundry** e escolha um tempo de execução. Siga o guia Introdução para especificar um nome e selecione como deseja codificar. Clique em **Criar**.
  3. Quando tiver concluído o guia Introdução, clique em **Visão geral**.
  5. É possível incluir um serviço em seu app clicando em **Criar conexão** na Visão geral do app no painel. Procure e selecione serviços a partir do catálogo ou role até o término do catálogo e clique em **Serviços experimentais do {{site.data.keyword.Bluemix_notm}}** para procurar serviços experimentais. Ou, é possível usar a interface de linha de comandos cf. Consulte Opções para trabalhar com apps.
  6. Na página Visão geral, role para o cartão "Entrega contínua" e clique em **Visualizar cadeia de ferramentas**. A origem de seu app será salva em um repositório hospedado no Bluemix. Uma cadeia de ferramentas aberta que usa esse repositório e um pipeline de entrega para desenvolver e implementar seu app também é criada. Para obter mais informações sobre o serviço Continuous Delivery, veja <a href="https://console.ng.bluemix.net/docs/services/ContinuousDelivery/index.html#cd_getting_started">Introdução ao Continuous Delivery</a>.

**Nota:** se um serviço ligado a um app travar, o app poderá parar sua execução ou apresentar erros. O {{site.data.keyword.Bluemix_notm}} não
reinicia automaticamente o app para recuperar desses problemas. Considere codificar seu app para identificar e recuperar de indisponibilidades, de exceções
e de falhas de conexão. Consulte o tópico de resolução de problemas Os apps não são reiniciados automaticamente para obter mais informações.

## Opções para trabalhar com apps

Depois que seu app for criado, você terá algumas opções para continuar a incluir
serviços nele e para construí-lo e implementá-lo:

<dl><dt>Interface de linha de comandos cf</dt>
<dd>Use a <a href="https://github.com/cloudfoundry/cli#getting-started">interface da linha de comandos cf</a> para atualizar seu aplicativo, criar uma instância de serviço ou ligar o serviço ao seu aplicativo. Também é possível usar a interface de linha de comandos cloud-cli para criar, atualizar e excluir ofertas de serviço.</dd>
<dt>Interface com o usuário do {{site.data.keyword.Bluemix_notm}}</dt>
<dd>Use a <a href="https://console.bluemix.net/dashboard/apps">interface com o usuário</a> do {{site.data.keyword.Bluemix_notm}} para construir seu aplicativo, incluindo a escolha de quais serviços e tempos de execução combinar para resolver seu problema de negócios.</dd>
<dt>{{site.data.keyword.contdelivery_full}}</dt>
<dd>Use o {{site.data.keyword.contdelivery_short}} para automatizar construções, testes de unidade, implementações e mais. Edite e envie o código por push por meio do IDE avançado baseado na web. Crie cadeias de ferramentas para ativar as integrações de ferramentas que suportam as tarefas de desenvolvimento, implementação e operação. O serviço Continuous Delivery inclui o Delivery Pipeline, o Eclipse Orion Web IDE e o Git Repos and Issue Tracking. Para obter mais informações, veja <a href="https://console.ng.bluemix.net/docs/services/ContinuousDelivery/index.html#cd_getting_started">Introdução ao Continuous Delivery</a>.</dd>
</dl>

## Dicas

Use as dicas a seguir enquanto desenvolve seus apps da web:

<dl><dt>Persistência</dt>
<dd>Não especifique nenhum armazenamento local para seus aplicativos. Cada instância de seu aplicativo, mesmo que apenas uma instância esteja em execução,
pode ser reiniciada ou movida para uma máquina virtual diferente a qualquer momento, em
geral para balanceamento de carga. Qualquer coisa armazenada no armazenamento local é apagada quando o
aplicativo é movido ou excluído. Use um dos serviços de armazenamento de dados do
{{site.data.keyword.Bluemix_notm}} para persistência.</dd>
<dt>Limites de recursos</dt>
<dd>Esteja ciente dos limites sobre as quantidades de recursos que podem ser usados
por uma conta para teste. Os limites
são os seguintes:
<table style="width:100%">
<caption>Tabela 1. Limites de recurso do {{site.data.keyword.Bluemix_notm}} para uma conta para teste</caption>
  <th>Tipo de recurso</th>	<th>Limite de quantidade</th>
<tr><td>Número de serviços que são usados em todos os apps</td> <td>10</td>
<tr><td>Memória usada em todos os apps</td> <td>	2 G</td>
<tr><td>Número de rotas</td> <td>500</td>
</table>
</dd>
</dl>
