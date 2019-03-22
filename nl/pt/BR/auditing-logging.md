---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-11-09"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Auditoria e criação de log
{: #auditing-logging}

Os recursos de auditoria e de criação de log no {{site.data.keyword.cfee_full}} (CFEE) permitem que os
administradores auditem os eventos que ocorrem em uma instância do CFEE e que os desenvolvedores controlem os eventos de
log gerados por meio de seus aplicativos do Cloud Foundry.

A auditoria e a criação de log no CFEE são suportadas por meio da integração com os serviços Log Analysis e
Activity Tracker do IBM Cloud.

## Auditando
{: #auditing}

A auditoria permite que os administradores do CFEE rastreiem as atividades auditáveis do Cloud Foundry que estão
ocorrendo em uma instância do CFEE.  Essas atividades incluem login, criação de organizações e espaços, participação do
usuário e designações de função, implementações de aplicativo, ligações de serviço e configuração de domínio. A
auditoria é suportada por meio da integração com o serviço Activity Tracker no IBM Cloud. Uma instância do serviço
Activity Tracker selecionada pelo administrador do CFEE é configurada automaticamente para receber eventos que
representam ações executadas no Cloud Foundry e no plano de controle do CFEE. O usuário pode ver e
gerenciar esses eventos na interface com o usuário da instância de serviço do Activity Tracker.

Para ativar a auditoria para uma instância do CFEE:

1. Abra uma interface com o usuário do CFEE e a entrada **Operações > Auditoria** na área
de janela de navegação esquerda para abrir a página Criação de log.
2. Clique em **Ativar auditoria** e selecione uma das **Instâncias do
Activity Tracker** disponível na conta do IBM Cloud.  Se nenhuma instância estiver disponível, o usuário verá
uma opção para criar uma nova instância do Activity Tracker no catálogo do IBM Cloud.
3.  Após a ativação da auditoria, os detalhes de configuração serão exibidos na página. Os detalhes incluem o status da configuração e um link para a própria instância de serviço do Activity Tracker, que o usuário pode acessar para ver e gerenciar os eventos de auditoria.

É possível desativar a auditoria clicando em **Desativar auditoria**, que removerá a
instância de serviço do Activity Tracker anteriormente incluída e configurada. Essa ação não exclui a instância de
serviço do Activity Tracker.

## Persistência de criação de log
{: #logging}

A criação de log de eventos do Cloud Foundry é suportada por meio da integração com o serviço Log Analysis no IBM Cloud. Uma instância de serviço do Log Analysis selecionada pelo administrador do CFEE é configurada
automaticamente para receber e persistir os eventos de criação de log do Cloud Foundry gerados por meio da
instância do CFEE.  O usuário pode ver e gerenciar esses eventos de criação de log na interface com o usuário da
instância de serviço do Log Analysis.

Para ativar a criação de log para uma instância do CFEE:

1. Certifique-se de ter uma [política de acesso ao IAM](https://console.bluemix.net/iam/#/users)
que designa a função de editor, de operador ou de administrador para a instância de serviço do Log Analysis na qual você
pretende persistir os eventos de criação de log.
2. Abra uma interface com o usuário do CFEE e a entrada **Operações > Criação de log** na área
de janela de navegação esquerda para abrir a página Criação de log.
3. Clique em **Ativar persistência** e selecione uma das **Instâncias do Log
Analysis** disponíveis na conta do IBM Cloud.  Se nenhuma instância estiver disponível, o usuário verá uma
opção para criar uma instância no catálogo do IBM Cloud.
4. Após a ativação da persistência de criação de log, os detalhes de configuração serão exibidos na página. Os detalhes incluem o status da configuração e um link para a própria instância de serviço do Log Analysis, que o
usuário pode acessar para ver e gerenciar os eventos de criação de log.

**Aviso:** a ativação da persistência de criação de log requer uma reinicialização
disruptiva do plano de controle e das células do CFEE.  Durante a reinicialização, toda a funcionalidade
administrativa estará disponível, mas alguns aplicativos e serviços em execução nessa instância do CFEE podem
ficar indisponíveis.  O status dos componentes do CFEE será refletido na página Verificação de funcionamento durante a
reinicialização.  A reinicialização leva aproximadamente 20 minutos.

É possível desativar a persistência de log clicando em **Desativar a persistência de log**, o
que removerá a instância de serviço anteriormente incluída e configurada. Essa ação não excluirá a instância de serviço
do Log Analysis.

**Nota:** ao desativar a persistência de log, os eventos de criação de log do Cloud
Foundry ainda estão sendo gerados. Eles não são persistidos fora da instância do CFEE.
