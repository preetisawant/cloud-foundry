---



copyright:

  years: 2015, 2017

lastupdated: "2017-12-14"

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

Se todos os princípios a seguir forem observados em seu app, o app estará pronto para nuvem e poderá ser migrado para o {{site.data.keyword.Bluemix_notm}}. Se um princípio for violado em seu app, geralmente será possível modificar o app para aderir aos princípios.

* Não codifique seu app diretamente para uma topologia específica.

  Em um ambiente não de nuvem, o app pode usar uma topologia de implementação específica. No entanto, a topologia do app pode ser mudada nos apps em nuvem, pois os apps e serviços prontos para nuvem permitem mudanças imediatas de escalabilidade. As mudanças de escalabilidade incluem ajuste de escala dinâmica e redimensionamento manual do número de instâncias de um app.

  Construa seu app para ser o mais genérico e stateless possível para evitar que seu app seja afetado pelas mudanças de escalabilidade.

* Não assuma que o sistema de arquivos local seja permanente.

  Como uma instância do app pode ser movida, excluída ou duplicada a qualquer momento na nuvem, não confie nos arquivos que são gravados no sistema de arquivos. Se um app usa o sistema de arquivos local como um cache de informações usadas frequentemente, incluindo logs do app, as informações são perdidas quando a instância é encerrada e reiniciada em um local diferente ou uma VM diferente.

  É possível armazenar informações em um serviço, como um banco de dados SQL ou NoSQL em vez do sistema de arquivos local. Em um ambiente de nuvem dinâmica, também é crítico que seus logs estejam disponíveis em um serviço que prolongue as instâncias do app nas quais os logs são gerados.

* Não armazene o estado de sessão em seu app.

  O estado de seu sistema é definido pelos seus bancos de dados e pelo armazenamento compartilhado e não por instância do app individual em execução. O stateful de qualquer classificação limita a escalabilidade de um app. Tente minimizar o impacto do estado da sessão armazenando-a em um local centralizado no servidor.

  Se não for possível eliminar o estado de sessão completamente, envie-o por push para um armazenamento altamente disponível que seja externo ao seu servidor de aplicativos. Os armazenamentos incluem IBM WebSphere Extreme Scale, Redis ou Memcached ou um banco de dados externo.

* Não use dependência de infraestrutura específica.

  Esse é um princípio geral que possui diversas manifestações. Por exemplo, não presuma que os serviços que seu app usa sejam nomes de hosts ou endereços IP específicos alocados. Os serviços podem ser realocados ou regenerados em seu ambiente de nuvem e os nomes de hosts e endereços IP também podem mudar.

  A extração de dependências específicas do ambiente para um conjunto de arquivos de propriedade é uma melhoria, mas ainda é inadequada. A melhor prática é usar um registro de serviço externo para resolver terminais em serviço ou delegar a função de roteamento inteira para um barramento de serviço ou um balanceador de carga com um nome virtual.

* Não use APIs de infraestrutura em seu app.

  Se você conta com uma API de infraestrutura específica em seu app, mudar a infraestrutura é mais desafiador porque uma API de infraestrutura pode referir-se a muitas camadas diferentes em sua pilha de software.

  É possível contar com produtos comerciais ou de software livre existentes e deixar as soluções PaaS na camada PaaS para mantê-las fora do seu código de app.

* Não use protocolos obscuros.

  Não use protocolos obscuros que requeiram configuração extra para resiliência.

  Os apps baseados em protocolos padrão são mais resilientes com os itens de configuração delegados para a plataforma. Os protocolos padrão incluem HTTP, SSL, banco de dados padrão, enfileiramento e conexões de serviço da web.

* Não conte com recursos específicos do S.O.

  Se você já usou recursos específicos do sistema operacional, será possível corrigir esse problema usando bibliotecas de compatibilidade, por exemplo, Cygwin e Mono. Cygwin é uma biblioteca de compatibilidade que fornece um conjunto de ferramentas Linux em um ambiente do Windows. Mono é uma biblioteca de compatibilidade que fornece recursos .NET do Windows no Linux.

  Evite as dependências específicas do sistema operacional; em vez disso, use serviços que sejam fornecidos pela infraestrutura de middleware ou por provedores de serviços.

* Não instale manualmente seu app.

  Seu app pode ser instalado frequentemente sob demanda no ambiente de nuvem dinâmica. O processo de instalação deve ser por script e confiável, e os dados da configuração devem ser exteriorizados a partir dos scripts.

  No mínimo, capture a instalação do app como um conjunto uniforme de scripts que sejam independentes do sistema operacional. Mantenha a instalação do app pequena e móvel para adaptar-se a diferentes técnicas de automação. Além disso, minimize as dependências que são requeridas pela instalação do app.

