---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-01-18"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Usando buildpacks da comunidade
{: #using_buildpacks}

Se não for possível localizar um iniciador no catálogo do {{site.data.keyword.Bluemix}} que forneça o tempo de execução desejado, será possível trazer um buildpack externo para o {{site.data.keyword.Bluemix_notm}}. É possível especificar um buildpack customizado e compatível com Cloud Foundry ao implementar o app usando o comando cf push.
{:shortdesc}

A comunidade Cloud Foundry fornece buildpacks externos para
que você use como seus próprios buildpacks. Antes de
implementar o app no {{site.data.keyword.Bluemix_notm}},
certifique-se de instalar a interface de linha de comandos cf.

**Nota:** os buildpacks externos não são fornecidos pela IBM. Entre em contato com a comunidade do Cloud Foundry para suporte.

## Buildpacks integrados da comunidade

No {{site.data.keyword.Bluemix_notm}},
é possível usar os buildpacks integrados que são fornecidos pela comunidade do
Cloud Foundry. Para consultar os buildpacks integrados da comunidade, execute o comando `cf
buildpacks`:

```
cf buildpacks
Obtendo buildpacks...

buildpack      position   enabled   locked   filename
...
java_buildpack     7      true      false    buildpack_java_v2.0.2.zip
ruby_buildpack     8      true      false    buildpack_ruby_v46-245-g2fc4ad8.zip
nodejs_buildpack   9      true      false    buildpack_nodejs_v8-177-g2b0a5cf.zip
```
{:screen}


Para obter o mesmo tempo de execução ou estrutura, os buildpacks criados pela IBM têm precedência sobre os da comunidade. Para usar o buildpack da comunidade para sobrescrever o buildpack criado pela IBM, deve-se especificar o buildpack usando a opção -b com o comando cf push.
Por exemplo, é possível usar o buildpack da comunidade para apps Java™ da web:

```
cf push app_name -b java_buildpack -p app_path
```
{:pre}

Também é possível usar o buildpack da comunidade para o app Node.js:

```
cf push app_name -b nodejs_buildpack -p app_path
```
{:pre}

Para um tempo de execução ou uma estrutura não suportados por buildpacks criados pela IBM, mas suportados pelos buildpacks integrados da comunidade, não é necessário usar a opção -b com o comando cf push. Por exemplo, para apps Ruby, não há buildpacks criados pela IBM. É possível
usar o buildpack integrado da comunidade inserindo o comando a seguir:

```
cf push app_name -p app_path
```
{:pre}

## Buildpacks externos

É possível usar buildpacks externos ou customizados no {{site.data.keyword.Bluemix_notm}}. Deve-se especificar a URL do buildpack com a opção -b e especificar a pilha com a opção
`-s` no comando **cf push**. Por exemplo, para usar um buildpack de comunidade externo para arquivos estáticos, execute o comando a seguir

```
cf push app_name -p app_path -b https://github.com/cloudfoundry/staticfile-buildpack.git
```
{:pre}

Se você não desejar usar o buildpack integrado da comunidade para apps Ruby, será possível usar um buildpack externo inserindo o comando a seguir:

```
cf push app_name -p app_path -b https://github.com/cloudfoundry/ruby-buildpack.git
```
{:pre}

Também é
possível usar um buildpack customizado para seu aplicativo. Por exemplo, para usar um buildback PHP de software livre fornecido pela comunidade Cloud Foundry, ao implementar o app PHP no Bluemix, insira o comando a seguir para especificar a URL do repositório Git do buildpack:

```
cf push app_name -p app_path -b https://github.com/cloudfoundry/php-buildpack.git
```
{:pre}

Também é possível editar o arquivo `manifest.yml` de seu projeto para incluir uma linha `buildpack`:

```
buildpack: https://github.com/cloudfoundry/python-buildpack.git
```
{:pre}


## Especificando a versão do buildpack Java

Use o comando `cf set-env`. Por exemplo, insira o comando a seguir para configurar a versão Java para 1.7.0:
```
cf set-env app_name JBP_CONFIG_OPEN_JDK_JRE &apos;{jre: { version: 1.7.0_+ }}&apos;
```
{:pre}

Em seguida,
remonte seu aplicativo para efetivar a mudança:

```
cf restage app_name
```
{:pre}

Use o arquivo `manifest.yml`. É possível incluir a variável de ambiente
e o valor que deseja especificar diretamente
no arquivo. Para obter informações detalhadas, consulte [Variáveis de ambiente](https://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html#env-block)
