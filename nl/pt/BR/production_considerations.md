---

copyright:
  years: 2016, 2017, 2018
lastupdated: "2018-01-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Melhores práticas para executar aplicativos em produção
{: #production}

O Cloud Foundry é uma excelente plataforma para executar aplicativos prontos para nuvem em produção. Essas melhores práticas podem ajudar na execução de aplicativos Cloud Foundry de produção com o {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## Múltiplas instâncias
{: #multiple_instances}

Os aplicativos prontos para nuvem são horizontalmente escaláveis e, portanto, podem incluir ou remover dinamicamente instâncias do aplicativo. Execute pelo menos três instâncias de cada aplicativo para ajudar a evitar tempo de inatividade inesperado no caso de incidentes isolados ou de manutenção da plataforma.

## Opções de monitoramento
{: #monitoring}

O {{site.data.keyword.Bluemix_notm}} torna mais fácil monitorar o seu aplicativo com serviços como [Monitoramento e Analytics](/docs/services/monana/index.html) e [New Relic ![Ícone de link externo](../icons/launch-glyph.svg)](http://newrelic.com/){: new_window}. Consulte [Recursos de criação de log integrados](../monitor_log/logging.html#logging_for_bluemix_apps) para obter mais informações.

## Opções de suporte
{: #support}

O plano de precificação pago do {{site.data.keyword.Bluemix_notm}} oferece uma série de tipos de conta diferentes com suporte pago *opcional*.  Não importa o tipo de sua conta, se você planeja trazer um aplicativo para produção no {{site.data.keyword.Bluemix_notm}}, considere a inscrição nesta opção.

Com ou sem suporte pago, é possível obter ajuda conforme descrito em [Como obter o suporte de que preciso?](../get-support/howtogetsupport.html), mas pagar pelo suporte ajudará a assegurar que seus chamados de suporte tenham o nível de atenção que merecem.
