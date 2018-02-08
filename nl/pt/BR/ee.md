---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2017-12-15"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Cenário: Desenvolvimento de ponta a ponta
{: #ee}


É possível usar o console do {{site.data.keyword.Bluemix}}, a plataforma e uma seleção de ferramentas ao construir, executar e implementar seus apps. Siga este cenário de desenvolvimento de ponta a ponta
para iniciar.
{:shortdesc}

## Inscrevendo-se
{: #ee_start}

Para começar, acesse [o console do IBM Cloud ![Ícone de link externo](../icons/launch-glyph.svg)](https://bluemix.net){: new_window}. Inscreva-se para obter um IBMid e efetue login no {{site.data.keyword.Bluemix_notm}} para iniciar sua avaliação grátis de 30 dias. O {{site.data.keyword.Bluemix_notm}} fornece
um abono de 2 GB de memória de tempo de execução e 10 instâncias de serviço para sua
avaliação grátis.

## Desenvolvendo seu aplicativo
{: #develop}

Há três formas de desenvolver seu app:

* Com o [serviço de Entrega Contínua](#ee_cd)
* No painel da [interface com o usuário do IBM Cloud](#ee_appui)
* Na [linha de comandos do Cloud Foundry](#ee_cf)

## Desenvolvendo e implementando seus apps usando cadeias de ferramentas e o serviço {{site.data.keyword.contdelivery_short}}
{: #ee_cd}

<a href="/docs/services/ContinuousDelivery/toolchains_working.html#creating_a_toolchain_from_an_app">Inclua uma cadeia de ferramentas</a> que inclua o serviço {{site.data.keyword.contdelivery_full}} em seu app. Em seguida, <a href="/docs/services/ContinuousDelivery/toolchains_using.html#toolchains-using">use a cadeia de ferramentas</a> para desenvolver e implementar seu app.

## Criando seu app da web com a interface com o usuário do {{site.data.keyword.Bluemix_notm}}
{: #ee_appui}

Depois de se inscrever, comece a construir seu primeiro app usando o catálogo e painel do {{site.data.keyword.Bluemix_notm}}.

No {{site.data.keyword.Bluemix_notm}},
os apps são associados a organizações e espaços. Uma organização
pertence e é usada por vários colaboradores. Inicialmente, você obtém uma
organização padrão que é nomeada depois de seu nome de usuário e você é
o único colaborador. Você também obtém um espaço com essa organização. O espaço é um ambiente para executar seus apps; por exemplo, é possível ter um espaço dev como um ambiente de
desenvolvimento, um espaço test como um ambiente de teste e um espaço production como um ambiente de produção. Cada um dos ambientes pertence a uma região. Com o {{site.data.keyword.Bluemix_notm}},
é possível implementar seus aplicativos em uma região geográfica específica
para menor latência de rede, privacidade de dados e melhor disponibilidade.

Para este cenário, você deseja desenvolver um app da web usando Node.js. Suponha que você esteja nos EUA e a maioria dos usuários do app também esteja
nos EUA. Você decide construir e executar o app próximo da base do
usuário, para se beneficiar da latência de rede inferior. Após efetuar login no {{site.data.keyword.Bluemix_notm}}, clique no link Preferências da conta do usuário e, em seguida, selecione a região **Sul dos EUA**. É possível, então, executar as
etapas a seguir para criar um app:

  1. Clique em **Catálogo** na barra de ferramentas do {{site.data.keyword.Bluemix_notm}}.
  2. Selecione **Apps Cloud Foundry**.
  3. Selecione **SDK for Node.js**.
  4. Digite um nome exclusivo para o app e clique em **Criar**. O nome do app deve ser exclusivo
em todo o ambiente do {{site.data.keyword.Bluemix_notm}}.

Agora, é possível ver o **Tutorial de Introdução**. Siga as instruções para fazer download do código de início de seu app, modificar e implementá-lo.

O app é designado com uma instância e 512 MB de cota de memória, por
padrão. É possível aumentar a memória ou incluir mais instâncias para obter
alta disponibilidade do app, por exemplo, 3 instâncias com 1 GB de
memória por instância. Clique em **Visualizar a visão geral do app** para
especificar as instâncias do app e a cota de memória. Por exemplo, digite 3 para
instâncias e 1 GB para cota de memória e clique em **Salvar**. Também é possível ver os arquivos, logs e variáveis de ambiente para solucionar
seus problemas.

### Ligando um serviço usando a interface com o usuário do {{site.data.keyword.Bluemix_notm}}
{: #ee_bindui}

Depois de criar seu app, conecte-se a um banco de dados com seu app. É possível armazenar e observar os dados do app usando a linguagem de consulta de banco de dados. Neste cenário, você decide
usar o serviço {{site.data.keyword.cloudant}}
fornecido pelo {{site.data.keyword.Bluemix_notm}}.

Para usar serviços no aplicativo, criar uma instância de serviço e ligue seu aplicativo à instância de serviço executando as etapas a seguir:

  1. No catálogo do {{site.data.keyword.Bluemix_notm}}, selecione o serviço {{site.data.keyword.cloudant}}. Inclua um nome exclusivo para o serviço Cloudant e clique em **Criar**. No painel Gerenciar do Cloudant, ative o serviço clicando em **Ativar**.
  2. Clique em
**Conexões**. Em seguida, clique em **Criar conexão**.
  3. Clique em **Conectar** próximo ao seu app.
  4. A janela Remontar app é exibida. Clique em **Nova preparação**.

Agora seu app está ligado ao serviço {{site.data.keyword.cloudant}}. É possível localizar todos os dados necessários para que o aplicativo se comunique com a instância de serviço na variável de ambiente VCAP_SERVICES. Por exemplo, como o
{{site.data.keyword.Bluemix_notm}} hospeda
diversos aplicativos na mesma máquina virtual, os aplicativos não podem usar o mesmo
número de porta HTTP para receber solicitações recebidas. Para evitar conflitos, cada
aplicativo recebe um número de porta exclusivo. Esse número de porta está disponível na variável VCAP_APP_PORT.

É possível ver a lista inteira de VCAP_SERVICES associada ao seu app no painel. Para ver essa lista, clique no Menu na barra de ferramentas do IBM Cloud, em seguida, clique em **Painel**. Clique em seu app. Em seguida, clique em **Tempos de execução** e selecione a guia **Variáveis de ambiente**.

**Nota:** essa variável de ambiente é a serialização de um objeto JSON com uma entrada para cada instância de serviço a que o app está ligado. A quantia e o tipo de
dados que cada instância de serviço fornece são específicos do serviço. Quando seu app não usar nenhum serviço, VCAP_SERVICES será um objeto JSON vazio. Essa variável de ambiente será usada somente quando
você incluir um serviço no app.

## Construindo seu app usando a cli cf
{: #ee_cf}

O {{site.data.keyword.Bluemix_notm}} fornece
várias ferramentas para você iniciar a codificação com seu app, por exemplo, a interface de linha
de comandos cf e as ferramentas Eclipse. É possível escolher a interface da linha de comandos cf para iniciar a codificação com seu app.

  1. Primeiramente, faça o download e desenvolva o código do app.

    1. Clique em Introdução no painel do app. Clique no link **Fazer download do código de amostra** para fazer download do código do app.
    2. Extraia o arquivo transferido por download em um diretório, por exemplo, `C:\test`.
    3. Desenvolva o código com seu ambiente de desenvolvimento integrado
local.

  2. Instale a interface da linha de comandos (CLI) **cf**.

    1. Faça download do programa de instalação da ferramenta de linha de comandos cf para seu sistema operacional.
    2. Siga o assistente de ferramenta para concluir a instalação.
    3. Use o comando `cf -v` para verificar a versão da interface de linha de comandos cf.

    **Requisito:** certifique-se de sempre usar a versão mais recente da ferramenta de linha de comandos cf.

  3. Depois de instalar a interface de linha de comandos **cf**, deve-se especificar
com qual região do {{site.data.keyword.Bluemix_notm}} você deseja trabalhar usando o comando **cf api**. A interface da linha de comandos **cf** usa *https://api.[Bluemix_URL]*, em que *Bluemix_URL* é a URL da região. O terminal de API para a região Sul dos EUA é `ng.bluemix.net`. Insira o comando a seguir para se conectar ao
{{site.data.keyword.Bluemix_notm}}:

  ```
  cf api https://api.ng.bluemix.net
  ```

  Para localizar outros terminais da API, veja [Regiões](/docs/overview/cf.html#ov_intro_reg). Após especificar a região do {{site.data.keyword.Bluemix_notm}},
as informações da localização especificadas são salvas.

  4. Em seguida, efetue login no {{site.data.keyword.Bluemix_notm}} usando o comando `cf login`.

  ```
  cf login -u your_user_ID -p ***** -o your_org_name -s your_space_name
  ```

  Se a sua organização usa a conexão única, use `cf login -sso`.

  5. Depois de ter efetuado login no {{site.data.keyword.Bluemix_notm}},
você estará pronto para implementar o app novamente no {{site.data.keyword.Bluemix_notm}}. No diretório `C:\test` de seu app, insira o comando a seguir:

  ```
  cf push [your_appname]
  ```

  Para obter mais informações sobre o comando **cf push**, veja [Fazendo upload do seu app](/docs/cfapps/hostingapps.html#ht_cfcli).

  6. Agora, é possível acessar o app inserindo a URL do app
a seguir em um navegador:
  ```
  http://your_app.stage1.mybluemix.net
  ```

Também é possível escolher outras ferramentas para construir o app, como
as ferramentas Eclipse. Para obter mais informações, veja a página Introdução de seu app no painel do {{site.data.keyword.Bluemix_notm}}.

### Ligando um serviço usando a cli cf
{: #ee_cfbind}

Também é possível ligar um serviço usando a interface da linha de comandos do **cf**. Suponha que você deseja incluir o serviço {{site.data.keyword.cloudant}} em seu app com a interface da linha de comandos cf.

Para usar o serviço {{site.data.keyword.cloudant}} dentro de seu app, crie uma instância de serviço do Cloudant, ligue o app à instância de serviço e, em seguida, use a instância de serviço. O mesmo procedimento se aplica a todos os outros serviços.

  1. Crie uma instância de serviço Cloudant NoSQL DB.

  Use o comando cf create-service para criar uma nova instância de um serviço. Neste exemplo, *Lite* é o nome do plano. Por
exemplo:

  ```
  cf create-service cloudantNoSQLDB Lite [your_name_for_your_cloudant_service]
  ```

  Também é possível usar o comando cf services para ver a lista de instâncias de serviço criadas.

  ```
  cf services
  ```

  Depois de uma instância de serviço ser criada, ele ficará disponível para ligação e
uso de qualquer um de seus aplicativos.

  2. Ligue a instância de serviço ao seu app.

  Para usar uma instância de serviço, deve-se ligá-la ao seu aplicativo. Use o comando cf bind-service para ligar uma instância de serviço a um aplicativo especificando o nome do aplicativo e a instância de serviço criada.

  ```
  cf bind-service [your_app_name] [your_name_for_your_cloudant_service]
  ```

  A ligação de uma instância de serviço a um aplicativo permite que o
{{site.data.keyword.Bluemix_notm}} se
comunique com o serviço e especifique que um novo aplicativo irá se comunicar com essa
instância de serviço. Para serviços diferentes, o
{{site.data.keyword.Bluemix_notm}} pode
processar o aplicativo e a instância de serviço de maneira diferente durante a ligação. Por
exemplo, alguns serviços podem criar um novo locatário para cada aplicativo que se
comunica com a instância de serviço. O serviço responde de volta ao {{site.data.keyword.Bluemix_notm}} com
informações, como credenciais, que devem ser transmitidas ao aplicativo para comunicação
entre o aplicativo e o serviço.

  **Nota:** se o aplicativo estiver em execução quando for ligado a uma instância de serviço, a variável de ambiente VCAP_SERVICES não será atualizada até que o aplicativo seja reiniciado. Para reiniciar seu aplicativo, use o comando cf restart.

  3. Use a instância de serviço.

  Neste cenário, a variável de ambiente VCAP_SERVICES inclui informações, como os itens a seguir, que um aplicativo pode usar para se conectar a esta instância do {{site.data.keyword.cloudant}}:

  <dl><dt>username</dt>
  <dd>d72837bb-b341-4038-9c8e-7f7232916197-bluemix</dd>
  <dt>password</dt>
  <dd>secret</dd>
  <dt>url</dt>
  <dd>https://d72837bb-b341-4038-9c8e-7f7232916197-bluemix:b6fc4708942b70a88853177ee52a528d07a43fa8575a69abeb8e044a7b0a7424@d72837bb-b341-4038-9c8e-7f7232916197-bluemix.cloudant.com</dd></dl>

  Por exemplo, o app Node.js pode acessar estas
informações, conforme a seguir:
  ```
  if (process.env.VCAP_SERVICES) {
        var env = JSON.parse(process.env.VCAP_SERVICES);
        var cloudant = env['cloudantNoSQLDB'][0].credentials;
  } else {
        var cloudant = {
                "username" : "user1",
                "password" : "secret",
                "url" : "https://user1:secret@localhost:25002"
                }
        };
  ```

  **Nota:** conforme visto no código de amostra, para se conectar a uma instância de serviço {{site.data.keyword.cloudant}}, é possível verificar se a variável de ambiente VCAP_SERVICES existe primeiro. Se existir, o aplicativo poderá usar as propriedades da variável do cloudant para acessar o banco de dados. No entanto, se a variável de ambiente VCAP_SERVICES não estiver presente, a instância de serviço local do {{site.data.keyword.cloudant}} será usada com os valores padrão fornecidos.

  4. Interaja com a instância de serviço.

  É possível interagir com a instância de serviço usando as informações de credenciais. As ações que podem ser tomadas incluem leitura, gravação e atualização. O
exemplo a seguir demonstra como inserir um objeto JSON na instância de serviço
{{site.data.keyword.cloudant}}:

  ```
  // create a new message
var create_message = function(req, res) {
  require('cloudantdb').connect(cloudant.url, function(err, conn) {
    var collection = conn.collection('messages');

    // create message record
    var parsedUrl = require('url').parse(req.url, true);
    var queryObject = parsedUrl.query;
    var name = (queryObject["name"] || 'Bluemix');
    var message = { 'message': 'Hello, ' + name, 'ts': new Date()
};
    collection.insert(message, {safe:true}, function(err){
      if (err) { console.log(err.stack); }
      res.writeHead(200, {'Content-Type': 'text/plain'});
      res.write(JSON.stringify(message));
      res.end('\n');
    });
  });
}
  ```

  5. **Opcional:** desvincular ou excluir uma instância de serviço.

  Talvez você queira desvincular ou excluir uma instância de serviço quando
ela não for mais usada ou quando você desejar liberar alguns espaços. Para desvincular uma instância de serviço do app, use o **comando cf unbind-service**; para excluir uma instância de serviço, use o comando **cf delete-service**.

  Para obter mais informações sobre serviços, consulte Serviços. Para obter mais informações sobre as opções **cf** que é possível usar
para gerenciar seus aplicativos no ambiente
{{site.data.keyword.Bluemix_notm}}, emita
**cf --help** na interface de linha de comandos **cf**.

  **Nota:** assegure-se de que não precisa mais de uma instância de serviço antes de excluí-la. A
exclusão de uma instância de serviço apaga todos os dados que estão associados a essa
instância do serviço. Qualquer aplicativo que estiver ligado a um serviço excluído não poderá ter sua variável de ambiente VCAP_SERVICES atualizada até que o aplicativo seja reiniciado.

## Calculando seu custo de app
{: #ee_billing}

Sua avaliação grátis de 30 dias expirou, mas você deseja continuar
usando o {{site.data.keyword.Bluemix_notm}}. Deve-se incluir suas informações de cartão de crédito para uma conta Pré-paga
ou uma conta de Assinatura para continuar usando o {{site.data.keyword.Bluemix_notm}}. No entanto, o {{site.data.keyword.Bluemix_notm}} ainda fornece abonos grátis para a maioria
das estruturas e dos serviços de tempo de execução, mesmo se você converter para uma conta de pagamento. Você não é cobrado pelo
{{site.data.keyword.Bluemix_notm}} a menos que o uso esteja além dos
abonos grátis.

O {{site.data.keyword.Bluemix_notm}} fornece
um estimador e uma calculadora para você ver o custo de seu app. É possível ver o custo de seu app das maneiras a seguir:

  * No painel, clique em seu app. Em seguida, na página Visão geral, clique em **estimar o custo deste app** para ver o preço de tempo de execução e suporte do **SDK for Node.js** e o preço mensal total de seu app.

  * Ou, na página Folha de precificação, digite o uso mensal do tempo de execução e serviços de seu app. Por exemplo, 3 instâncias de **SDK for Node.js** com 1 GB
de memória para cada instância. O preço mensal é calculado e exibido.

Também é possível calcular seu custo de app manualmente, somando os
preços de seus tempos de execução e serviços e deduzindo o abono grátis. Para obter mais informações, consulte Calculando seus custos manualmente.

## Removendo apps
{: #ee_removing}

À medida que os apps são construídos, a cota pode se aproximar do limite. No entanto, alguns apps que você
talvez não use mais ainda ocupam a cota. É fácil excluir apps para liberar alguns espaços no
{{site.data.keyword.Bluemix_notm}} a qualquer momento.

Na interface com o usuário do {{site.data.keyword.Bluemix_notm}}, acesse a página Visão geral do app, clique no ícone **Menu** e exclua o app que você não usa mais. Também é possível usar o comando **cf delete**
para excluir apps.
