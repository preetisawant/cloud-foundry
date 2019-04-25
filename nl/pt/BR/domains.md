---

copyright:
  years: 2018
lastupdated: "2019-01-25"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}


# Gerenciando os domínios
{: #domains}

[Aprenda sobre domínios](https://docs.cloudfoundry.org/devguide/deploy-apps/routes-domains.html){: new_window} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo") e como eles trabalham no Cloud Foundry.

Há dois tipos de domínios do Cloud Foundry:
* Domínios compartilhados disponíveis para qualquer aplicativo em qualquer espaço dentro do {{site.data.keyword.cfee_full_notm}}.  Para acessar os domínios compartilhados, acesse a página **Domínios** na área de janela de
navegação esquerda da IU (em *Operações*).
* Domínios privados disponíveis apenas para aplicativos e espaços dentro de uma organização específica.  Para
acessar os domínios dentro de uma organização, acesse a página **Organizações** na área de
janela de navegação esquerda da IU, abra a organização e acesse a guia **Domínios**.

## Criando e excluindo os domínios
{: #create-domains}

Para criar domínios compartilhados, acesse **Domínios** na área de janela de navegação
esquerda do {{site.data.keyword.cfee_full_notm}}.  

Para criar um domínio privado, acesse a página **Organizações** na área de janela de
navegação esquerda da IU, abra a organização e acesse a guia **Domínios**.

Na página _Domínios_ (para domínios compartilhados) ou na guia _Domínios_ de
uma organização específica (para domínios privados), clique em **Criar domínio** para criar um domínio e insira um nome exclusivo.

**Nota:** os nomes de domínio devem ser exclusivos em todo o escopo do {{site.data.keyword.cfee_full_notm}}.  Ou seja, um domínio privado não pode tomar o nome de nenhum domínio compartilhado ou privado dentro de um determinado {{site.data.keyword.cfee_full_notm}}

Também é possível criar um domínio compartilhado por meio da CLI do Cloud Foundry emitindo o comando a
seguir:
  ```
  cf create-shared-domain <domain name>
  ```
  {: pre}
  
É possível criar um domínio privado por meio da CLI do Cloud Foundry emitindo o comando a seguir:
  ```
  cf create-domain my-org <domain name>
  ```
  {: pre}
  
**Nota:** os domínios criados por meio da CLI do Cloud Foundry serão refletidos na IU
imediatamente, mas podem levar até 1 hora para se tornarem efetivos.

Para excluir um domínio, acesse o menu localizado na extremidade direita da linha da tabela correspondente ao
domínio que deseja excluir e selecione **Excluir domínio**.
  
Também é possível excluir um domínio compartilhado da CLI do Cloud Foundry emitindo o comando a seguir:
  ```
  cf delete-shared-domain <domain name>
  ```
  {: pre}  
  
  ```
  cf delete-domain my-org <domain name>
  ```
  {: pre}
  
 
 ## Fazendo upload de certificados SSL
 {: #upload-certificates}
 
É possível fazer upload de um certificado SSL para um domínio (compartilhado ou privado). Clique em **Upload** na linha da tabela correspondente ao domínio para o qual o certificado está sendo incluído,
selecione o arquivo que contém o certificado e o arquivo que contém a chave privada.
  