Para obter mais informações sobre apps prontos para nuvem, veja [O app de 12 fatores ![External link icon](../icons/launch-glyph.svg)](http://12factor.net/){: new_window}.

##Migrando seus apps
{: #ht_hostapp}

É possível migrar seus apps para o {{site.data.keyword.Bluemix_notm}} de uma maneira incremental, em vez de deslocar o app completamente para o ambiente de nuvem. É possível migrar uma parte de seu app primeiro e conectar-se aos dados existentes ou sistema de registros usando o serviço Cloud Integration.

Em seu apps em nuvem, você pode precisar acessar os dados ou serviços de backend, por exemplo, um sistema de registro. No {{site.data.keyword.Bluemix_notm}}, é possível usar o serviço Secure Gateway para estabelecer um túnel seguro entre uma organização do {{site.data.keyword.Bluemix_notm}} e a rede de backend corporativa. O serviço permite que os apps no {{site.data.keyword.Bluemix_notm}} acessem os dados e serviços da rede de backend. Para obter detalhes, veja [Atingindo o backend corporativo com o Bluemix Secure Gateway por meio do console ![Ícone de link externo](../icons/launch-glyph.svg)](https://developer.ibm.com/bluemix/2015/04/01/reaching-enterprise-backend-bluemix-secure-gateway/){: new_window}.

Para implementar seu app no {{site.data.keyword.Bluemix_notm}} como um app Cloud Foundry, selecione um tempo de execução no Catálogo do {{site.data.keyword.Bluemix_notm}}. O tempo de execução contém um app iniciador Hello World que pode ser substituído por seu próprio app. Se não for possível localizar um iniciador que forneça o tempo de execução desejado, será possível trazer um buildpack customizado compatível com Cloud Foundry para o {{site.data.keyword.Bluemix_notm}} usando a opção –b com o comando cf push. Para obter detalhes, consulte [Usando buildpacks da comunidade](/docs/cfapps/byob.html).

É possível usar as ferramentas e serviços a seguir que o {{site.data.keyword.Bluemix_notm}} fornece:

| Ferramenta | Método |
|:------|:--------|
| Interface da linha de comandos do Cloud Foundry (cf cli) | Gerencie seu código no cliente local e usar a interface da linha de comandos do Cloud Foundry para enviar por push seu app para o {{site.data.keyword.Bluemix_notm}} manualmente. Para obter mais informações, consulte [Fazendo upload de seus apps](/docs/starters/upload_app.html). |
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
  1. Faça download do programa de instalação para seu sistema operacional.</li>
  2. Siga o assistente de ferramenta para instalar a linha de comandos.</li>
  3. Use o comando a seguir para verificar a versão da interface de linha de comandos cf: `cf -v`

Opcional: se você desejar especificar e salvar os detalhes da implementação antes de enviar por push um app para o {{site.data.keyword.Bluemix_notm}}, será possível incluir o manifest do app executando as etapas a seguir:
  1. Acesse o diretório ativo de seu app e crie um arquivo intitulado manifest.yml, que é o nome padrão.</li>
  2. Especifique detalhes da implementação no arquivo manifest. O exemplo a seguir mostra um arquivo manifest para um app Java™.
  ```applications:
  - disk_quota: 1024M
  host: myjavatest
  name: MyJavaTest
  path: webStarterApp.war
  domain: mybluemix.net
  instances: 1
  memory: 512M
  ```
  Para obter mais informações sobre as opções suportadas que podem ser usadas nesse arquivo, veja [Manifest do app](../manageapps/depapps.html#appmanifest).

Envie por push seu app. É possível fazer upload de seu app usando o comando cf push.
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
  Veja [Usando buildpacks da comunidade](../cfapps/byob.html) para obter detalhes.

Opcional: se você muda seu app, deve-se fazer upload dessas mudanças inserindo o comando cf push novamente. A interface da linha de comandos cf usa as opções anteriores e suas respostas aos prompts para atualizar quaisquer instâncias em execução de seu app com os novos bits de código.

**Notas:**

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

* [IBM Containers](/docs/containers/container_index.html)
* [Virtual Machines](/docs/virtualmachines/vm_index.html)
* [Introdução ao pipeline de entrega](/docs/services/DeliveryPipeline/index.html)
* [Implementando apps com IBM Eclipse Tools for Bluemix](/docs/manageapps/eclipsetools/eclipsetools.html)
* [O app de 12 fatores ![Ícone de link externo](../icons/launch-glyph.svg)](http://12factor.net/){: new_window}
* [Atingindo o backend corporativo com o Bluemix Secure Gateway por meio do console ![Ícone de link externo](../icons/launch-glyph.svg)](https://developer.ibm.com/bluemix/2015/04/01/reaching-enterprise-backend-bluemix-secure-gateway/){: new_window}
