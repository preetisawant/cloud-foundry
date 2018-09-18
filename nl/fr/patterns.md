---

copyright:

  years: 2015, 2018
lastupdated: "2018-04-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Présentation structurelle
{: #patterns}

Pour que votre projet aboutisse, prenez le temps de planifier et concevoir les ressources dont vous avez besoin et les exigences de votre entreprise. Pour vous aider à démarrer, tenez compte des questions suivantes :
{:shortdesc}

* Combien d'applications, et de quel type, allez-vous développer ?
* A quels services ces applications doivent-elles accéder ?
* Qui participe au processus de développement et quel est leur rôle ?
* Quel est le niveau d'isolement requis pour chaque phase du projet ?
* Les ressources d'infrastructure sont-elles fournies par votre entreprise ?
* De quelle manière votre société communique-t-elle ?
* Existe-t-il une norme de dénomination que vous pouvez implémenter pour identifier clairement l'utilisation de l'organisation et de l'espace ?

Lorsque vous déterminez le type d'environnement de cloud dont vous avez besoin, planifiez la structure de votre compte, de vos organisations, de vos espaces, de vos ressources et des membres de votre équipe.

Pour la plupart des entreprises, un seul compte {{site.data.keyword.Bluemix_notm}} suffit. Pour les entreprises de grande taille, comprenant plusieurs domaines métier, vous souhaiterez peut-être disposer d'un compte {{site.data.keyword.Bluemix_notm}} distinct pour chacun d'eux. Par exemple, une compagnie bancaire de grande taille peut disposer de comptes distincts pour le secteur de la vente au détail et le secteur commercial.

Le tableau suivant fournit un récapitulatif de certains des éléments clés.

| Elément   | Description |
|-----------|---------------|
|| Contient une ou plusieurs organisations. Vous devez disposer d'un compte de type Paiement à la carte pour créer plusieurs organisations. |
|| Ne peut posséder qu'un seul compte. |
|| Peut ajouter un ou plusieurs responsables d'organisation afin de déléguer la gestion de l'organisation, ce qui inclut les droits d'accès en lecture et en écriture aux organisations. |
|| Peut être un membre d'équipe dans des organisations et des espaces dans d'autres comptes {{site.data.keyword.Bluemix_notm}}. |
| Organisation   | Contient un ou plusieurs espaces. |
|| Contient un ou plusieurs responsables d'organisation. |
|| Contient un ou plusieurs membres d'équipe. Chaque membre d'équipe peut se voir accorder un ou plusieurs rôles. |
|| Les frais d'utilisation, générés par une application déployée dans un espace, sont signalés au niveau de l'organisation. |
| Espace   | Contient une ou plusieurs ressources. |
|| Contient une ou plusieurs applications. |
|| Contient un ou plusieurs responsables d'espace. |
|| Contient un ou plusieurs membres d'équipe. Chaque utilisateur doit déjà être un membre d'équipe dans l'organisation propriétaire. Chaque membre d'équipe peut se voir accorder un ou plusieurs rôles. |
| Membre d'équipe   | Peut être ajouté à une ou plusieurs organisations et à un ou plusieurs espaces sur différents comptes. |
|| Peut se voir accorder plusieurs rôles au sein d'une même organisation et/ou d'un même espace. |
{:caption="Tableau 1. Description des éléments clés" caption-side="top"}

