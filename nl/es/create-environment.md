---

copyright:
  years: 2017, 2018
lastupdated: "2019-04-02"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Creación de un entorno
{: #create-environment}

## Requisitos previos
* Asegúrese de que está en la cuenta de {{site.data.keyword.Bluemix_notm}} en la que desea crear el entorno.
* Asegúrese de que tiene los [permisos](https://cloud.ibm.com/catalog/docs/cloud-foundry/permissions.html) correctos antes de crear instancias de {{site.data.keyword.cfee_full_notm}}. 
* [Prepare su cuenta de IBM Cloud](https://cloud.ibm.com/docs/cloud-foundry/prepare-account.html) para garantizar que puede crear los recursos de infraestructura necesarios para una instancia de CFEE (las instancias de CFEE se despliegan en nodos trabajadores de Kubernetes desde el servicio Kubernetes).  

## Creación de una instancia de CFEE
1.  Abra el catálogo de {{site.data.keyword.Bluemix_notm}} [](https://cloud.ibm.com/catalog).

2.  Localice el servicio {{site.data.keyword.cfee_full_notm}} en el catálogo y púlselo para abrir la página de visión general del servicio.  La primera página contiene un resumen de las características principales del servicio. Pulse **Continuar**.

3.  Configure la instancia de CFEE que se debe crear:
    * Seleccione un plan. Consulte la sección [Presentación técnica de Eirini](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-create-environment#create-environment#eirini) para ver una descripción de las limitaciones de este plan.
    * Escriba un **Nombre** para la instancia de CFEE.
    * Seleccione un **Grupo de recursos** en el que se agrupa el entorno. Únicamente se listarán en el desplegable _Grupos de recursos_ los grupos de recursos a los que tiene acceso en la cuenta de IBM Cloud actual, lo que significa que necesita permisos para acceder como mínimo a un grupo de recursos en la cuenta para poder crear un CFEE.
    * Seleccione la **Geografía** y la **Ubicación** en las que debe suministrarse la instancia de servicio. Consulte la lista de [ubicaciones de suministro y centros de datos disponibles](https://cloud.ibm.com/catalog/docs/cloud-foundry/index.html#provisioning-targets){: new_window} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo") por geografía para los servicios de soporte y CFEE. 

4. Las instancias de CFEE se suministran en un clúster de Kubernetes. Las células de Cloud Foundry se suministran dentro de zonas de nodos trabajadores del clúster de Kubernetes. Puede configurar la ubicación, el hardware y el cifrado del clúster:
    * Seleccione el aislamiento de hardware para el clúster de Kubernetes:   
      * _Virtual compartido_: los recursos de la infraestructura del clúster, como el hipervisor y el hardware físico, se distribuyen entre el cliente y otros clientes de IBM, pero cada uno de los nodos trabajadores es de un único arrendatario.
      * _Virtual dedicado_: los nodos trabajadores del clúster se alojan en una infraestructura está dedicada a su cuenta.
    * Los datos del clúster están cifrados de forma predeterminada. Tiene la opción de desactivar la opción _Cifrar disco local_.
    * Seleccione la **Geografía** y la **Región** donde se suministrará el clúster de Kubernetes.
    * Seleccione las **Zonas** en las que se desplegarán los nodos trabajadores de Kubernetes. Tiene la opción de suministrar los nodos trabajadores en la misma zona (**Una sola zona**) o en varias zonas (**Multizona**).  **Tenga en cuenta** que para crear CFEE multizona se necesita la [expansión de VLAN](https://cloud.ibm.com/docs/containers?topic=containers-subnets#vlan-spanning), que también recibe soporte cuando la cuenta de {{site.data.keyword.Bluemix_notm}} está [habilitada para VRF](https://cloud.ibm.com/docs/infrastructure/direct-link/vrf-on-ibm-cloud.html#overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud).
    
    Las VLAN disponibles se recuperan automáticamente para las zonas seleccionadas. Si no hay VLAN disponibles, se crearán automáticamente.
    
    **Nota: Suministro en una red aislada:** Puede definir como destino de las VLAN una red aislada. Cuando la instancia de CFEE se crea en una red aislada, las políticas de la red aislada (por ejemplo, políticas de calico o reglas de VRA) deben permitir TODO el acceso de salida desde la instancia de CFEE para que la CFEE se suministre correctamente. Una vez que se ha creado CFEE, las restricciones de acceso de salida se pueden volver a establecer, excepto para el acceso de salida a determinados servicios y microservicios de IBM Cloud.  Consulte la documentación sobre [Funcionamiento en una red aislada](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-isolated-network#isolated-network) para obtener más información.
    
    Una vez que se ha creado CFEE, aparecerá el clúster de Kubernetes en el que se suministrará el entorno (como cualquier otro recurso de su cuenta de IBM Cloud) en el {{site.data.keyword.Bluemix_notm}}[panel de control](https://https://cloud.ibm.com/catalog/dashboard/apps/). Para obtener más información, consulte la documentación de [Servicio de Kubernetes](https://https://cloud.ibm.com/catalog/docs/containers/cs_why.html#cs_ov).

5.  Configure la capacidad de CFEE:
    * Seleccione el **Número de células** para CFEE. Se trata de las células de aplicación que alojarán las aplicaciones desplegadas en CFEE.  
    * Seleccione el **Tamaño de nodo**, que determina la capacidad de las células de Cloud Foundry (CPU y memoria).
    
    Además de las células de aplicación que especifique arriba, se crean y se reservan _células de plano de control_ adicionales para el funcionamiento y el control de la plataforma Cloud Foundry en CFEE. 

    **Nota:** Recomendamos que se habilite la expansión de VLAN si los nodos de trabajo del clúster de Kubernetes se suministran en subredes diferentes.  Los nodos de trabajo en distintas subredes pueden impedir la conectividad entre ellos, si la expansión de VLAN está inhabilitada.  Consulte la documentación de [expansión de VLAN](https://cloud.ibm.com/catalog/docs/containers/cs_subnets.html#vlan-spanning) para obtener más información.

6.  En los campos **Compose for PostgreSQL**, seleccione una de las organizaciones públicas y, a continuación, seleccione uno de los espacios disponibles en dicha organización. La instancia de Compose for PostgreSQL se suministrará en el espacio seleccionado. El servicio de Compose for PostgreSQL es una dependencia necesaria del servicio CFEE.

    **Nota:** Bajo _Compose for PostgreSQL_, solo las organizaciones de la ubicación en la que tiene la intención de suministrar la instancia CFEE (paso 4 anterior) y a las que tiene acceso están disponibles para su selección.  Dentro de una organización específica, solo los espacios a los que tiene acceso de _desarrollador_ están disponibles para la selección. 

7.  El **Resumen del pedido** en la parte derecha de la página refleja el coste de la instancia CFEE y los servicios auxiliares junto con el total mensual estimado.

8.  Pulse **Crear**, lo que abre el panel de control del entorno y muestra el estado y el progreso de creación.

**Nota:** Una vez comenzado el proceso de creación, se muestra una fila en la tabla correspondiente a CFEE en el panel de control de {{site.data.keyword.Bluemix_notm}}, en la _Lista de recursos_ y en el [panel de control de Cloud Foundry Environments](https://cloud.ibm.com/dashboard/cloudfoundry?filter=cf_environments).  El estado de la fila de la tabla indica cuándo finaliza la creación.

El proceso automatizado que crea el entorno despliega la infraestructura en un clúster de Kubernetes y la configura para que se pueda utilizar. El proceso tarda de 90 a 120 minutos.

Una vez que se haya creado CFEE, recibirá varios correos electrónicos confirmando el suministro de los servicios de CFEE y soporte, así como correos electrónicos en los que se notificará el estado de los pedidos correspondientes.

Cuando crea una instancia de CFEE, hay tres instancias de servicio de soporte adicionales que se crean en la misma cuenta de IBM Cloud. Estas instancias de servicio de soporte se llaman como la instancia de CFEE. Por lo tanto, la creación de un CFEE da lugar a la creación de un total de cuatro instancias de servicio en la cuenta de IBM Cloud:
* Instancia de CFEE ("_cfeename_").
* Clúster Kubernetes ("_cfeename_-cluster"). El clúster proporciona la infraestructura en la que se suministra la instancia de CFEE.
* Instancia de Cloud Object Storage ("_cfeename_-cos"). La instancia se utiliza para almacenar los datos generados durante la creación de los contenedores de aplicaciones CFEE (por ejemplo, paquetes de aplicaciones cargados, paquetes de compilación y ejecutables compilados).
* Instancia de Compose for PosgreSQL ("_cfeename_-postgres"). La instancia se utiliza para almacenar los datos de Cloud Foundry en la instancia de CFEE (p. ej. la auditoría del despliegue de aplicación, inicio y detención de sucesos; y el mantenimiento de registros de la pertenencia de usuarios de CFEE, organizaciones, espacios, aplicaciones y conexiones de servicio). 

## El plan de presentación técnica de Eirini
{: #eirini}

 El plan de presentación técnica de Eirini le permite explorar un CFEE utilizando Kubernetes nativo como planificador de contenedores (en lugar de Diego). El planificador de Kubernetes se utiliza en CFEE para desplegar y ejecutar apps en el entorno de ejecución de aplicaciones Cloud Foundry, añadir usuarios, crear una organización y espacios, desplegar apps y enlazar esas apps a los servicios. Consulte la documentación del [proyecto Eirini](https://www.cloudfoundry.org/project-eirini/) para obtener más información sobre el proyecto de la incubadora Eirini de Cloud Foundry Foundation.
 Se aplican las limitaciones siguientes a las instancias de CFEE creadas a partir del plan de presentación técnica de Eirini:
 
* No se da soporte a Kubernetes con `containerd`. Solo se da soporte a las versiones de Kubernetes que utilizan Docker en lugar de `containerd`. La versión más reciente de IBM Container Service (IKS) que da soporte a Docker es v1.10.
* No se da soporte a Cloud Foundry SSH.
* No se da soporte al mandato `cf push` de imágenes de Docker.
* No se da soporte a la transferencia (staging) de Erini nativa de Kubernetes. Las instancias de CFEE creadas a partir del plan de presentación técnica de Eirini utilizan Eirini para ejecutar apps, pero no para transferirlas. Se siguen utilizando células de Diego para transferir las apps.
* No se da soporte al reinicio de instancias de app específicas (`cf restart-app-instance`).

 
