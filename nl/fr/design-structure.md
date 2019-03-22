---

copyright:

  years: 2018
lastupdated: "2018-10-26"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Conception de la structure de votre environnement IBM Cloud Foundry Enterprise Environment
{: #bpimplementation}

Au lieu de la méthodologie de production, de test et de développement traditionnelle strictement définie, vous pouvez implémenter un environnement dans lequel les développeurs et les testeurs peuvent collaborer avec d'autres membres d'équipe. Si vous concevez la façon dont vous voulez développer et distribuer vos applications, créez des espaces qui satisfont cette méthodologie. Au lieu de concevoir votre environnement au niveau de l'organisation (inférieur), pensez à concevoir votre environnement {{site.data.keyword.cfee_full}} (CFEE) au niveau de l'espace (supérieur).

Tenez compte de l'échelle et de la portée des applications que vous prévoyez de développer et déployer. Un espace Cloud Foundry peut être utilisé en tant qu'environnement de développement pour une ou plusieurs applications rigoureusement connectées ou définies. Hormis un espace de développement, par exemple, vous pouvez créer des espaces pour un test unitaire, un test de performance et un test d'intégration. Des espaces peuvent également être définis pour la génération, le transfert et la production. Chacun des espaces que vous créez peut être partagé par différents membres d'équipe au sein d'une même organisation.

Créez des organisations Cloud Foundry distinctes lorsque des personnes travaillent dans différents domaines métier et que leurs activités ne se chevauchent pas. S'il existe deux groupes totalement indépendants, la création d'une organisation pour chacun d'eux définit des limites précises pour la distribution et la gestion des membres d'équipe et des ressources. Vous pouvez définir une API permettant la communication entre les organisations.

Vous pouvez créer des organisations en adéquation avec la façon dont vous voulez travailler plutôt qu'avec la structure au sein d'une société. En général, même s'il arrive que des organisations de société soient modifiées, rien ne peut empêcher la poursuite du développement et de la maintenance d'une application. Concevez votre instance {{site.data.keyword.cfee_full}} pour la durée de vie des applications et non selon la structure d'organisation de votre société.

Un développement et un déploiement itératifs peuvent engendrer une extension rapide des applications. La conception de votre processus de distribution doit pouvoir s'adapter rapidement et facilement. Vous souhaitez bénéficier d'un développement en continu avec un taux de déploiement rapide. Le fait d'avoir des espaces de développement et de production dans la même organisation CFEE permet d'accéder aux mêmes ressources. Le fait de gérer différents espaces au sein d'une même organisation réduit la charge administrative. Le personnel du développement, des tests et des opérations peut collaborer facilement s'il ne travaille pas dans la même organisation CFEE.

Implémentez une norme de dénomination pour identifier clairement l'utilisation de l'organisation et de l'espace. Par exemple, vous pouvez inclure le type de cloud, la région géographique, le type d'utilisation (par exemple, développement, test et production), le nom d'application et le numéro de version ou de révision. Les organisations et les espaces peuvent ensuite être facilement identifiés à des fins d'administration et d'accès.  

Le nombre d'espaces peut croître rapidement dans le cadre d'un développement itératif. Vous pouvez définir autant d'espaces que nécessaire au sein d'une organisation. Si vous prévoyez de définir un grand nombre d'espaces, vous souhaiterez peut-être créer une application dédiée à la gestion des espaces. Pour plus de soixante espaces, vous pouvez envisager de définir une autre organisation.

Chargez une personne de créer et gérer une organisation, de définir les espaces et d'accorder un accès aux membres d'équipe. Une seconde personne peut se voir accorder le même accès pour gérer l'environnement lorsque le responsable de l'organisation n'est pas disponible.  

Identifiez toutes les personnes qui doivent accéder à chaque espace et à chaque organisation. Déterminez leur rôle. Le rôle professionnel d'un membre d'équipe détermine ses droits d'accès. Par exemple, un développeur confirmé doit disposer des droits nécessaires pour visualiser et mettre à jour l'ensemble de l'environnement de développement {{site.data.keyword.cfee_full}}. En revanche, un développeur débutant ne peut visualiser et mettre à jour que la partie de l'environnement de développement qui lui a été affectée.
