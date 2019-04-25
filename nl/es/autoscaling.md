---

copyright:
  years: 2019
lastupdated: "2019-03-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Escalado automático de aplicaciones
{: #autoscale_cloud_foundry_apps}

{{site.data.keyword.Bluemix}} tiene soporte integrado de escalado automático para las aplicaciones de Cloud Foundry para ajustar automáticamente el número de instancias de la aplicación mediante 
  * Escalado dinámico basado en métricas de rendimiento de aplicaciones.
  * Escalado planificado basado en tiempo.

Esta prestación se ofrece en base al proyecto de código abierto de Cloud Foundry [App-Autoscaler][autoscaler_project]. Consulte la [guía de usuario][autoscaler_user_guide] para empezar. 

## Gestión del escalado automático mediante la CLI

Puede utilizar el plugin de la interfaz de línea de mandatos del programa de escalado automático de apps (CLI de AutoScaler) para gestionar políticas, métricas de consulta e historial de escalado. 

### Instalación de la CLI de AutoScaler
Utilice el mandato siguiente para instalar la `CLI de AutoScaler`, que es un plugin de la CLI de Cloud Foundry.  

``` 
cf install-plugin -r CF-Community app-autoscaler-plugin
```
{:codeblock} 

Se puede utilizar el mismo mandato para actualizar el plugin de la `CLI de AutoScaler` a la versión más reciente si tiene una instalación anterior. 

### Utilización de la CLI de AutoScaler

Si ya ha iniciado una sesión en un entorno de Cloud Foundry en {{site.data.keyword.Bluemix}} y tiene aplicaciones que se ejecutan en el espacio tal como se describe en [la guía de despliegue de aplicaciones][deploy_app], siga los pasos siguientes para crear una política de escalado para la aplicación y métricas de consulta e historial de escalado. 

 *  (Opcional) Confirme que el punto final de la API de App-Autoscaler se ha establecido correctamente de forma predeterminada.  

    Si el punto final de la API de Cloud Foundry se presenta como `api.<DOMAIN>`, el punto final de la API de App-Autoscaler debería ser `autoscaler.<DOMAIN>`.  
    Utilice el mandato siguiente para comprobar el valor de punto final de la API de App-Autoescaler.

    ```
    cf asa
    ```
    {:codeblock} 

    Si el punto final de la API de App-Autoscaler es incorrecto, tiene que restablecerlo con este mandato:

    ```
    cf asa autoscaler.<DOMAIN>
    ```
    {:codeblock} 


*  Cree un archivo JSON de política en la máquina local. 

    ```
    cat > <YOUR_POLICY_FILE> << EOF
    {
            "instance_min_count": 1,
            "instance_max_count": 5,
            "scaling_rules": [
                    {
                            "metric_type": "memoryutil",
                            "breach_duration_secs": 120,
                            "threshold": 80,
                            "operator": ">=",
                            "cool_down_secs": 120,
                            "adjustment": "+1"
                    },
                    {
                            "metric_type": "memoryutil",
                            "breach_duration_secs": 120,
                            "threshold": 10,
                            "operator": "<",
                            "cool_down_secs": 120,
                            "adjustment": "-1"
                    }
            ]
    }
    EOF
    ```
    {:codeblock} 

    La política anterior sirve para activar el escalado según la utilización de memoria cuando se incumple el umbral definido durante al menos `120   segundos`.  Consulte la [guía del usuario de App-Autoscaler de Cloud Foundry][autoscaler_user_guide] para ver cómo crear su propia política de escalado automático.

*  Adjunte la política a la aplicación

    ```
    cf aasp <YOUR_APP> <YOUR_POLICY_FILE>
    ```
    {:codeblock} 

*  (Opcional) Además, puede consultar las métricas agregadas más recientes de la aplicación. App-Autoscaler da soporte a varios [tipos de métricas][metric_type], pero solo se pueden recuperar las métricas que ha definido en su política, es decir `memoryutil` en el ejemplo anterior.  

    ```
    cf asm <YOUR_APP> <METRIC_TYPE> --desc
    ```
    {:codeblock} 

*  (Opcional) Utilice el mandato siguiente para consultar el historial de escalado:

    ```
    cf ash <YOUR_APP> --desc
    ```
    {:codeblock} 

    Consulte la [guía del plugin de la CLI de App Autoscaler de Cloud Foundry][autoscaler_cli] para ver más opciones que puede utilizar en la línea de mandatos. 


## Gestión del escalado automático mediante la consola de Stratos 

Además de la interfaz de línea de mandatos, también puede gestionar los valores de escalado automático mediante la consola de Stratos. 

Si ha instalado [stratos][stratos] en su {{site.data.keyword.cfee_full}} (CFEE), vaya al separador **"Escalado automático**" del panel de control de la aplicación para ver una visión general de la política de escalado automático y de los sucesos de escalado más recientes. 
Pulse cualquiera de los iconos de cualquiera de los mosaicos para iniciar el editor de políticas y editar la política.

Si no se ha definido ninguna política de escalado automático, la página de visión general no contendrá información.  Pulse **Crear política** para iniciar el editor de políticas y crear una política.

Le recomendamos que examine la [guía del usuario de App-Autoscaler de Cloud Foundry][autoscaler_user_guide] para comprender los conceptos básicos para definir correctamente una política de escalado automático. 

### Estadísticas de métrica

Cuando haya definido una política basada en uno o varios tipos de métricas seleccionados, puede ver los valores de las métricas más recientes y el historial de métricas de los últimos 30 minutos. 

**Nota:** Las métricas representan datos medios de todas las instancias de la aplicación, no datos sin procesar de cada instancia de la aplicación.
    
### Historial de escalado

El separador **Historial** del editor de políticas muestra las acciones de escalado que se han realizado en la aplicación activadas por la política de escalado automático. También muestra los mensajes de error resultantes de las anomalías de escalado. Puede consultar el historial de escalado de los últimos 30 días. 


[autoscaler_project]: https://github.com/cloudfoundry-incubator/app-autoscaler
[autoscaler_user_guide]: https://github.com/cloudfoundry-incubator/app-autoscaler/blob/master/docs/Readme.md
[autoscaler_cli]: https://github.com/cloudfoundry-incubator/app-autoscaler-cli-plugin#cloud-foundry-cli-autoscaler-plug-in-
[metric_type]: https://github.com/cloudfoundry-incubator/app-autoscaler/blob/master/docs/Readme.md#metric-types
[deploy_app]: https://cloud.ibm.com/docs/cloud-foundry/deploy-apps.html#dep_apps
[stratos]: https://cloud.ibm.com/docs/cloud-foundry/getting-started.html#install-stratos
