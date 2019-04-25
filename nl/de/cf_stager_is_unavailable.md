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

# Fehlerbehebung bei nicht verfügbarer Zwischenspeicherungsfunktion
{: #unavailable_stager}

In diesem Lernprogramm wird gezeigt, wie die Fehlerbehebung für eine nicht verfügbare Zwischenspeicherungsfunktion für Ihre Instanz von {{site.data.keyword.cfee_full}} (CFEE) ausgeführt wird. 

## Erläuterungen zu Komponenten
{: #stager_components}

Das {{site.data.keyword.Bluemix_notm}} Bulletin Board System (BBS) wird im aktiven oder passiven Modus ausgeführt und verwaltet eine Sperre in Locket, um sicherzustellen, dass nur ein BBS aktiv ist. Wenn die Verbindung zwischen Locket und der Back-End-Datenbank getrennt wird, antwortet das BBS in manchen Fällen nicht mehr. In diesem Fall ist kein aktives BBS ausgewählt, die BBS-API ist nicht zugänglich und Operationen wie `cf push` schlagen fehl, da Cloud Controller nicht mit der BBS-API kommunizieren kann. In CFEE V2.0 und höher werden Diego BBS und Locket im Pod diego-api-x ausgeführt. Daher müssen Benutzer alle Pods diego-api-x neu starten, um die Umgebung wiederherzustellen. 

## Auswirkung
{: #stager_impact}

Auf die Diego BBS-API kann nicht zugegriffen werden. Benutzer können den Befehl `cf push app` nicht ausführen und die Zwischenspeicherung von CF-Anwendungen schlägt mit einer Fehlernachricht wie `Zwischenspeicherungsfunktion ist nicht verfügbar` fehl, wie unten dargestellt: 

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

## Vorgehensweise zur Fehlerbehebung
{: #stager_howtofix}

Die Fehlernachricht `Zwischenspeicherungsfunktion ist nicht verfügbar` bedeutet in der Regel, dass Probleme bei der Kommunikation von Cloud Controller mit der Diego BBS-API bestehen. Führen Sie die folgenden Schritte aus, um zu überprüfen, ob Ihr Problem mit dem hier beschriebenen Fall übereinstimmt. Ist dies der Fall, fahren Sie fort, um die Umgebung wiederherzustellen. 

1. Stellen Sie sicher, dass Cloud Controller verfügbar ist, indem Sie den Status der Pods api-x überprüfen. 

    ```
    kubectl get pod -n cf
    ```
    {: pre}

2. Die Ausgabe zeigt beispielsweise an, dass 2 Pods api-x aktiv sind:
    ```
    NAME                            READY   STATUS      RESTARTS   AGE
    api-0                           2/2     Running     0          1d
    api-1                           2/2     Running     0          1d
    ```

3. Wechseln Sie zum Pod api-0. 

    ```
    kubectl exec -ti api-0 bash -n cf
    ```
    {: pre}

4. Wenn im Pod api-0 ein Fehler wie der folgende ausgegeben wird, bedeutet dies, dass Cloud Controller nicht auf das BBS zugreifen kann.
    ```
    nc -zv diego-api.cf.svc.cluster.local 8889

    ```
    {: pre}

    - Die Ausgabe gibt beispielsweise an, dass die Verbindung fehlgeschlagen ist:
    ```
    nc: connect to diego-api.cf.svc.cluster.local port 8889 (tcp) failed: Connection timed out
    ```

5. Verlassen Sie api-0 und löschen Sie anschließend alle Pods diego-api-x mit dem folgenden Befehl. Kubernetes erstellt alle Pods automatisch neu. 

    ```
    kubectl delete pod diego-api-0 -n cf
    ```
    {: pre}

    In Versionen vor CFEE 2.0 befinden sich Diego Lockets in separaten Pods mit dem Namen diego-locket-x. Ist dies der Fall, starten Sie alle Pods diego-locket-x wie in Schritt 5 angegeben erneut. 

6. Warten Sie, bis alle Pods diego-api-x den Status `running` haben und `2/2` bereit sind. Stellen Sie sicher, dass einer der Pods diego-api-x als aktiv gekennzeichnet ist. 

    ```
    kubectl get pod  -n cf -L skiff-role-active
    ```
    {: pre}

7. Überprüfen Sie wie in Schritt 3 & Schritt 4 angegeben, ob Cloud Controller auf die BBS-API zugreifen kann. Die Ausgabe sollte ähnlich wie die folgende aussehen. 

    ```
    api/0:/$ nc -zv diego-api.cf.svc.cluster.local 8889
    Connection to diego-api.cf.svc.cluster.local 8889 port [tcp/*] succeeded!
    ```

8. Die Umgebung müsste für das Staging von CF-Apps bereit sein. 
