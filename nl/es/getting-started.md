---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-12"

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
obtener más información, consulte [Permisos](/docs/cloud-foundry/permissions.html).

## Paso 1: Cómo asegurar que la cuenta de {{site.data.keyword.Bluemix_notm}} puede crear recursos de infraestructura
{: #accountprep-environment}

Las instancias de CFEE se despliegan en recursos de infraestructura, que son nodos de trabajador de Kubernetes del servicio de IBM Containers.  [Prepare su cuenta de IBM Cloud](/docs/cloud-foundry/prepare-account.html) para garantizar que puede crear los recursos de infraestructura necesarios para una instancia de CFEE.

## Paso 2: Creación de su instancia de CFEE
{: #creating-environment}

Antes de crear su CFEE, asegúrese de que está utilizando la cuenta de IBM Cloud de {{site.data.keyword.Bluemix_notm}} en la que desea crear el entorno y de que dispone de las políticas de acceso necesarias (en el paso 1 anterior).

1. Abra el catálogo de {{site.data.keyword.Bluemix_notm}} [](https://console.bluemix.net/catalog).
2. Localice el servicio de {{site.data.keyword.cfee_full_notm}} en el catálogo y púlselo para abrir la página de visión general del servicio.
3. La primera página de la página de creación proporciona un resumen de las características principales del servicio. Pulse **Continuar**.
4. Configure la instancia que se debe crear proporcionando lo siguiente:
    * Seleccione un plan (la disponibilidad de plan puede estar restringida durante la beta).
    * Escriba un **Nombre** para la instancia de servicio.
    * Seleccione una **Ubicación** en la que debe suministrarse la instancia de servicio.
    * Seleccione el **Número de células** para el entorno de Cloud Foundry.
    * Seleccione el **Tipo de máquina**, que determina el tamaño de las células de Cloud Foundry (CPU y memoria).
    * Seleccione un **Grupo de recursos** en el que se agrupa el entorno. Únicamente se listarán en el desplegable _Grupos de recursos_ los grupos de recursos a los que tiene acceso en la cuenta de IBM Cloud actual, lo que significa que necesita permisos para acceder como mínimo a un grupo de recursos en la cuenta para poder crear un CFEE.
5. De forma opcional, abra la sección **Infraestructura** para ver las propiedades del clúster de Kubernetes que ofrecen soporte a la instancia de CFEE. Tenga en cuenta que el **número de nodos de trabajador** es igual al número de celdas más 2 (dos de los nodos de trabajador de Kubernetes suministrados ofrecen soporte al plano de control de CFEE).
6. El **Resumen del pedido** en la parte derecha de la página refleja el coste de la instancia CFEE y el total estimado.
7. Haga clic en **Crear**, lo que abre el panel de control del entorno y muestra el estado y el progreso de creación.
8. Una vez iniciado el suministro, el entorno se muestra en el panel de control de {{site.data.keyword.Bluemix_notm}}, además de en el [panel de control de Cloud Foundry Environments](https://console.bluemix.net/dashboard/cloudfoundry?filter=cf_environments).  El estado indica cuándo se completa el suministro.

El proceso automatizado que crea el entorno despliega la infraestructura en un clúster de Kubernetes y la configura para que se pueda utilizar. El proceso tarda de 90 a 120 minutos.

**Nota:** El clúster de Kubernetes en el que se ha desplegado el entorno aparece en el panel de control de {{site.data.keyword.Bluemix_notm}} [](https://console.bluemix.net/dashboard/apps/). Para obtener más información, consulte la documentación de [{{site.data.keyword.Bluemix_notm}} Container Service](/docs/containers/cs_why.html#cs_ov).

## Paso 3: Creación de organizaciones y espacios

Después de crear el {{site.data.keyword.cfee_full_notm}}, consulte [Creación de organizaciones y espacios](/docs/cloud-foundry/orgs-spaces.html) para obtener información sobre cómo estructurar el entorno creando organizaciones y espacios. Las apps de {{site.data.keyword.cfee_full_notm}} abarcan espacios específicos. A su vez, el espacio existe en una organización específica. Los miembros de una organización comparten un plan de cuotas, apps, instancias de servicio y dominios personalizados.

**Nota:** La página _Organizaciones de Cloud Foundry_ disponible desde el menú **_Gestionar > Cuenta > Organizaciones de Cloud Foundry _** ubicado en la cabecera de IBM Cloud superior está destinado únicamente a organizaciones de IBM Cloud públicas, **no a organizaciones de CFEE**. Las organizaciones de CFEE se gestionan en la página _Organizaciones_ de una instancia de CFEE.  Abra la interfaz de usuario de CFEE y pulse en la página **_Organizaciones_** para crear y gestionar organizaciones para el CFEE.

## Paso 4: Adición de usuarios a organizaciones y espacios

[Añada usuarios](/docs/cloud-foundry/add-users.html) a las organizaciones y espacios con asignaciones de roles específicos controlando su nivel de acceso.  Antes de poder añadir a los usuarios como miembros de organizaciones y espacios en un CFEE, los usuarios deben tener acceso previo a la instancia de CFEE. Consulte [Permisos](/docs/cloud-foundry/permissions.html).

## Paso 5: Despliegue y visualización de aplicaciones

Cuando esté listo, puede [desplegar la app](/docs/cloud-foundry/deploy-apps.html) con la interfaz de línea de mandatos de {{site.data.keyword.Bluemix_notm}}.  Visualice la lista de aplicaciones desplegadas en la interfaz de usuario, en el contexto de un espacio de CFEE específico o de forma global en todas las instancias de CFEE.  También puede iniciar, detener o suprimir las aplicaciones de dichas vistas.

## Paso 6: Creación de alias e instancias de servicio

Cree [alias de servicio](/docs/cloud-foundry/add-serv-inst.html) a partir de las instancias de servicio disponibles en la cuenta de IBM Cloud para poder optimizarlas en sus aplicaciones de CFEE.

## Paso 7: Enlace de aplicaciones a instancias de servicio

[Enlace su app](/docs/cloud-foundry/binding.html) al alias de una instancia de servicio para poder utilizar las funciones del servicio.

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

Lo que puede ver y gestionar está limitado por sus organizaciones y pertenencias a espacios y por los roles.
