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

# Depurando o stager indisponível
{: #unavailable_stager}

Este tutorial mostra como depurar um stager indisponível em seu {{site.data.keyword.cfee_full}} (CFEE).

## Entendendo os componentes
{: #stager_components}

O {{site.data.keyword.Bluemix_notm}} Bulletin Board System (BBS) é executado no modo ativo ou passivo e mantém um bloqueio no Locket para assegurar que apenas um BBS esteja ativo. Às vezes, se o Locket perder a conexão com o banco de dados de back-end, o BSS poderá ser executado em um estado não responsivo. Nesse caso, nenhum BBS ativo será eleito, a API do BBS não será acessível e operações como `cf push` falharão, uma vez que o Cloud Controller não poderá se comunicar com a API do BBS.
No CFEE v2.0 e acima, o Diego BBS e o Locket são executados no pod diego-api-x, de modo que os usuários precisam reiniciar todos os pods diego-api-x para trazerem o ambiente de volta.

## Impacto
{: #stager_impact}

A API do Diego BBS não é acessível. Os usuários não podem executar `cf push app` e a preparação do aplicativo do CF falha com um erro `Stager is unavailable`, como abaixo:

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

## Como corrigir
{: #stager_howtofix}

A mensagem de erro `Stager está indisponível`geralmente significa que o Cloud Controller tem problemas para se comunicar com a API Diego BBS.
Siga estas etapas para confirmar se o problema relatado é o mesmo com este caso.
Caso afirmativo, continue a recuperar o ambiente.

1. Certifique-se de que o Cloud Controller esteja disponível verificando o status do pod api-x.

    ```
    kubectl get pod -n cf
    ```
    {: pre}

2. Por exemplo, a saída indica que 2 pods api-x estão em execução:
    ```
    NAME                            READY   STATUS      RESTARTS   AGE
    api-0                           2/2     Running     0          1d
    api-1                           2/2     Running     0          1d
    ```

3. Acesse o pod api-0.

    ```
    kubectl exec -ti api-0 bash -n cf
    ```
    {: pre}

4. No pod api-0, se você obtiver um erro como abaixo, ele indicará que o Cloud Controller não pode acessar o BBS.
    ```
    nc -zv diego-api.cf.svc.cluster.local 8889

    ```
    {: pre}

    - Por exemplo, a saída indica que a conexão falhou:
    ```
    nc: connect to diego-api.cf.svc.cluster.local port 8889 (tcp) failed: Connection timed out
    ```

5. Saia da api-0 e, em seguida, exclua todos os pods diego-api-x como abaixo. O Kubernetes recriará todos eles automaticamente.

    ```
    kubectl delete pod diego-api-0 -n cf
    ```
    {: pre}

    Antes do CFEE 2.0, os Diego Lockets estão localizados em pods separados denominados diego-locket-x. Se esse for o caso, reinicie todos os pods diego-locket-x como a etapa 5.

6. Espere até que todos os pods diego-api-x estejam `running` e prontos para `2/2`. Certifique-se de que um dos pods diego-api-x esteja rotulado como ativo.

    ```
    kubectl get pod -n cf -L skiff-role-active
    ```
    {: pre}

7. Verifique se o Cloud Controller pode acessar a API do BBS como a etapa 3 & etapa 4. Você deverá obter uma saída semelhante como abaixo.

    ```
    api/0:/$ nc -zv diego-api.cf.svc.cluster.local 8889
    A conexão com a porta 8889 diego-api.cf.svc.cluster.local [tcp/*] foi bem-sucedida!
    ```

8. O ambiente deve estar pronto para a preparação do app do CF.
