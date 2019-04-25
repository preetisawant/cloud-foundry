---

copyright:
  years: 2019
lastupdated: "2019-02-02"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Débogage de stager non disponible
{: #unavailable_stager}

Ce tutoriel montre comment déboguer un stager non disponible sur votre environnement {{site.data.keyword.cfee_full}} (CFEE).

## Description des composants
{: #stager_components}

Le système BBS (Bulletin Board System) d'{{site.data.keyword.Bluemix_notm}} s'exécute en mode actif ou passif et gère un verrou dans Locket afin de garantir qu'un seul système BBS est actif. Parfois, si Locket perd la connexion avec la base de données de back-end, BSS peut s'exécuter sans réponse. Dans ce cas, aucun système BBS n'est retenu, l'API BBS n'est pas accessible et les opérations telles que `cf push` échouent car le contrôleur de cloud ne peut pas communiquer avec l'API BBS.
Dans CFEE version 2.0 et supérieure, Diego BBS et Locket s'exécutent dans le pod diego-api-x. Les utilisateurs doivent donc redémarrer tous les pods diego-api-x pour restaurer l'environnement.

## Impact
{: #stager_impact}

L'API Diego BBS n'est pas accessible. Les utilisateurs ne peuvent pas exécuter de commande `cf push app` et la préproduction d'application CF échoue avec une erreur `Stager is unavailable` comme ci-dessous :

```
    Response code: 503
    CC code:       0
    CC error code:
    Request ID:    xxxxxxx-xxxxx-xxx-xxxx-xxxxxxxx
    Description:   {
    "description": "Stager is unavailable: execution expired",
    "error_code": "CF-StagerUnavailable",
    "code": 170010
    }
    Server error, status code: 503, error code: 170010, message: Stager is unavailable: execution expired
```

## Procédure de résolution du problème
{: #stager_howtofix}

Le message d'erreur `Stager is unavailable` signifie généralement que le contrôleur de cloud rencontre des difficultés pour communiquer avec l'API BBS de Diego.
Procédez comme suit pour vérifier si le problème signalé est identique ici.
Si tel est le cas, continuez à restaurer l'environnement.

1. Assurez-vous que le contrôleur de cloud est disponible en vérifiant le statut du pod api-x.

    ```
    kubectl get pod -n cf
    ```
    {: pre}

2. Par exemple, la sortie indique que les 2 pods api-x s'exécutent :
    ```
    NAME                            READY   STATUS      RESTARTS   AGE
    api-0                           2/2     Running     0          1d
    api-1                           2/2     Running     0          1d
    ```

3. Accédez au pod api-0.

    ```
    kubectl exec -ti api-0 bash -n cf
    ```
    {: pre}

4. Dans le pod api-0, si vous obtenez une erreur telle que celle ci-dessous, cela signifie que le contrôleur de cloud ne peut pas accéder à BBS.
    ```
    nc -zv diego-api.cf.svc.cluster.local 8889

    ```
    {: pre}

    - Par exemple, la sortie indique que la connexion a échoué :
    ```
    nc: connect to diego-api.cf.svc.cluster.local port 8889 (tcp) failed: Connection timed out
    ```

5. Quittez le pod api-0, puis supprimez tous les pods diego-api-x comme ci-dessous. Kubernetes les recréera tous automatiquement.

    ```
    kubectl delete pod diego-api-0 -n cf
    ```
    {: pre}

    Avant CFEE 2.0, Diego Lockets se trouvent dans des pods séparés nommés diego-locket-x. Dans ce cas, redémarrez tous les pods diego-locket-x comme à l'étape 5.

6. Attendez que tous les pods diego-api-x soient à l'état `running` et prêts `2/2`. Assurez-vous que l'un des pods diego-api-x soit indiqué comme actif.

    ```
    kubectl get pod  -n cf -L skiff-role-active
    ```
    {: pre}

7. Vérifiez si le contrôleur de cloud peut accéder à l'API BBS comme à l'étape 3 & et à l'étape 4. Vous devez obtenir une sortie similaire à la suivante.

    ```
    api/0:/$ nc -zv diego-api.cf.svc.cluster.local 8889
    Connection to diego-api.cf.svc.cluster.local 8889 port [tcp/*] succeeded!
    ```

8. L'environnement devrait être prêt pour la préproduction d'application CF.
