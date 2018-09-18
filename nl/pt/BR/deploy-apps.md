---

copyright:
  years: 2018
lastupdated: "2018-07-17"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Implementando e visualizando apps
{: #deploy_apps}

É possível implementar aplicativos para {{site.data.keyword.Bluemix}} com a interface da linha de comandos ou os ambientes de desenvolvimento integrados (IDEs). É possível também usar manifests do aplicativo para
implementar aplicativos. Ao usar um manifest do aplicativo, você reduz o número de detalhes de implementação que deverão ser especificados sempre que implementar um aplicativo no {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## Implementando aplicativos com o comando Cloud Foundry
{: #dep_apps}

Faça download e instale a interface da linha de comandos do {{site.data.keyword.Bluemix}}. [Faça download da CLI do {{site.data.keyword.Bluemix_notm}}](https://clis.ng.bluemix.net){: new_window} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo").

Depois de instalar a interface da linha de comandos, siga estas etapas:

1. Mude para o diretório no qual o seu código está localizado. ` cd <your_directory>`
2. Acesse a página Visão geral do {{site.data.keyword.cfee_full}} e localize o terminal de API do ambiente.
3. Na interface da linha de comandos, configure o terminal de API para o terminal do seu ambiente:

  ```
  cf api <api_enpoint>
  ```
  {: pre}

4. Efetue login no ambiente do

  ```
  cf login -u <username> -o <org_name> -s <space_name>
  ```
  {: pre}

  Se você estiver usando um ID federado, use a opção `-sso`.

  ```
  cf login -o <org_name> -s <space_name> -sso
  ```
  {: pre}

  **Nota**: deve-se incluir aspas simples ou duplas ao redor de `username`, `org_name` e `space_name` se o valor incluir um espaço, por exemplo, `-o "my org"`.

5.  De  `<your_new_directory>`, reimplemente seu app no {{site.data.keyword.Bluemix_notm}} usando o comando `bluemix app push`. Para obter mais informações sobre o comando `cf app push`, consulte [Fazendo upload de seu aplicativo](/docs/starters/upload_app.html).

  ```
  cf push <app_name>
  ```
  {: pre}

6.  Acesse seu app navegando para `https://<app_url>.<AppDomainName>`.

## Visualizando aplicativos implementados na interface com o usuário
{: #view_apps}

É possível visualizar aplicativos implementados do CFEE no contexto de um espaço específico ou globalmente em todas as instâncias do CFEE.

### Visualizando aplicativos implementados em um espaço específico do CFEE
{: #view_specific}

Para visualizar aplicativos implementados em um espaço específico de uma instância específica do CFEE:
1. Acesse o [painel do {{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/dashboard/apps/) e abra o {{site.data.keyword.cfee_full_notm}} no qual você deseja criar organizações.
2. Na interface com o usuário do {{site.data.keyword.cfee_full_notm}}, acesse a entrada **Organizações** na área de janela de navegação para abrir a página _organizações_.
3. Acesse a guia **Espaços** na parte superior da página.
4. Na guia __Espaços__, clique em um espaço na tabela para abrir a página do espaço.
5. Na página __Espaço__, acesse a guia **Aplicativos**.
6. A guia __Applications_)_ mostra todos os aplicativos implementados nesse espaço.
Opcionalmente, é possível Iniciar, Reiniciar, Parar ou Excluir um aplicativo acessando o menu na extrema direita da linha que representa o aplicativo.

Também é possível expandir a linha para um aplicativo para visualizar as instâncias de serviço às quais o aplicativo está ligado.

### Visualizando aplicativos implementados em todas as instâncias do CFEE
{: #view_global}

Para visualizar todos os aplicativos implementados em todas as instâncias do CFEE:
1. Clique no ícone de Menu ![Verificação de conta](img/HamburgerMenu.png "Captura de tela que mostra o ícone de menu") > **Cloud Foundry** para abrir o painel do Cloud Foundry.
2. Clique em **Corporativo > Aplicativos** na área de janela de navegação esquerda.
A tabela na visualização mostra as informações a seguir:

| Elemento   | Descrição |
|-----------|---------------|
| Nome | O nome do aplicativo. |
| Instâncias | O número de instâncias do aplicativo. |
| Ambiente | O ambiente do {{site.data.keyword.cfee_full}} no qual o aplicativo é implementado. |
| Organização | A organização na qual o aplicativo é implementado. |
| Espaço | A organização na instância do CFEE na qual o alias reside. |
| Memória | A quantia de memória usada pelo aplicativo. |
| Status | O status do aplicativo. |
{:caption="Tabela 1. Descrição dos elementos-chave" caption-side="top"}

Opcionalmente, é possível Iniciar, Reiniciar, Parar ou Excluir um aplicativo acessando o menu na extrema direita da linha que representa o aplicativo.
É possível clicar em qualquer um dos aplicativos, ambientes, organizações ou espaços para navegar para a página correspondente na interface com o usuário do CFEE.

Nessa visualização, você tem a opção de agrupar aplicativos por organização, espaço e/ou nome do aplicativo. Esse recurso permite unir em uma única entidade os aplicativos que podem ter nomes diferentes e/ou ser implementados em diferentes organizações ou espaços do CFEE, mas que correspondem à mesma entidade de aplicativo lógico. Por exemplo, você pode ter aplicativos diferentes que representam componentes de um projeto mais amplo ou que são implementados em estágios de entrega diferentes (por exemplo, desenvolvimento, teste, produção), mas que você gostaria de visualizar agrupados como parte da mesma entidade lógica.

Para agrupar aplicativos, acesse a lista suspensa **Grupo** localizada na parte superior da página.
Quando você agrupa aplicativos, cada grupo resultante é representado por uma única entrada na tabela. É possível expandir essa linha para mostrar os aplicativos sob esse grupo.

É possível executar as ações a seguir nessa visualização:
* Classifique os itens na tabela por qualquer uma das propriedades exibidas como colunas da tabela.
* Ligue os aplicativos a um alias específico acessando o menu overflow do alias localizado na extrema direita da linha.
* Expanda um alias (linha) para ver todos os aplicativos ligados a esse alias.
* Inicie, pare aplicativos acessando o menu overflow do aplicativo do alias localizado na extrema direita da linha.
* Navegue até um CFEE, uma organização do CFEE ou um espaço do CFEE clicando no link com o CFEE, a organização ou o espaço correspondente.

## Manifest do aplicativo
{: #appmanifest}

Os manifests do aplicativo incluem opções que são aplicadas ao comando `cf push`. É possível usar um manifest do aplicativo para reduzir o
número de detalhes de implementação que deve-se especificar toda vez que enviar por push
um aplicativo para o {{site.data.keyword.Bluemix_notm}}.

Em manifests do aplicativo, é possível especificar opções como o número de instâncias do aplicativo a serem criadas, a quantia de memória e a cota do disco a serem alocadas e outras variáveis de ambiente. É
possível também usar manifests do aplicativo para automatizar implementações de
aplicativos. O nome padrão de um arquivo manifest é `manifest.yml`.

### Opções Suportadas no Arquivo de Manifesto

A tabela a seguir mostra as opções suportadas que é possível usar em um arquivo
manifest do aplicativo. Se você optar por usar um nome de arquivo diferente de
`manifest.yml`, deve-se usar a opção **-f** com o comando
`cf push`. No exemplo a seguir, `appManifest.yml` é o
nome do arquivo:

```
cf push -f appManifest.yml
```

| Opções | Descrição | Uso ou exemplo |
|:----------|:--------------|:---------------|
| **buildpack** | A URL ou o nome do buildpack customizado. | `buildpack:` *buildpack_URL* |
| **disk_quota** | A cota do disco que é alocada para um aplicativo. O valor padrão é 1 G. | `disk_quota: 500M` |
| **domain** | O nome de domínio do aplicativo no {{site.data.keyword.Bluemix_notm}}. | `domain:` ng.bluemix.net |
| **host** | O nome do host do aplicativo no {{site.data.keyword.Bluemix_notm}}. Esse valor deve ser exclusivo no ambiente do {{site.data.keyword.Bluemix_notm}}. | `host:` *host_name* |
| **name** | O nome do aplicativo no  {{site.data.keyword.Bluemix_notm}}. Esse valor deve ser exclusivo no ambiente do {{site.data.keyword.Bluemix_notm}}. | `name:` *appname* |
| **path** | O local de seu aplicativo. Esse valor pode ser um caminho relativo ou um caminho absoluto. | `path:` *path_to_application* |
| **command** | O comando inicial customizado para seu aplicativo ou o comando para executar arquivos de script. | `command:` *custom_command* `command:` *bash ./run.sh* |
| **memory** | A quantia de memória a ser alocada para o aplicativo. O valor padrão é 1G. | `memory: 512M` |
| **instances** | O número de instâncias a serem criadas para seu aplicativo. | `instances: 2` |
| **timeout** | O período máximo de tempo em segundos usado para iniciar o aplicativo. O valor padrão é 60 segundos. | `timeout: 80` |
| **no-route** | Um valor booleano para evitar que uma rota seja designada ao aplicativo se ele estiver sendo executado apenas em segundo plano. O valor padrão é  ** false **. | `no-route: true` |
| **random-route** | Um valor booleano para designar uma rota aleatória para o aplicativo. O valor padrão é  ** false **. | `random-route: true` |
| **services** | Os serviços a serem ligados ao aplicativo. | `services: - mysql_maptest` |
| **env** | As variáveis de ambiente customizadas do aplicativo. | `env: DEV_ENV: production` |
{: caption="Tabela 2. Opções suportadas no arquivo YAML de manifest" caption-side="top"}

### Um arquivo manifest.yml de amostra
{: #sample}

O exemplo a seguir mostra um arquivo manifest para um aplicativo Node.js que usa
o buildpack do Node.js da comunidade integrada no
{{site.data.keyword.Bluemix_notm}}.

```
---
- name: myNodejsapp
  memory: 256M
  disk_quota: 512M
  path: /dev/myNodejsApp
  buildpack: nodejs_buildpack
  host: nodejs001
  domain: mybluemix.net
  command: node app.js
  timeout: 80
  services:
  - mongo_8917
  env:
    env_type: production
```
{: codeblock}
