---



copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-01-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Hospedando apps no {{site.data.keyword.Bluemix_notm}}
{: #hosting_apps}

Com o {{site.data.keyword.Bluemix}}, é possível criar apps e hospedar seus apps existentes. É possível mover seu app para o {{site.data.keyword.Bluemix_notm}} desde que ele esteja pronto para nuvem. O {{site.data.keyword.Bluemix_notm}} fornece muitas maneiras de você executar seus apps, por exemplo, Cloud Foundry, IBM Containers e Máquinas virtuais.

## Tornando seus apps prontos para nuvem
{: #cloud-readyapps}

Se todos os princípios a seguir forem observados em seu app, o app estará pronto para nuvem e poderá ser migrado para o {{site.data.keyword.Bluemix_notm}}. Se um princípio for violado em seu aplicativo, geralmente será possível [modificar seu aplicativo](../apps/cloud-ready.html) para aderir aos princípios.

## Migrando seus apps
{: #ht_hostapp}

É possível migrar os seus apps para {{site.data.keyword.Bluemix_notm}} incrementalmente, em vez de deslocar o app completamente para o ambiente de nuvem. É possível migrar uma parte de seu app primeiro e conectar-se aos dados existentes ou sistema de registros usando o serviço Cloud Integration.

Em seu apps em nuvem, você pode precisar acessar os dados ou serviços de backend, por exemplo, um sistema de registro. No {{site.data.keyword.Bluemix_notm}}, é possível usar o serviço Secure Gateway para estabelecer um túnel seguro entre uma organização do {{site.data.keyword.Bluemix_notm}} e a rede de backend corporativa. O serviço permite que os apps no {{site.data.keyword.Bluemix_notm}} acessem os dados e serviços da rede de backend. Para obter detalhes, consulte [Atingindo o backend corporativo com o {{site.data.keyword.Bluemix_notm}} Secure Gateway por meio do console ![Ícone de link externo](../icons/launch-glyph.svg)](https://developer.ibm.com/bluemix/2015/04/01/reaching-enterprise-backend-bluemix-secure-gateway/){: new_window}.

Para implementar seu aplicativo no {{site.data.keyword.Bluemix_notm}} como um aplicativo Cloud Foundry, selecione um tempo de execução no catálogo do {{site.data.keyword.Bluemix_notm}}. O tempo de execução contém um app iniciador Hello World que pode ser substituído por seu próprio app. Se não for possível localizar um iniciador que forneça o tempo de execução desejado, será possível trazer um buildpack customizado compatível com Cloud Foundry para o {{site.data.keyword.Bluemix_notm}} usando a opção –b com o comando cf push. Para obter detalhes, consulte [Usando buildpacks da comunidade](byob.html).

É possível usar as ferramentas e serviços a seguir que o {{site.data.keyword.Bluemix_notm}} fornece:

| Ferramenta | Método |
|:------|:--------|
| Interface da linha de comandos do Cloud Foundry (cf cli) | Gerencie seu código no cliente local e usar a interface da linha de comandos do Cloud Foundry para enviar por push seu app para o {{site.data.keyword.Bluemix_notm}} manualmente. Para obter mais informações, consulte [Fazendo upload de seus apps](../starters/upload_app.html). |
| Eclipse | Gerencie seu código no Eclipse e use o IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} para enviar por push seu app. |
| Integração Git | Gerencie seu código no GitHub e Git integrado no {{site.data.keyword.Bluemix_notm}}. É possível colaborar com outros desenvolvedores. Seu app é implementado no {{site.data.keyword.Bluemix_notm}} automaticamente quando você confirma as mudanças no código. Você não precisa enviar por push o app manualmente. |
| {{site.data.keyword.Bluemix_notm}} DevOps Delivery Pipeline | Gerencie seu código no repositório DevOps GitHub e implemente o app no {{site.data.keyword.Bluemix_notm}} usando o DevOps Delivery Pipeline. |
{: caption="Tabela 1. Ferramentas do {{site.data.keyword.Bluemix_notm}}" caption-side="top"}

Se a plataforma Cloud Foundry não suportar seus requisitos de app, será possível usar um contêiner ou VM no qual o tempo de execução é configurado e mantido com mais opções customizadas.

## Desenvolvendo e implementando seus apps usando cadeias de ferramentas no Continuous Delivery
{:ht_cd}

Inclua uma [cadeia de ferramentas em seu app](/docs/services/ContinuousDelivery/toolchains_working.html#creating_a_toolchain_from_an_app) e, em seguida, use a [UI da cadeia de ferramentas do Continuous Delivery](/docs/services/ContinuousDelivery/toolchains_using.html#toolchains-using) para desenvolver e implementar seu app.

## Fazendo upload de apps usando cf cli
{: #ht_cfcli}

É possível gerenciar seu código no cliente local e usar a interface da linha de comandos do Cloud Foundry para fazer upload de seu app para o {{site.data.keyword.Bluemix_notm}} manualmente. Se você muda o código, deve-se enviar por push o app para o {{site.data.keyword.Bluemix_notm}} novamente para executar o código atualizado.

Execute as etapas a seguir para migrar seu app:

Instale a interface de linha de comandos do Cloud Foundry. Assegure-se
de usar a versão mais recente da interface da linha de comandos cf.
  1. Faça download do programa de instalação para seu sistema operacional.
  2. Siga o assistente de ferramenta para instalar a linha de comandos.
  3. Use o comando a seguir para verificar a versão da interface de linha de comandos cf: `cf -v`

Opcional: se você desejar especificar e salvar os detalhes da implementação antes de enviar por push um app para o {{site.data.keyword.Bluemix_notm}}, será possível incluir o manifest do app executando as etapas a seguir:

  1. Acesse o diretório ativo de seu app e crie um arquivo intitulado manifest.yml, que é o nome padrão.</li>
  2. Especifique detalhes da implementação no arquivo manifest. O exemplo a seguir mostra um arquivo manifest para um app Java™.

  ```
  applications:
  - disk_quota: 1024M
  host: myjavatest
  name: MyJavaTest
  path: webStarterApp.war
  domain: mybluemix.net
  instances: 1
  memory: 512M
  ```

Para obter mais informações sobre as opções suportadas que podem ser usadas nesse arquivo, veja [Manifest do app](depapps.html#appmanifest).

### Envie seu app por push

É possível fazer upload de seu aplicativo usando o comando `cf push`.
  1. Conecte e efetue login no {{site.data.keyword.Bluemix_notm}} executando o seguinte comando. Selecione sua organização e espaço
quando solicitado.
  ```
  cf login -a https://api.ng.bluemix.net
  ```
  Inclua a sinalização `-sso` se sua organização usar a Conexão única.

  2. De seu diretório de aplicativos, insira o comando cf push com o nome do app. O nome do
app deve ser exclusivo no ambiente do {{site.data.keyword.Bluemix_notm}}.

  ```
  cf push appname
  ```

  3. Opcional: se você usar um buildpack externo, deverá usar a opção -b com o comando cf push. Por exemplo:

  ```
  cf push appname -b buildpack_URL
  ```

  Consulte [Usando buildpacks da comunidade](byob.html) para obter detalhes.

Opcional: se você mudar seu aplicativo, faça upload dessas mudanças inserindo o `comando cf push` novamente. A interface da linha de comandos cf usa as opções anteriores e suas respostas aos prompts para atualizar quaisquer instâncias em execução de seu app com os novos bits de código.

#### Notas:

* Ao usar o comando cf push, a interface de linha de comandos cf copia todos os arquivos e diretórios de seu diretório atual para o {{site.data.keyword.Bluemix_notm}}. Assegure-se de que você tenha somente os arquivos necessários em seu diretório de aplicativos.
* Assegure-se de que sua organização tenha memória suficiente para todas as instâncias de seu app. Para visualizar a cota de memória de sua organização, use cf org org_name.
* Para obter mais informações sobre cf push, consulte [Comandos cf](../cli/reference/cfcommands/index.html).

## Migrando seus dados e usando serviços
{: #ht_service}

Depois de fazer upload de seu app para o {{site.data.keyword.Bluemix_notm}}, selecione o serviço ao qual seu app está conectado no catálogo do {{site.data.keyword.Bluemix_notm}}, crie uma instância de serviço, vincule a instância ao seu app e, em seguida, reinicie o app.

A variável de ambiente VCAP_SERVICES de seu app é um objeto JSON que contém informações sobre como interagir com uma instância de serviço no {{site.data.keyword.Bluemix_notm}}. As informações incluem o nome da instância de serviço, credenciais e a URL de conexão com a instância de serviço.

Para executar o código no {{site.data.keyword.Bluemix_notm}}, deve-se incluir a lógica de código para analisar a variável VCAP_SERVICES, a fim de obter informações sobre a conexão de serviços. Modifique seu app para obter o host e a porta designados dinamicamente da instância de serviço por meio das variáveis de ambiente. O exemplo a seguir mostra como obter as credenciais de uma instância de serviço do Postgre SQL em um app Ruby:

```
services = JSON.parse(ENV['VCAP_SERVICES'], :symbolize_names => true)
        url = services.values.map do |srvs|
          srvs.map do |srv|
            if srv[:credentials][:uri] =~ /^postgres/
              srv[:credentials][:uri]
            else
              []
            end
          end
        end.flatten!.first
```
{:codeblock}

Para assegurar que seu app possa ser executado em um ambiente local depois de modificar o app para o {{site.data.keyword.Bluemix_notm}}, verifique a presença da variável de ambiente VCAP_SERVICES, a qual está configurada para todos os apps {{site.data.keyword.Bluemix_notm}} Cloud Foundry.


# Links Relacionados
{: #rellinks}

## Links Relacionados
{: #general}

* [{{site.data.keyword.containershort_notm}}](/docs/containers/container_index.html)
* [Virtual Machines](/docs/virtualmachines/vm_index.html)
* [Introdução ao pipeline de entrega](/docs/services/DeliveryPipeline/index.html)
* [Implementando apps com IBM Eclipse Tools for Bluemix](/docs/manageapps/eclipsetools/eclipsetools.html)
* [O app de 12 fatores ![Ícone de link externo](../icons/launch-glyph.svg)](http://12factor.net/){: new_window}
* [Atingindo o backend corporativo com o Bluemix Secure Gateway por meio do console ![Ícone de link externo](../icons/launch-glyph.svg)](https://developer.ibm.com/bluemix/2015/04/01/reaching-enterprise-backend-bluemix-secure-gateway/){: new_window}
