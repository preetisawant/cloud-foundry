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

# Guía de aprendizaje de iniciación
{: #getting-started}

{{site.data.keyword.cfee_full}} (CFEE) es una plataforma en la nube para alojar apps y servicios en la nube. {{site.data.keyword.cfee_full_notm}} facilita el escalado de apps a medida que aumenta el consumo, simplificando el tiempo de ejecución, el middleware y la infraestructura para que pueda centrarse en desarrollar apps.
{: shortdesc}

Esta guía de aprendizaje de iniciación muestra cómo crear un {{site.data.keyword.cfee_full_notm}}, añadir usuarios, crear una organización y espacios, desplegar apps y enlazar dichas apps a servicios.

**Nota:** Los pasos siguientes se aplican a los CFEE creados a partir del plan **Estándar**.  Si este CFEE se ha creado desde el plan **Presentación técnica de Eirini**, siga los **pasos del 1 al 6** y el paso **11**. Las prestaciones descritas en los pasos 8 a 11 no reciben soporte en el plan de _Presentación técnica de Eirini_.  Consulte [Iniciación a la presentación técnica de Eirini](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-getting-started-eirini#getting-started-eirini).
El plan de _presentación técnica de Eirini_ le permite explorar un CFEE utilizando Kubernetes nativo como planificador de contenedores (en lugar de Diego).  El planificador de Kubernetes se utiliza en CFEE para desplegar y ejecutar apps en el entorno de ejecución de aplicaciones Cloud Foundry, añadir usuarios, crear una organización y espacios, desplegar apps y enlazar esas apps a los servicios. 

## Paso 1: Crear su instancia de CFEE
{: #create-environment}

Puede crear una instancia de {{site.data.keyword.cfee_full_notm}} (CFEE) desde el catálogo de {{site.data.keyword.Bluemix_notm}}. Antes de crear la instancia de CFEE, visite la documentación sobre cómo [Crear un entorno](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-create-environment#create-environment) para obtener instrucciones sobre cómo preparar la cuenta de {{site.data.keyword.Bluemix_notm}} y garantizar los permisos correctos y ver los pasos para crear la instancia de CFEE.


## Paso 2: Crear organizaciones y espacios
{: #create-orgsandspaces}

Después de crear el {{site.data.keyword.cfee_full_notm}}, consulte [Creación de organizaciones y espacios](https://cloud.ibm.com/docs/cloud-foundry/orgs-spaces.html) para obtener información sobre cómo estructurar el entorno creando organizaciones y espacios. Las apps de {{site.data.keyword.cfee_full_notm}} abarcan espacios específicos. A su vez, el espacio existe en una organización específica. Los miembros de una organización comparten un plan de cuotas, apps, instancias de servicio y dominios personalizados.

Cuando se crea una organización, se le asigna una cuota.  La cuota fija los límites de recursos (memoria, cpu, etc.) disponible para dicha organización. Puede asignar una cuota distinta posteriormente. Hay un conjunto de cuotas preconfiguradas disponibles en cada CFEE, pero también puede crear sus propias cuotas personalizadas en la página **Cuotas** de la interfaz de usuario de CFEE.  Puede convertir una cuota personalizada en la cuota _predeterminada_ invocando la acción _Copiar en valor predeterminado_ del menú de la cuota, que copia los valores de la cuota personalizada en la cuota predeterminada.

**Nota:** La página _Organizaciones de Cloud Foundry_ disponible desde el menú **_Gestionar > Cuenta > Organizaciones de Cloud Foundry_** ubicado en la cabecera de IBM Cloud superior está destinado únicamente a organizaciones de IBM Cloud públicas, **no a organizaciones de CFEE**. Las organizaciones de CFEE se gestionan en la página _Organizaciones_ de una instancia de CFEE.  Abra la interfaz de usuario de CFEE y pulse en la página **_Organizaciones_** para crear y gestionar organizaciones para el CFEE.

## Paso 3: Añadir usuarios a organizaciones y espacios
{: #add-users}

[Añada usuarios](https://console.bluemix.net/docs/cloud-foundry/add-users.html) a las organizaciones y espacios con asignaciones de roles específicos controlando su nivel de acceso.  Antes de poder añadir a los usuarios como miembros de organizaciones y espacios en un CFEE, los usuarios deben tener acceso previo a la instancia de CFEE. Consulte [Permisos](https://console.bluemix.net/docs/cloud-foundry/permissions.html).

## Paso 4: Desplegar y ver las aplicaciones
{: #deploy-apps}

Cuando esté listo, puede [desplegar la app](https://cloud.ibm.com/docs/cloud-foundry/deploy-apps.html) con la interfaz de línea de mandatos de {{site.data.keyword.Bluemix_notm}}.  Visualice la lista de aplicaciones desplegadas en la interfaz de usuario, en el contexto de un espacio de CFEE específico o de forma global en todas las instancias de CFEE.  También puede iniciar, detener o suprimir las aplicaciones de dichas vistas.

## Paso 5: Crear o añadir instancias de servicio de IBM Cloud a espacios de CFEE
{: #service-instances}

Las funciones [Crear servicios](https://cloud.ibm.com/docs/cloud-foundry/add-serv-inst.html#workingwith-services#creating-services-inspace) o [Añadir servicios existentes](https://cloud.ibm.com/docs/cloud-foundry/add-serv-inst.html#workingwith-services#adding-services-inspace) se encuentran disponibles en la cuenta de IBM Cloud.  Cuando se encuentre disponible una instancia de servicio en un espacio CFEE, puede enlazarla a las aplicaciones CFEE desplegadas en dicho espacio.

## Paso 6: Enlazar aplicaciones a instancias de servicio
{: #bind-apps}

[Enlace su app](https://cloud.ibm.com/docs/cloud-foundry/binding.html) al alias de una instancia de servicio para poder utilizar las funciones del servicio.

En el [panel de control de Cloud Foundry](https://cloud.ibm.com/dashboard/cloudfoundry/overview){: new_window} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo") tendrá una vista consolidada de todas las aplicaciones y servicios, tanto *públicos* como de *empresa*.  Una vez en el panel de control de Cloud Foundry, pulse *Público* en el panel de navegación de la izquierda para ver las aplicaciones y servicios públicos disponibles en la cuenta de IBM Cloud.  Pulse en *Enterprise* para ver todos los entornos de CFEE, aplicaciones desplegadas en espacios de CFEE y servicios disponibles en espacios de CFEE.
{:tip}

## Paso 7: Habilitar la persistencia de auditoría y registro (opcional)
{: #enable-auditingandlogging}

Habilite el entorno para [sucesos de auditoría](https://cloud.ibm.com/docs/cloud-foundry/auditing-logging.html#auditing-logging#auditing) y [persistencia de registro](https://cloud.ibm.com/docs/cloud-foundry/auditing-logging.html#logging).

## Paso 8: Habilitar las herramientas de supervisión (opcional)
{: #enable-monitoring}

Las herramientas de supervisión no se suministran automáticamente en instancias de CFEE v2.2.0 o posteriores. Los administradores de CFEE pueden [habilitar las herramientas de supervisión](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-monitoring) una vez que se ha creado la instancia de CFEE. El conjunto de herramientas de supervisión incluye Prometheus, Grafana y Alertmanager.

## Paso 9: Crear y proteger los dominios de Cloud Foundry (opcional)
{: #create-domains}

Cree [dominios](https://cloud.ibm.com/docs/cloud-foundry/domains.html#domains) para todas las aplicaciones de CFEE (dominios compartidos) o para determinada organización (dominios privados) y protéjalos con certificados SSL.

## Paso 10: Configurar el orden de precedencia de los paquetes de compilación de Cloud Foundry
{: #create-buildpacks}

Los paquetes de compilación proporcionan el soporte de tiempo de ejecución para las aplicaciones desplegadas en un entorno de Cloud Foundry, configurando automáticamente el tiempo de ejecución para una aplicación y gestionando sus dependencias.  Cloud Foundry incluye un conjunto de paquetes de compilación para lenguajes e infraestructuras comunes.  [Obtenga más información](https://docs.cloudfoundry.org/buildpacks/) sobre los paquetes de compilación de Cloud Foundry.  

Puede crear y cargar paquetes de compilación personalizados en la página **Paquetes de compilación** de la interfaz de usuario de CFEE. Los paquetes de construcción tienen una posición ordinal en la lista de prioridades.  Durante la transferencia de una aplicación, Cloud Foundry comprueba la compatibilidad de la aplicación con el conjunto de paquetes de compilación, empezando por la posición 1. Las comprobaciones de compatibilidad se realizan en la lista de prioridades hasta que se encuentra un paquete de compilación compatible. Asegúrese de que la secuencia de prioridades del conjunto de paquetes de compilación satisface las necesidades de los equipos de desarrollo.  Puede cambiar la posición de un paquete de compilación en la secuencia de prioridades arrastrando y soltando el nombre del paquete de compilación en otra posición.  También puede gestionar los paquetes de compilación a través de la [CLI de Cloud Foundry](https://docs.cloudfoundry.org/adminguide/buildpacks.html).

## Paso 11: Instalar Stratos Console para gestionar aplicaciones (opcional)
{: #install-stratos}

Stratos Console es una herramienta basada en web de código abierto para trabajar con Cloud Foundry. La aplicación Stratos Console se puede instalar de forma opcional y utilizarse en un entorno de CFEE específico para gestionar sus organizaciones, espacios y aplicaciones.

Los usuarios con roles de administrador o editor de IBM Cloud en la instancia de CFEE pueden instalar la aplicación Stratos Console en dicha instancia de CFEE.

Para instalar la aplicación Stratos Console:

1. Abra la instancia de CFEE en la que desea instalar Stratos Console.
2. Pulse **Instalar Stratos Console** en la página de visión general. El botón está visible únicamente para los usuarios con permisos de administrador o editor en la instancia de CFEE.
3. En el diálogo Instalar Stratos Console, seleccione una opción de instalación. Puede instalar la aplicación Stratos en una célula de Cloud Foundry o en el clúster Kubernetes. Seleccione una versión de Stratos Console y el número de instancias de la aplicación a instalar. Si instala la app Stratos Console en una célula de Cloud Foundry, se le solicitará que proporcione una organización y espacio en los que desplegar la aplicación.
4. Pulse **Instalar**.

La instalación de la aplicación tarda 5 minutos aproximadamente. Una vez completada la instalación, aparecerá el botón de **Stratos Console** en lugar del botón _Instalar Stratos Console_ en la página de visión general. El botón _Stratos Console_ inicia la consola y está disponible para todos los usuarios con acceso a la instancia de CFEE. Es posible que las asignaciones de pertenencia a un espacio y organización limiten lo que un usuario puede ver y gestionar en Stratos Console.

Para iniciar Stratos Console:

1. Abra la instancia de CFEE en la que se ha instalado Stratos Console.
2. Pulse **Stratos Console** en la página de visión general.
3. Stratos Console se abre en un separador del navegador distinto. Cuando abre la consola por primera vez, se le solicita que acepte dos avisos consecutivos debido a certificados autofirmados.
4. Pulse **Iniciar sesión** para abrir la consola. No se necesitan credenciales puesto que la aplicación utiliza sus credenciales de {{site.data.keyword.Bluemix_notm}}.

## Recursos adicionales
{: #additional-resources}

Puede realizar algunas tareas de administración en CFEE con los mandatos de CLI `ibmcloud CFEE`. Los mandatos le permiten obtener información sobre una instancia de CFEE, así como gestionar sus organizaciones y espacios. Revise la [Consulta de mandatos de CFEE de CLI de IBM Cloud](https://console.cloud.ibm.com/docs/cli/reference/ibmcloud/cli_cfee.html#ibmcloud_commands_cfee){: new_window} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo").

Encontrará vídeos y explicaciones y demostraciones exhaustivas sobre diversos temas de CFEE en la [lista de reproducciones de vídeos de CFEE](https://ibm.biz/CFEE-Playlist){: new_window} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo").

Encontrará información sobre las API de CFEE en la [documentación de API](https://cloud.ibm.com/apidocs/cfaas){: new_window} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo").
