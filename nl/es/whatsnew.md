---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-11-08"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Novedades de IBM Cloud Foundry Enterprise Environment

En este documento se describen las novedades de cada versión comercializada hasta esta fecha del servicio {{site.data.keyword.cfee_full_notm}}.

## Versión 1.1.0
{: #v101}

_Fecha de lanzamiento:_ 16-11-2018

Se han realizado los siguientes cambios en la versión 1.1.0 del servicio {{site.data.keyword.cfee_full_notm}}:

* Nuevas prestaciones:
   * [Actualización](https://console.bluemix.net/docs/cloud-foundry/updating-scaling.html#update-scale#update) de una instancia de CFEE a una nueva versión.
   * [Escalado](https://console.bluemix.net/docs/cloud-foundry/updating-scaling.html#update-scale#scale) de la capacidad de una instancia de CFEE mediante la adición o supresión de células de Cloud Foundry.
   * [Auditoría](https://console.bluemix.net/docs/cloud-foundry/auditing-logging.html#auditing-logging#auditing) de las actividades de Cloud Foundry mediante la integración con una instancia de servicio de IBM Cloud Activity Tracker que se configura automáticamente.
   * Conservación de forma permanente de los [sucesos de registro](https://console.bluemix.net/docs/cloud-foundry/auditing-logging.html#auditing-logging#logging) de Cloud Foundry mediante una instancia de servicio de IBM Cloud Log Analysis que se configura automáticamente.
   * Nuevos [mandatos](https://console.bluemix.net/docs/cloud-foundry/permissions.html#permissions#permcli-creating) `ibmcloud cfee` para recuperar y establecer permisos para crear instancias de CFEE. Los mandatos agregan y simplifican el establecimiento de permisos para el servicio CFEE y para los servicios de soporte necesarios.
   * Nuevo mandato `ibmcloud catalog blacklist` para simplificar el [control de la visibilidad](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#workingwith-services#service_visibility) de los servicios de IBM Cloud para los usuarios de una cuenta de IBM Cloud.

* Problemas resueltos:
   *  Problema resuelto: error intermitente al acceder a las métricas de células
   
Vea una demostración de las novedades de CFEE v1.1.0 en este [vídeo breve](https://ibm.biz/CFEE-V110){: new_window} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo").

Encontrará otros vídeos sobre diversos temas de CFEE en la [ lista de reproducción de vídeos de CFEE ](https://ibm.biz/CFEE-Playlist){: new_window}![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo").
