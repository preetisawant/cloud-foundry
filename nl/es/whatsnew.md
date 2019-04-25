---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-04-01"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Novedades de IBM Cloud Foundry Enterprise Environment

En este documento se describen las novedades de cada versión comercializada hasta esta fecha del servicio {{site.data.keyword.cfee_full_notm}}.

## Versión 2.2.0
{: #v220}

_Fecha de lanzamiento:_ 01-04-2019

CFEE v2.2.0 incluye las siguientes versiones de sus componentes:
* Cloud Foundry: v2.7.1.15.5
* Cloud Foundry API: v2.115.0
* Paquetes de compilación de CFEE: v0.1.5
* Servicio IBM Kubernetes: no se proporciona actualización de versión.  **Importante:** Recomendamos actualizar el clúster de CFEE Kubernetes a v1.13 antes de actualizar a CFEE v2.2.0 (obligatorio cuando la instancia de CFEE opera en una red aislada).

Se han realizado los siguientes cambios en la versión 2.2.0 del servicio {{site.data.keyword.cfee_full_notm}}. Para actualizar la versión de CFEE, vaya a la página **Actualizaciones y escalado** en la interfaz de usuario de CFEE y pulse **Actualizar**:

* Nueva opción para **crear** una instancia de CFEE en un clúster de Kubernetes **multizona**. Las instancias de CFEE creadas en un clúster multizona distribuyen las instancias de la aplicación, no solo entre los nodos trabajadores dentro de un centro de datos, sino también entre los centros de datos, lo que hace que las aplicaciones sean más resistentes a las interrupciones de la infraestructura. Además, los CFEE multizona se pueden **escalar** añadiendo células adicionales o eliminando las existentes de las zonas actuales.  Tenga en cuenta que no puede añadir ni eliminar zonas de un CFEE multizona una vez que se ha creado la instancia de CFEE.
* Las instancias de CFEE v2.2.0 ahora pueden [operar dentro de una **red aislada**](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-isolated-network#isolated-network). Tenga en cuenta que si la instancia de CFEE se despliega en las VLAN de una red aislada, algunos puntos finales (direcciones IP) [deben identificarse y direccionarse correctamente](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-isolated-network#oppening-access-points) para que la instancia de CFEE sea operativa. Una instancia de CFEE requiere que un clúster de Kubernetes v1.13 funcione en una red aislada.
* Nueva prestación para enlazar aplicaciones (desplegadas en un espacio de CFEE) con instancias de servicio a través de la red interna de IBM. La prestación permite que se consuman servicios que dan soporte al punto final de servicio de IBM Cloud sin acceder a Internet público.
* Herramientas de **supervisión**:
    * Las herramientas de supervisión (Prometheus, Grafana y Alertmanager) ya no se suministran de forma predeterminada cuando se crea un CFEE.  En CFEE v2.2.0, solo se suministran herramientas de supervisión cuando los administradores de CFEE habilitan esta opción de forma explícita.  Además, cuando están habilitadas, las herramientas de supervisión ya no se suministran en los nodos trabajadores del plano de control de CFEE. Se suministran en sus propios nodos trabajadores, fuera del plano de control. Para habilitar y suministrar herramientas de supervisión, vaya a la página _Supervisión_ de CFEE (en el panel de navegación de la izquierda) y pulse **Habilitar supervisión**. 
    * Cuando se actualiza un CFEE existente a la versión 2.2.0, las herramientas de supervisión existentes se suprimen del plano de control. Se perderá cualquier configuración personalizada existente de las herramientas de supervisión. 
    *  Nueva prestación para sustituir la [configuración de Alertmanager](https://prometheus.io/docs/alerting/configuration/) predeterminada por una configuración personalizada que le permite personalizar el manejo, la agrupación y el direccionamiento de notificaciones de alertas. En la página _Supervisión_ podrá _Descargar_ el archivo de configuración predeterminado y _Cargar_ un archivo de configuración desde el sistema de archivos local.  Puede consultar un [ejemplo](https://github.com/prometheus/alertmanager/blob/master/doc/examples/simple.yml) de archivo de configuración.
* Nueva prestación para etiquetar instancias de CFEE en la {{site.data.keyword.Bluemix_notm}}[_Lista de recursos_](https://cloud.ibm.com/resources) y en la interfaz de usuario de CFEE.
* Mejoras generales en la experiencia del usuario del {{site.data.keyword.Bluemix_notm}}[**panel de control de Cloud Foundry**](https://cloud.ibm.com/dashboard/cloudfoundry/overview). El _panel de control de Cloud Foundry_ muestra vistas globales de instancias de CFEE, aplicaciones y servicios públicos de los que se han creado alias en espacios de CFEE. 

**Nota:** Está disponible un nuevo plan de **presentación técnica de Eirini** cuando se crea una nueva instancia de CFEE. El plan es independiente de la v2.2.0 descrita anteriormente, que se aplica solo al plan _Estándar_.  El plan de presentación técnica de Eirini le permite explorar un CFEE utilizando Kubernetes nativo como planificador de contenedores (en lugar de Diego). Consulte [Iniciación a la presentación técnica de Eirini](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-getting-started-eirini#getting-started-eirini) para obtener más información.

Vea una demostración de las novedades de CFEE v2.1.0 en este [vídeo breve](https://ibm.biz/CFEE-V220){: new_window} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo").


## Versión 2.1.1
{: #v211}

_Fecha de lanzamiento:_ 20-03-2019

Se han realizado los siguientes cambios en la versión 2.1.1 del servicio {{site.data.keyword.cfee_full_notm}}. Para actualizar la versión de CFEE, vaya a la página _Actualizaciones y escalado_ en la interfaz de usuario de CFEE:

* Se han resuelto problemas que impedían un suministro correcto. 


## Versión 2.1.0
{: #v210}

_Fecha de lanzamiento:_ 20-02-2019

**Nota:** Solo se puede actualizar a esta versión desde la versión **2.0.2**. Actualice a la versión 2.0.2 antes de actualizar a la versión v2.1.0.

Se han realizado los siguientes cambios en la versión 2.1.0 del servicio {{site.data.keyword.cfee_full_notm}}. Para actualizar la versión de CFEE, vaya a la página **Actualizaciones y escalado** en la interfaz de usuario de CFEE y pulse **Actualizar**:

* Nueva función de escalado automático que escala automáticamente las instancias de aplicaciones de Cloud Foundry en función de reglas personalizadas. Se puede acceder al escalado automático desde la CLI y desde la consola de Stratos. La consola de Stratos se puede instalar e iniciar de forma opcional desde la página _Visión general_ de la interfaz de usuario de CFEE. En la página _Aplicaciones_ de la consola de Stratos, seleccione una aplicación y busque el separador **Escalado automático**. Pulse *Crear política* para iniciar el editor de escalado automático a fin de definir la política de escalado para la aplicación de destino.
  Consulte la [documentación de escalado automático](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-autoscale_cloud_foundry_apps#autoscale_cloud_foundry_apps) para obtener más información.
* Nueva prestación para gestionar paquetes de compilación desde la interfaz de usuario de CFEE, incluida la posibilidad de arrastrar y soltar un paquete de compilación en la lista de prioridades. La función está disponible en la nueva página **Paquetes de compilación** de la interfaz de usuario de CFEE (no en la consola de Stratos). En el release, solo se pueden añadir o actualizar a través de la interfaz de usuario los archivos zip de paquetes de compilación de 1 MB o menos. Puede cargar los archivos zip de paquetes de compilación de más de 1 MB mediante los mandatos `cf create-buildpack` y `cf update-buildpack`. 
* Nueva prestación para gestionar cuotas de la organización desde la interfaz de usuario, incluida la visualización de las organizaciones que utilizan una determinada cuota. La función está disponible en la nueva página **Cuotas** de la interfaz de usuario de CFEE (no en la consola de Stratos). Puede crear nuevas cuotas y editar las existentes. También puede actualizar los valores de la cuota predeterminada con valores de cualquier cuota existente con la opción **Copiar en valor predeterminado** del menú de la cuota.
* Una nueva página **Iniciación** de la interfaz de usuario guía a los usuarios por las tareas más importantes para configurar y utilizar el entorno.
* Se pueden añadir **etiquetas** a una instancia de CFEE en la lista de recursos de IBM Cloud.  Las etiquetas añadidas a la lista de recursos aparecerán en la cabecera de la página de visión general de CFEE.
* **Cloud Foundry** versión 2.7.21.
* Consola de **Stratos** versión 2.3.0, que incluye un parche de seguridad. Tenga en cuenta que la sola actualización de la versión de CFEE no actualizará la versión de la consola de Stratos. Es necesario suprimir y volver a instalar la consola de Stratos (en la página Visión general de CFEE), lo cual selecciona automáticamente la última versión de la consola de Stratos.
* Los usuarios pueden navegar a la página **Clúster** de Kubernetes de CFEE desde el menú de desbordamiento de la página de visión general de CFEE.

**Nota:** Si actualiza a CFEE v2.1.0 desde una versión v2.0.x, la actualización se lleva a cabo con una sola acción _Actualizar_ que actualiza automáticamente tanto el plano de control como las células en secuencia. Si actualiza desde una versión v1.x.x, la actualización requiere dos acciones _Actualizar_ separadas, una para actualizar el plano de control (primero) y otra para actualizar las células.

Vea una demostración de las novedades de CFEE v2.1.0 en este [vídeo breve](https://ibm.biz/CFEE-V210){: new_window} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo").


## Versión 2.0.2
{: #v202}

_Fecha de lanzamiento:_ 08-02-2019

Se han realizado los siguientes cambios en la versión 2.0.2 del servicio {{site.data.keyword.cfee_full_notm}}. Para actualizar la versión de CFEE, vaya a la página _Actualizaciones y escalado_ en la interfaz de usuario de CFEE:

* Se han resuelto problemas que impedían actualizaciones correctas de versión. Esta versión es un requisito previo para actualizar a la versión **2.1.0**.


## Versión 2.0.1
{: #v201}

_Fecha de lanzamiento:_ 10-01-2019

Se han realizado los siguientes cambios en la versión 2.0.1 del servicio {{site.data.keyword.cfee_full_notm}}. Para actualizar la versión de CFEE, vaya a la página _Actualizaciones y escalado_ en la interfaz de usuario de CFEE:

* Se ha resuelto el problema que impide que los dominios personalizados funcionen correctamente.
* Se ha resuelto el problema por el que las métricas de la organización no están disponibles mientras se recuperan las nuevas métricas.


## Versión 2.0.0
{: #v200}

_Fecha de lanzamiento:_ 13-12-2018

Se han realizado los siguientes cambios en la versión 2.0.0 del servicio {{site.data.keyword.cfee_full_notm}}. Para actualizar la versión de CFEE, vaya a la página _Actualizaciones y escalado_ en la interfaz de usuario de CFEE:

* Se ha mejorado la resiliencia de actualizaciones de versión de CFEE.
* Se ha mejorado la disponibilidad operativa y la resiliencia de las instancias de CFEE.
* Certificados del lado del cliente para un acceso más seguro a las aplicaciones, lo que permite que el servidor otorgue acceso a las aplicaciones solo a los clientes certificados.
* Cuando se crea una instancia de CFEE, el clúster de Kubernetes de soporte y la instancia de servicio de Cloud Object Storage se crean en el mismo grupo de recursos que la instancia de servicio de CFEE (en lugar de crearse bajo el grupo de recursos "Default").
* Parche de seguridad.
* Mejoras en la CLI `ibmcloud cfee`:
    * Nuevos mandatos para crear una instancia de servicio de IBM Cloud desde un espacio de CFEE y para añadirla a dicho espacio de CFEE (`ibmcloud cfee service-create`, `ibmcloud cfee service-alias-create`).
    * Nuevos mandatos para escalar la capacidad de CFEE (`ibmcloud cfee scale-up`, `ibmcloud cfee scale-down`).
    * Mejoras en el mandato para gestionar instancias de CFEE (`ibmcloud cfee environments`).
    
      Actualización de la CLI ibmcloud (`ibmcloud update`) para acceder a estas mejoras de mandatos; ejecute `ibmcloud cfee -help` para obtener más información.
      
**Nota**: para actualizar una instancia de CFEE a la versión 2.0.0 solo se necesita una sola acción _update_ que actualiza tanto el plano de control como las células. No se necesitan actualizaciones separadas para el plano de control de CFEE y las células.


## Versión 1.1.2
{: #v112}

_Fecha de lanzamiento:_ 07-12-2018

Se han realizado los siguientes cambios en la versión 1.1.2 del servicio {{site.data.keyword.cfee_full_notm}}:
* Nuevos centros de datos en Chennai (che01) y Milán (mil01) disponibles para suministrar instancias de CFEE.
* Parche de seguridad.

## Versión 1.1.1
{: #v111}

_Fecha de lanzamiento:_ 28-11-2018

Se han realizado los siguientes cambios en la versión 1.1.1 del servicio {{site.data.keyword.cfee_full_notm}}:
* Parche de seguridad.
   
## Versión 1.1.0
{: #v110}

_Fecha de lanzamiento:_ 16-11-2018

Se han realizado los siguientes cambios en la versión 1.1.0 del servicio {{site.data.keyword.cfee_full_notm}}:

* Nuevas prestaciones:
   * Las instancias de CFEE se pueden suministrar en los nodos trabajadores de Kubernetes de [dedicados virtuales](https://console.bluemix.net/docs/containers/cs_clusters.html#clusters#clusters_ui_standard) alojados en la infraestructura que se dedica a su cuenta de IBM Cloud.
   * Se dispone de un nuevo centro de datos en Tokio (tok05) para el suministro de instancias de CFEE.
   * [Actualización](https://console.bluemix.net/docs/cloud-foundry/updating-scaling.html#update-scale#update) de una instancia de CFEE a una nueva versión.
   * [Escalado](https://console.bluemix.net/docs/cloud-foundry/updating-scaling.html#update-scale#scale) de la capacidad de una instancia de CFEE mediante la adición o supresión de células de Cloud Foundry.
   * [Auditoría](https://console.bluemix.net/docs/cloud-foundry/auditing-logging.html#auditing-logging#auditing) de las actividades de Cloud Foundry mediante la integración con una instancia de servicio de IBM Cloud Activity Tracker que se configura automáticamente.
   * Conservación de forma permanente de los [sucesos de registro](https://console.bluemix.net/docs/cloud-foundry/auditing-logging.html#auditing-logging#logging) de Cloud Foundry mediante una instancia de servicio de IBM Cloud Log Analysis que se configura automáticamente.
   * Vista de comprobación de estado que indica el estado operativo de los componentes de CFEE.
   * Nuevos mandatos para llevar a cabo acciones relacionadas con CFEE en la interfaz de línea de mandatos (CLI):
     * Mandatos `ibmcloud cfee create`, `ibmcloud cfee create-locations` e `ibmcloud cfee create-status` para crear instancias de CFEE desde la interfaz de línea de mandatos, obtener una lista de los centros de datos disponibles en los que se puede suministrar un CFEE y comprobar el estado de suministro de un CFEE creado.
     * [Mandatos](https://console.bluemix.net/docs/cloud-foundry/permissions.html#permissions#permcli-creating) `ibmcloud cfee create-permission-get` e `ibmcloud cfee create-permission-set` para recuperar y establecer los permisos necesarios para crear  instancias de CFEE. Los mandatos agregan y simplifican el establecimiento de permisos para el servicio CFEE y para los servicios de soporte necesarios.
     * Mandato `ibmcloud catalog blacklist` para simplificar el [control de la visibilidad](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#workingwith-services#service_visibility) de los servicios de IBM Cloud para los usuarios de una cuenta de IBM Cloud.

* Problemas resueltos:
   *  Problema resuelto: error intermitente al acceder a las métricas de células
<br/>   
Vea una demostración de las novedades de CFEE v1.1.0 en este [vídeo breve](https://ibm.biz/CFEE-V110){: new_window} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo").  También encontrará otros vídeos sobre diversos temas de CFEE en la [lista de reproducción de vídeos de CFEE](https://ibm.biz/CFEE-Playlist){: new_window}![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo").
