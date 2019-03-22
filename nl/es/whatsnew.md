---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-12-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Novedades de IBM Cloud Foundry Enterprise Environment

En este documento se describen las novedades de cada versión comercializada hasta esta fecha del servicio {{site.data.keyword.cfee_full_notm}}.


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
