---



copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-01-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Alojamiento de apps en {{site.data.keyword.Bluemix_notm}}
{: #hosting_apps}

Con {{site.data.keyword.Bluemix}}, puede crear apps y alojar sus apps existentes. Puede trasladar su app a {{site.data.keyword.Bluemix_notm}} siempre que esté preparada para la nube. {{site.data.keyword.Bluemix_notm}} proporciona muchos modos distintos para ejecutar las apps, como por ejemplo Cloud Foundry, IBM Containers y Virtual Machines.

## Cómo hacer que sus apps estén listas para la nube
{: #cloud-readyapps}

Si su app cumple todos los principios siguientes, será una app
lista para la nube y se puede migrar a {{site.data.keyword.Bluemix_notm}}. Si su app infringe algún principio, por lo general podrá [modificarla](../apps/cloud-ready.html) para que lo cumpla.

## Migración de sus apps
{: #ht_hostapp}

Puede migrar sus apps a {{site.data.keyword.Bluemix_notm}} de forma incremental, en lugar de desplazarlas completamente al entorno de nube. Primero puede migrar una parte de
su app y conectar a los datos existentes o sistema de registros mediante el
servicio Cloud Integration.

En sus apps de nube, podría necesitar acceso a los datos o servicios de fondo, por ejemplo,
un sistema de registros. En {{site.data.keyword.Bluemix_notm}},
puede utilizar el servicio Secure Gateway para establecer un túnel seguro entre una
organización de {{site.data.keyword.Bluemix_notm}} y la red principal de fondo empresarial. El servicio permite a las
apps en {{site.data.keyword.Bluemix_notm}} acceder a los datos y servicios de la red principal de fondo. Para obtener detalles, consulte [Alcanzar el elemento de fondo empresarial con {{site.data.keyword.Bluemix_notm}} Secure Gateway a través de la consola ![Icono de enlace externo](../icons/launch-glyph.svg)](https://developer.ibm.com/bluemix/2015/04/01/reaching-enterprise-backend-bluemix-secure-gateway/){: new_window}.

Para desplegar su app en {{site.data.keyword.Bluemix_notm}} como una app de Cloud Foundry, seleccione un ejecutable del catálogo de {{site.data.keyword.Bluemix_notm}}. El ejecutable contiene una app Hello World iniciadora que puede sustituir por su propia app. Si no encuentra un iniciador que proporcione
el ejecutable que quiere, puede aportar un paquete de compilación personalizado
compatible con Cloud Foundry a {{site.data.keyword.Bluemix_notm}}, utilizando la opción -b con el
mandato cf push. Para obtener detalles, consulte [Uso de paquetes de compilación de comunidad](byob.html).

Puede utilizar las herramientas y servicios siguientes que {{site.data.keyword.Bluemix_notm}} proporciona:

| Herramienta | Método |
|:------|:--------|
| Interfaz de línea de mandatos de Cloud Foundry (cf cli) | Gestione su código en el cliente local y utilizar la interfaz de línea de mandatos de Cloud Foundry para enviar por push su app manualmente a {{site.data.keyword.Bluemix_notm}}. Para obtener más información, consulte [Subir sus apps](../starters/upload_app.html). |
| Eclipse | Gestione su código en Eclipse y utilice IBM Eclipse tools for {{site.data.keyword.Bluemix_notm}} para enviar por push su app. |
| Integración con Git | Gestione su código en GitHub e integre Git en {{site.data.keyword.Bluemix_notm}}. Puede colaborar con otros desarrolladores. Su app se despliega automáticamente en
{{site.data.keyword.Bluemix_notm}} cuando confirma los cambios en el código. No necesita enviar por push manualmente
la app. |
| {{site.data.keyword.Bluemix_notm}} DevOps Delivery Pipeline | Gestione su código en el repositorio DevOps GitHub y despliegue su app en
{{site.data.keyword.Bluemix_notm}} utilizando DevOps Delivery Pipeline. |
{: caption="Tabla 1. Herramientas de {{site.data.keyword.Bluemix_notm}}" caption-side="top"}

Si la plataforma Cloud Foundry no admite los requisitos de su app,
puede utilizar un contenedor o MV en la que el tiempo de ejecución se establezca,
configure y mantenga con opciones más personalizadas.

## Despliegue y desarrollo de apps utilizando cadenas de herramientas en Continuous Delivery
{:ht_cd}

Añada una [cadena de herramientas a su app](/docs/services/ContinuousDelivery/toolchains_working.html#creating_a_toolchain_from_an_app) y, a continuación, utilice la [interfaz de usuario de la cadena de herramientas de Continuous Delivery](/docs/services/ContinuousDelivery/toolchains_using.html#toolchains-using) para desarrollar y desplegar su app.

## Subir sus apps mediante la CLI de cf
{: #ht_cfcli}

Puede gestionar su código en el cliente local y utilizar la
interfaz de línea de mandatos de Cloud Foundry para subir su app manualmente a
{{site.data.keyword.Bluemix_notm}}. Si cambia el código, debe enviar por push su app otra vez a {{site.data.keyword.Bluemix_notm}}
para ejecutar el código actualizado.

Realice los pasos siguientes para migrar su app:

Instalar la interfaz de línea de mandatos de Cloud Foundry. Asegúrese de utilizar la versión
más reciente de la interfaz de línea de mandatos de cf.
  1. Descargue el programa de instalación para su sistema operativo.
  2. Siga el asistente de la herramienta para instalar la línea de mandatos.
  3. Utilice el mandato siguiente para comprobar la versión de la interfaz de línea de mandatos de cf: `cf -v`

Opcional: Si quiere especificar y guardar los detalles de despliegue antes de enviar por push
una app a {{site.data.keyword.Bluemix_notm}},
puede añadir el manifiesto de la app realizando los pasos siguientes:

  1. Acceda al directorio de trabajo de su app y cree un archivo llamado manifest.yml, que es el nombre predeterminado.</li>
  2. Especifique los detalles de despliegue en el archivo de manifiesto. El ejemplo siguiente muestra un archivo de manifiesto de una app Java™.

  ```
  aplicaciones:
  - disk_quota: 1024M
  host: myjavatest
  name: MyJavaTest
  path: webStarterApp.war
  domain: mybluemix.net
  instances: 1
  memory: 512M
  ```

Para obtener más información sobre las opciones admitidas que puede utilizar en este archivo, consulte
[Manifiesto de la app](depapps.html#appmanifest).

### Envíe la app por push

Puede subir su app utilizando el mandato `cf push`.
  1. Conecte e inicie sesión en {{site.data.keyword.Bluemix_notm}} ejecutando el mandato siguiente. Seleccione su
organización y espacio cuando se le solicite.
  ```
  cf login -a https://api.ng.bluemix.net
  ```
  Añada el distintivo `-sso` si su organización utiliza Single Sign On.

  2. En el directorio de la app, escriba el mandato cf push con el nombre de la app. El nombre de la app debe ser exclusivo en el entorno {{site.data.keyword.Bluemix_notm}}.

  ```
  cf push nombre_app
  ```

  3. Opcional: Si utiliza un paquete de compilación externo, debe usar la opción -b
con el mandato push de cf. Por ejemplo:

  ```
  cf push appname -b buildpack_URL
  ```

  Para obtener detalles, consulte [Utilización de paquetes de compilación de la comunidad](byob.html).

Opcional: Si modifica la app, debe cargar los cambios volviendo a especificar el mandato `cf push`. La interfaz de línea de mandatos cf utiliza sus opciones anteriores y las respuestas a las solicitudes para actualizar las instancias en ejecución de la app con los nuevos bits de código.

#### Notas:

* Cuando se utiliza el mandato cf push, la interfaz de línea de mandatos de copia todos los archivos y directorios del directorio actual en {{site.data.keyword.Bluemix_notm}}. Asegúrese de tener solo los archivos necesarios en su directorio de app.
* Asegúrese de que su organización dispone de memoria suficiente para todas las instancias de su
app. Para ver la cuota de memoria para su organización, utilice cf org org_name.
* Para obtener más información sobre cf push, consulte [Mandatos cf](../cli/reference/cfcommands/index.html).

## Migración de sus datos y uso de servicios
{: #ht_service}

Tras subir su app a {{site.data.keyword.Bluemix_notm}}, seleccione en el catálogo de {{site.data.keyword.Bluemix_notm}} el servicio al que está conectado su app, cree una instancia de servicio, enlace la instancia a su app y luego reinicie su app.

La variable de entorno VCAP_SERVICES de su app es un
objeto JSON que contiene información sobre cómo interactuar con una instancia de servicio en
{{site.data.keyword.Bluemix_notm}}. La información incluye el nombre de instancia de servicio, credenciales y el URL de conexión
a la instancia de servicio.

Para ejecutar su código en {{site.data.keyword.Bluemix_notm}},
debe añadir la lógica de código para el análisis de la variable VCAP_SERVICES
para obtener información sobre la conexión de servicio. Modifique su app para
obtener el host y el puerto asignados dinámicamente para la instancia de servicio
por medio de variables de entorno. El ejemplo siguiente muestra cómo obtener las credenciales de una
instancia de servicio de Postgre SQL en una app de Ruby:

```
services = JSON.parse(ENV['VCAP_SERVICES'], :symbolize_names => true)
        url = services.values.map do |srvs|
          srvs.map do |srv|
            if srv[:credentials][:uri] =~ /^postgres/
              srv[:credentials][:uri]
            else
              []
            end
          end
        end.flatten!.first
```
{:codeblock}

Para asegurarse de que su app se pueda ejecutar en un entorno local tras modificarla para
{{site.data.keyword.Bluemix_notm}},
compruebe la presencia de la variable de entorno VCAP_SERVICES, que se establece para todas las
apps de {{site.data.keyword.Bluemix_notm}} Cloud
Foundry.


# Enlaces relacionados
{: #rellinks}

## Enlaces relacionados
{: #general}

* [{{site.data.keyword.containershort_notm}}](/docs/containers/container_index.html)
* [Virtual Machines](/docs/virtualmachines/vm_index.html)
* [Cómo empezar con Delivery Pipeline](/docs/services/DeliveryPipeline/index.html)
* [Despliegue de apps con IBM Eclipse Tools for Bluemix](/docs/manageapps/eclipsetools/eclipsetools.html)
* [La app de factor doce (twelve-factor)![icono de enlace externo](../icons/launch-glyph.svg)](http://12factor.net/){: new_window}
* [Alcanzar el elemento de fondo empresarial con Bluemix Secure Gateway a través de la consola ![icono de enlace externo](../icons/launch-glyph.svg)](https://developer.ibm.com/bluemix/2015/04/01/reaching-enterprise-backend-bluemix-secure-gateway/){: new_window}
