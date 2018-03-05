---

copyright:
  years: 2016, 2017, 2018
lastupdated: "2018-01-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Meilleures pratiques pour l'exécution d'applications en production
{: #production}

Cloud Foundry constitue une excellente plateforme pour l'exécution d'applications prêtes pour le cloud dans un environnement de production. Ces meilleures pratiques peuvent faciliter l'exécution d'applications Cloud Foundry en production avec {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## Instances multiples
{: #multiple_instances}

Les applications prêtes pour le cloud sont évolutives horizontalement, et sont de ce fait capables d'ajouter ou de retirer de manière dynamique des instances d'application. Exécutez au moins trois instances de chaque application pour permettre d'éviter une durée d'indisponibilité inattendue en cas d'incidents isolés ou de maintenance de plateforme.

## Options de surveillance
{: #monitoring}

{{site.data.keyword.Bluemix_notm}} simplifie la surveillance de votre application grâce à des services comme [Monitoring and Analytics](/docs/services/monana/index.html) et [New Relic ![Icône de lien externe](../icons/launch-glyph.svg)](http://newrelic.com/){: new_window}. Consultez les [fonctions de journalisation intégrées](../monitor_log/logging.html#logging_for_bluemix_apps) pour plus d'informations.

## Options de support
{: #support}

Le forfait payant {{site.data.keyword.Bluemix_notm}} offre plusieurs autres types de compte avec un support payant *facultatif*.  Quel que soit le type de votre compte, si vous prévoyez de mettre en production une application sur {{site.data.keyword.Bluemix_notm}}, envisagez de vous inscrire à cette option.

Avec ou sans support payant, vous pouvez obtenir de l'aide comme décrit à la rubrique [Comment obtenir l'aide dont j'ai besoin ?](../get-support/howtogetsupport.html), mais payer pour le support vous permettra de vous assurer que vos tickets de demande de service recevront le niveau d'attention qu'ils méritent.
