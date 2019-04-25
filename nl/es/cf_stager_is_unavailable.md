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

# Depuración de transferencias no disponibles
{: #unavailable_stager}

En esta guía de aprendizaje se muestra cómo solucionar el problema de transferencias no disponibles en {{site.data.keyword.cfee_full}} (CFEE).

## Visión general de los componentes
{: #stager_components}

El sistema de tablón de anuncios (BBS) de {{site.data.keyword.Bluemix_notm}} se ejecuta en modalidad activa o pasiva y mantiene un bloqueo sobre Locket para garantizar que solo BBS está activo. A veces, si Locket pierde la conexión con la base de datos de fondo, BSS puede dejar de responder. En este caso, no se ha seleccionado ningún BBS activo, no se puede acceder a la API de BBS y operaciones como `cf push` fallan porque no se pueden comunicar con la API de BBS.
En CFEE v2.0 y superiores, Diego BBS y Locket se ejecutan en el pod diego-api-x, de modo que los usuarios tienen que reiniciar todos los pods diego-api-x para volver a activar el entorno.

## Impacto
{: #stager_impact}

No se puede acceder a la API de Diego BBS. Los usuarios no pueden ejecutar `cf push app` y la transferencia de aplicaciones CF falla con el error `Stager is unavailable` (Transferencia no disponible), como en el siguiente ejemplo:

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

## Cómo solucionarlo
{: #stager_howtofix}

El mensaje de error `Stager is unavailable` suele significar que Cloud Controller tiene problemas para comunicarse con la API de Diego BBS.
Siga estos pasos para confirmar si el problema notificado se ajusta a este caso.
Si es así, continúe para recuperar el entorno.

1. Asegúrese de que Cloud Controller está disponible comprobando el estado del pod api-x.

    ```
    kubectl get pod -n cf
    ```
    {: pre}

2. Por ejemplo, la salida indica que 2 pods api-x se están ejecutando:
    ```
    NAME                            READY   STATUS      RESTARTS   AGE
    api-0                           2/2     Running     0          1d
    api-1                           2/2     Running     0          1d
    ```

3. Vaya al pod api-0.

    ```
    kubectl exec -ti api-0 bash -n cf
    ```
    {: pre}

4. En el pod api-0, si recibe un error como el siguiente, significa que Cloud Controller no puede acceder a BBS.
    ```
    nc -zv diego-api.cf.svc.cluster.local 8889

    ```
    {: pre}

    - Por ejemplo, la salida indica que la conexión ha fallado:
    ```
    nc: connect to diego-api.cf.svc.cluster.local port 8889 (tcp) failed: Connection timed out
    ```

5. Salga de api-0 y suprima todos los pods diego-api-x, como en el siguiente ejemplo. Kubernetes volverá a crearlos todos automáticamente.

    ```
    kubectl delete pod diego-api-0 -n cf
    ```
    {: pre}

    Antes de CFEE 2.0, Diego Lockets se encontraban en distintos pods llamados diego-locket-x. Si este es su caso, reinicie todos los pods diego-locket-x como en el paso 5.

6. Espere hasta que todos los pods diego-api-x estén en estado `running` y listos para `2/2`. Asegúrese de que uno de los pods diego-api-x esté etiquetado como activo.

    ```
    kubectl get pod  -n cf -L skiff-role-active
    ```
    {: pre}

7. Compruebe si Cloud puede acceder a la API de BBS como en el paso 3 y 4. Debería ver una salida parecida a la siguiente.

    ```
    api/0:/$ nc -zv diego-api.cf.svc.cluster.local 8889
    Connection to diego-api.cf.svc.cluster.local 8889 port [tcp/*] succeeded!
    ```

8. El entorno debería estar preparado para la transferencia de apps CF.
