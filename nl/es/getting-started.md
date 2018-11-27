---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-08"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Guía de aprendizaje de iniciación
{: #getting-started}

{{site.data.keyword.cfee_full}} es una plataforma en la nube para alojar apps y servicios en la nube. {{site.data.keyword.cfee_full_notm}} facilita el escalado de apps a medida que aumenta el consumo, simplificando el tiempo de ejecución, el middleware y la infraestructura para que pueda centrarse en desarrollar apps.
{: shortdesc}

Esta guía de aprendizaje de iniciación muestra cómo crear un {{site.data.keyword.cfee_full_notm}}, añadir usuarios, crear una organización y espacios, desplegar apps y enlazar dichas apps a servicios.

## Introducción a los permisos
{: #permissions}

Para trabajar con instancias de {{site.data.keyword.cfee_full_notm}}, los usuarios de servicio deben disponer de los permisos adecuados. Para
obtener más información, consulte [Permisos](https://console.bluemix.net/docs/cloud-foundry/permissions.html).

## Paso 1: Cómo asegurar que la cuenta de {{site.data.keyword.Bluemix_notm}} puede crear recursos de infraestructura
{: #accountprep-environment}

Las instancias de CFEE se despliegan en recursos de infraestructura, que son nodos de trabajo de Kubernetes del servicio de Kubernetes.  [Prepare su cuenta de IBM Cloud](https://console.bluemix.net/docs/cloud-foundry/prepare-account.html) para garantizar que puede crear los recursos de infraestructura necesarios para una instancia de CFEE.

## Paso 2: Creación de su instancia de CFEE
{: #creating-environment}

Antes de crear su CFEE, asegúrese de que está utilizando la cuenta de {{site.data.keyword.Bluemix_notm}} en la que desea crear el entorno y de que dispone de las políticas de acceso necesarias (en el paso 1 anterior).

1.  Abra el catálogo de {{site.data.keyword.Bluemix_notm}} [](https://console.bluemix.net/catalog).

2.  Localice el servicio de {{site.data.keyword.cfee_full_notm}} en el catálogo y púlselo para abrir la página de visión general del servicio.

3.  La primera página de la página de creación proporciona un resumen de las características principales del servicio. Pulse **Continuar**.

4.  Configure la instancia de CFEE que se debe crear proporcionando lo siguiente:
    * Seleccione un plan (la disponibilidad de plan puede estar restringida durante la beta).
    * Escriba un **Nombre** para la instancia de servicio.
    * Seleccione una **Ubicación** en la que debe suministrarse la instancia de servicio. Consulte la lista de [ubicaciones de suministro y centros de datos disponibles](https://console.bluemix.net/docs/cloud-foundry/index.html#provisioning-targets){: new_window} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo") por geografía para los servicios de soporte y CFEE. 
    * Seleccione el **Número de células** para el entorno de Cloud Foundry.
    * Seleccione el **Tipo de máquina**, que determina el tamaño de las células de Cloud Foundry (CPU y memoria).
    * Seleccione un **Grupo de recursos** en el que se agrupa el entorno. Únicamente se listarán en el desplegable _Grupos de recursos_ los grupos de recursos a los que tiene acceso en la cuenta de IBM Cloud actual, lo que significa que necesita permisos para acceder como mínimo a un grupo de recursos en la cuenta para poder crear un CFEE.

5.  En los campos **Compose for PostgreSQL**, seleccione una de las organizaciones públicas y, a continuación, seleccione uno de los espacios disponibles en dicha organización. La instancia de Compose for PostgreSQL se suministrará en el espacio seleccionado. El servicio de Compose for PostgreSQL es una dependencia necesaria del servicio CFEE

**Nota:** Sólo las organizaciones de la ubicación en la que tiene la intención de suministrar la instancia CFEE (paso 4 anterior) y a las que tiene acceso están disponibles para su selección.  Dentro de una organización específica, solo los espacios a los que tiene acceso de _ desarrollador _ están disponibles para la selección. 

6.  De forma opcional, abra la sección **Infraestructura** para ver las propiedades del clúster de Kubernetes que ofrecen soporte a la instancia de CFEE. Tenga en cuenta que el **número de nodos de trabajador** es igual al número de celdas más 2 (dos de los nodos de trabajador de Kubernetes suministrados ofrecen soporte al plano de control de CFEE).
El clúster de Kubernetes en el que se ha desplegado el entorno aparece en el panel de control de {{site.data.keyword.Bluemix_notm}} [](https://console.bluemix.net/dashboard/apps/). Para obtener más información, consulte la documentación de [Servicio de Kubernetes](https://console.bluemix.net/docs/containers/cs_why.html#cs_ov).

** Nota:** Recomendamos que se habilite la expansión de VLAN si los nodos de trabajo del clúster de Kubernetes se suministran en subredes diferentes.  Los nodos de trabajo en distintas subredes pueden impedir la conectividad entre ellos, si la expansión de VLAN está inhabilitada.  Consulte la documentación de [expansión de VLAN](https://console.bluemix.net/docs/containers/cs_subnets.html#vlan-spanning) para obtener más información.

7.  El **Resumen del pedido** en la parte derecha de la página refleja el coste de la instancia CFEE y los servicios auxiliares junto con el total mensual estimado.

8.  Haga clic en **Crear**, lo que abre el panel de control del entorno y muestra el estado y el progreso de creación.

9.  Una vez iniciado el suministro, el entorno se muestra en el panel de control de {{site.data.keyword.Bluemix_notm}}, además de en el [panel de control de Cloud Foundry Environments](https://console.bluemix.net/dashboard/cloudfoundry?filter=cf_environments).  El estado indica cuándo se completa el suministro.

El proceso automatizado que crea el entorno despliega la infraestructura en un clúster de Kubernetes y la configura para que se pueda utilizar. El proceso tarda de 90 a 120 minutos.

Una vez que haya creado correctamente el entorno, recibirá varios correos electrónicos confirmando el suministro de los servicios de CFEE y soporte, así como correos electrónicos en los que se notificará el estado de los pedidos correspondientes.

## Paso 3: Creación de organizaciones y espacios

Después de crear el {{site.data.keyword.cfee_full_notm}}, consulte [Creación de organizaciones y espacios](https://console.bluemix.net/docs/cloud-foundry/orgs-spaces.html) para obtener información sobre cómo estructurar el entorno creando organizaciones y espacios. Las apps de {{site.data.keyword.cfee_full_notm}} abarcan espacios específicos. A su vez, el espacio existe en una organización específica. Los miembros de una organización comparten un plan de cuotas, apps, instancias de servicio y dominios personalizados.

**Nota:** La página _Organizaciones de Cloud Foundry_ disponible desde el menú **_Gestionar > Cuenta > Organizaciones de Cloud Foundry _** ubicado en la cabecera de IBM Cloud superior está destinado únicamente a organizaciones de IBM Cloud públicas, **no a organizaciones de CFEE**. Las organizaciones de CFEE se gestionan en la página _Organizaciones_ de una instancia de CFEE.  Abra la interfaz de usuario de CFEE y pulse en la página **_Organizaciones_** para crear y gestionar organizaciones para el CFEE.

## Paso 4: Adición de usuarios a organizaciones y espacios

[Añada usuarios](https://console.bluemix.net/docs/cloud-foundry/add-users.html) a las organizaciones y espacios con asignaciones de roles específicos controlando su nivel de acceso.  Antes de poder añadir a los usuarios como miembros de organizaciones y espacios en un CFEE, los usuarios deben tener acceso previo a la instancia de CFEE. Consulte [Permisos](https://console.bluemix.net/docs/cloud-foundry/permissions.html).

## Paso 5: Despliegue y visualización de aplicaciones

Cuando esté listo, puede [desplegar la app](https://console.bluemix.net/docs/cloud-foundry/deploy-apps.html) con la interfaz de línea de mandatos de {{site.data.keyword.Bluemix_notm}}.  Visualice la lista de aplicaciones desplegadas en la interfaz de usuario, en el contexto de un espacio de CFEE específico o de forma global en todas las instancias de CFEE.  También puede iniciar, detener o suprimir las aplicaciones de dichas vistas.

## Paso 6: Cómo trabajar con servicios

Las funciones [Crear servicios](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#creating-services_inspace) o [Añadir servicios existentes](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#adding-services_inspace) se encuentran disponibles en la cuenta de IBM Cloud.  Cuando se encuentre disponible una instancia de servicio en un espacio CFEE, puede enlazarla a las aplicaciones CFEE desplegadas en dicho espacio.

## Paso 7: Enlace de aplicaciones a instancias de servicio

[Enlace su app](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#bind_services) al alias de una instancia de servicio para poder utilizar las funciones del servicio.

¿Conocía el [ panel de control de Cloud Foundry ](https://console.bluemix.net/dashboard/cloudfoundry/overview)? Aquí puede ver una vista consolidada de todas las aplicaciones y servicios de {{site.data.keyword.Bluemix_notm}}, tanto _ públicos_ como _ Enterprise _ (CFEE).  Una vez en el panel de control de Cloud Foundry, pulse _Público_ en el panel de navegación de la izquierda para ver las aplicaciones y servicios públicos disponibles en la cuenta de IBM Cloud.  Pulse en _Enterprise_ para ver todos los entornos de CFEE, aplicaciones desplegadas en espacios de CFEE y servicios disponibles en espacios de CFEE.
{:tip}

## Paso 8: Instalación de Stratos Console para gestionar aplicaciones (opcional)

Stratos Console es una herramienta basada en web de código abierto para trabajar con Cloud Foundry. La aplicación Stratos Console se puede instalar de forma opcional y utilizarse en un entorno de CFEE específico para gestionar sus organizaciones, espacios y aplicaciones.

Los usuarios con roles de administrador o editor de IBM Cloud en la instancia de CFEE pueden instalar la aplicación Stratos Console en dicha instancia de CFEE.

Para instalar la aplicación Stratos Console:

1. Abra la instancia de CFEE en la que desea instalar Stratos Console.
2. Pulse **Instalar Stratos Console** en la página de visión general. El botón está visible únicamente para los usuarios con permisos de administrador o editor en la instancia de CFEE.
3. En el diálogo Instalar Stratos Console, seleccione una opción de instalación. Puede instalar la aplicación Stratos Console en el plano de control de CFEE o en una de las células. Seleccione una versión de Stratos console y el número de instancias de la aplicación a instalar. Si instala la app Stratos Console en una célula, se le solicitará que proporcione una organización y espacio en los que desplegar la aplicación.
4. Pulse **Instalar**.

La instalación de la aplicación tarda 5 minutos aproximadamente. Una vez completada la instalación, aparecerá el botón de **Stratos Console** en lugar del botón _Instalar Stratos Console_ en la página de visión general. El botón _Stratos Console_ inicia la consola y está disponible para todos los usuarios con acceso a la instancia de CFEE. Es posible que las asignaciones de pertenencia a un espacio y organización limiten lo que un usuario puede ver y gestionar en Stratos Console.

Para iniciar Stratos Console:

1. Abra la instancia de CFEE en la que se ha instalado Stratos Console.
2. Pulse **Stratos Console** en la página de visión general.
3. Stratos Console se abre en un separador del navegador distinto. Cuando abre la consola por primera vez, se le solicita que acepte dos avisos consecutivos debido a certificados autofirmados.
4. Pulse **Iniciar sesión** para abrir la consola. No se necesitan credenciales puesto que la aplicación utiliza sus credenciales de {{site.data.keyword.Bluemix_notm}}.

La información sobre la API CFEE está disponible en la [ documentación de API ](https://console.bluemix.net/apidocs/cfaas){: new_window} de CFEE ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo").
{:tip}


## Recursos adicionales
{: #additional-resources}

Puede realizar algunas tareas de administración en CFEE con los mandatos de CLI `ibmcloud CFEE`. Los mandatos le permiten obtener información sobre una instancia de CFEE, así como gestionar sus organizaciones y espacios. Revise la [Consulta de mandatos de CFEE de CLI de IBM Cloud](https://console.cloud.ibm.com/docs/cli/reference/ibmcloud/cli_cfee.html#ibmcloud_commands_cfee){: new_window} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo").

Encontrará vídeos y explicaciones y demostraciones exhaustivas sobre diversos temas de CFEE en la [lista de reproducciones de vídeos de CFEE](https://ibm.biz/CFEE-Playlist){: new_window} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo").

Encontrará información sobre las API de CFEE en la [documentación de API](https://console.stage1.bluemix.net/apidocs/cfaas){: new_window} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo").
