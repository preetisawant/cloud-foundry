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

# Debug di uno stager non disponibile
{: #unavailable_stager}

Questa esercitazione mostra come eseguire il debug di uno stager non disponibile su {{site.data.keyword.cfee_full}} (CFEE).

## Descrizione dei componenti
{: #stager_components}

Il {{site.data.keyword.Bluemix_notm}} Bulletin Board System (BBS) viene eseguito in modalità attiva o passiva e mantiene un blocco in Locket per garantire che sia attivo solo un BBS. Alcune volte, se Locket perde la connessione con il database di backend, BBS può essere eseguito in uno stato senza risposta. In questo caso, non viene scelto alcun BBS attivo, l'API BBS non è accessibile e le operazioni come `cf push` avranno esito negativo perché il controller cloud non può comunicare con l'API BBS.
In CFEE v2.0 e superiore, Diego BBS e Locket vengono eseguiti nel pod diego-api-x, pertanto gli utenti devono riavviare tutti i pod diego-api-x per ripristinare l'ambiente.

## Impatto
{: #stager_impact}

L'API Diego BBS non è accessibile. Gli utenti non possono eseguire `cf push app` e la preparazione dell'applicazione CF ha esito negativo con un errore `Stager is unavailable` come qui di seguito:

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

## Come risolverlo
{: #stager_howtofix}

Il messaggio di errore `Stager is unavailable` normalmente significa che il controller cloud ha riscontrato dei problemi con la comunicazione con l'API Diego BBS.
Segui questa procedura per confermare se il problema riscontrato è lo stesso di questo caso.
Se è così, continua con il ripristino dell'ambiente.

1. Assicurati che il controller cloud sia disponibile controllando lo stato del pod api-x.

    ```
    kubectl get pod -n cf
    ```
    {: pre}

2. Ad esempio, l'output indica che sono in esecuzione 2 pod api-x:
    ```
    NAME                            READY   STATUS      RESTARTS   AGE
    api-0                           2/2     Running     0          1d
    api-1                           2/2     Running     0          1d
    ```

3. Passa al pod api-0.

    ```
    kubectl exec -ti api-0 bash -n cf
    ```
    {: pre}

4. Se nel pod api-0 ricevi un errore simile al seguente, significa che il controller cloud non può accedere a BBS.
    ```
    nc -zv diego-api.cf.svc.cluster.local 8889

    ```
    {: pre}

    - Ad esempio, l'output indica che la connessione non è riuscita:
    ```
    nc: connect to diego-api.cf.svc.cluster.local port 8889 (tcp) failed: Connection timed out
    ```

5. Esci da api-0 ed elimina tutti i pod diego-api-x come segue. Kubernetes li ricreerà tutti automaticamente.

    ```
    kubectl delete pod diego-api-0 -n cf
    ```
    {: pre}

    Prima di CFEE 2.0, i Locket Diego erano ubicati in pod separati denominati diego-locket-x. Se è questo il caso, riavvia tutti i pod diego-locket-x come nel passo 5.

6. Attendi finché tutti i pod diego-api-x siano in esecuzione (`running`) e pronti `2/2`. Assicurati che uno dei pod diego-api-x sia etichettato come attivo.

    ```
    kubectl get pod  -n cf -L skiff-role-active
    ```
    {: pre}

7. Controlla se il controller cloud può accedere all'API BBS come nel passo 3 e 4. Dovresti ricevere un output simile al seguente.

    ```
    api/0:/$ nc -zv diego-api.cf.svc.cluster.local 8889
    Connection to diego-api.cf.svc.cluster.local 8889 port [tcp/*] succeeded!
    ```

8. L'ambiente dovrebbe essere pronto per la preparazione dell'applicazione CF.
