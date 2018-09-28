---

copyright:
  years: 2018
lastupdated: "2018-07-17"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Despliegue y visualización de apps
{: #deploy_apps}

Puede desplegar aplicaciones en {{site.data.keyword.Bluemix}} con la interfaz de línea de mandatos o los entornos de desarrollo integrado (IDE). También puede utilizar manifiestos de aplicación para desplegar aplicaciones. Cuando utilice un manifiesto de aplicación, debe reducir el número de detalles de despliegue que debe especificar cada vez que despliega una aplicación en {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## Despliegue de aplicaciones con el mandato Cloud Foundry
{: #dep_apps}

Descargar e instalar la interfaz de línea de mandatos de {{site.data.keyword.Bluemix}}. [Descargue la CLI de {{site.data.keyword.Bluemix_notm}} ](https://clis.ng.bluemix.net){: new_window} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo").

Después de instalar la interfaz de línea de mandatos, siga los pasos siguientes:

1. Cambie al directorio donde se encuentra el código. `cd <your_directory>`
2. Vaya a la página Visión general de {{site.data.keyword.cfee_full}} y localice el punto final de API del entorno.
3. En la interfaz de línea de mandatos, fije el punto final de API en el punto final de su entorno:

  ```
  cf api <api_enpoint>
  ```
  {: pre}

4. Inicie sesión en el entorno

  ```
  cf login -u <username> -o <org_name> -s <space_name>
  ```
  {: pre}

  Si está utilizando un ID federado, utilice la opción `-sso`.

  ```
  cf login -o <org_name> -s <space_name> -sso
  ```
  {: pre}

  **Nota**: Debe añadir comillas simples o dobles alrededor de `nombre de usuario`, `nombre_org` y `nombre_espacio` si el valor incluye un espacio, por ejemplo, `-o "my org"`.

5.  Desde `<your_new_directory>`, vuelva a desplegar la app en {{site.data.keyword.Bluemix_notm}} mediante el mandato `bluemix app push`. Para obtener más información sobre el mandato `cf app push`, consulte [Carga de una aplicación](/docs/starters/upload_app.html).

  ```
  cf push <app_name>
  ```
  {: pre}

6.  Acceda a la app navegando a `https://<app_url>.<AppDomainName>`.

## Visualización de aplicaciones desplegadas en la interfaz de usuario
{: #view_apps}

Puede visualizar aplicaciones desplegadas de CFEE en el contexto de un espacio específico o de forma global en todas las instancias de CFEE.

### Visualización de aplicaciones desplegadas en un espacio de CFEE específico
{: #view_specific}

Para visualizar aplicaciones desplegadas en un espacio específico de una instancia de CFEE específica:
1. Vaya al panel de control de [{{site.data.keyword.Bluemix_notm}} ](https://console.bluemix.net/dashboard/apps/) y abra el {{site.data.keyword.cfee_full_notm}} en el que desea crear organizaciones.
2. En la interfaz de usuario de {{site.data.keyword.cfee_full_notm}}, vaya a la entrada **Organizaciones** en el panel de navegación para abrir la página _Organizaciones_.
3. Vaya al separador **Espacios** en la parte superior de la página.
4. En el separador __Espacios__, haga clic en un espacio de la tabla para abrir la página del espacio.
5. En la página __Espacio__, vaya al separador **Aplicaciones**.
6. El separador __Aplicaciones_)_ muestra todas las aplicaciones desplegadas en el espacio.
De forma opcional, puede Iniciar, Reiniciar, Detener o Suprimir una aplicación accediendo al menú del extremo derecho de la fila que representa la aplicación.

También puede expandir la fila de una aplicación para visualizar las instancias de servicio a las que está enlazada la aplicación.

### Visualización de aplicaciones desplegadas en todas las instancias de CFEE
{: #view_global}

Para visualizar todas las aplicaciones desplegadas en todas las instancias de CFEE:
1. Haga clic en el icono Menú ![Comprobación de cuenta](img/HamburgerMenu.png "Captura de pantalla que muestra el icono de menú") > **Cloud Foundry** para abrir el panel de control de Cloud Foundry.
2. Haga clic en **Empresa > Aplicaciones** en el panel de navegación izquierdo.
La tabla de la vista muestra la información siguiente:

| Elemento   | Descripción |
|-----------|---------------|
| Nombre | El nombre de la aplicación. |
| Instancias | El número de instancias de la aplicación. |
| Entorno | El entorno de {{site.data.keyword.cfee_full}} en el que se despliega la aplicación. |
| Organización | La organización en la que se despliega la aplicación. |
| Espacio | La organización de la instancia del CFEE en la que reside el alias. |
| Memoria | La cantidad de memoria utilizada por la aplicación. |
| Estado | El estado de la aplicación. |
{:caption="Tabla 1. Descripción de elementos clave" caption-side="top"}

De forma opcional, puede Iniciar, Reiniciar, Detener o Suprimir una aplicación accediendo al menú del extremo derecho de la fila que representa la aplicación.
Puede pulsar en cualquiera de las aplicaciones, entornos, organizaciones o espacios para ir a la página correspondiente en la interfaz de usuario de CFEE.

En esta vista tiene la opción de agrupar aplicaciones por organización, espacio y/o nombre de aplicación.  Esta funcionalidad le permite fusionar en una única entidad las aplicaciones que pueden tener nombres distintos y/o estar desplegadas en distintas organizaciones o espacios de CFEE, pero que corresponden a la misma entidad de aplicación lógica.  Por ejemplo, puede tener aplicaciones distintas que representan componentes de un proyecto más amplio o que se despliegan en distintas etapas de entrega (por ejemplo, desarrollo, prueba, producción), pero que desearía visualizar agrupadas como parte de la misma entidad lógica.

Para agrupar aplicaciones, vaya al menú desplegable **Grupo** ubicado en la parte superior de la página.
Cuando agrupa aplicaciones, cada grupo resultante se representa mediante una única entrada en la tabla. Puede expandir la fila para mostrar las aplicaciones en dicho grupo.

Puede realizar las acciones siguientes en esta vista:
* Ordenar los elementos de la tabla según las propiedades que se muestran como columnas de tabla.
* Enlazar aplicaciones a un alias específico accediendo al menú de desbordamiento de alias del alias ubicado en el extremo derecho de la fila.
* Expandir un alias (fila) para ver todas las aplicaciones enlazadas al mismo.
* Iniciar o detener aplicaciones accediendo al menú de desbordamiento de aplicación del alias ubicado en el extremo derecho de la fila.
* Ir a un CFEE, una organización de CFEE o a un espacio de CFEE haciendo clic en el enlace con el espacio, organización o CFEE correspondiente.

## Manifiesto de aplicación
{: #appmanifest}

Los manifiestos de aplicación incluyen opciones que se aplican al mandato `cf push`. Puede utilizar un manifiesto de aplicación para reducir el número de detalles de despliegue que debe especificar cada vez que envíe por push una aplicación a {{site.data.keyword.Bluemix_notm}}.

En los manifiestos de aplicación, puede especificar opciones como el número de instancias de aplicación que se deben crear, el número de memoria y cuota de disco que se debe asignar y otras variables de entorno. También puede utilizar los manifiestos de aplicación para automatizar despliegues de aplicaciones. El nombre predeterminado de un archivo de manifiesto es `manifest.yml`.

### Opciones soportadas en el archivo de manifiesto

La tabla siguiente muestra las opciones soportadas que puede utilizar en un archivo de manifiesto de la aplicación. Si elige utilizar un nombre que no sea `manifest.yml`, debe utilizar la opción **-f** con el mandato `cf push`. En el ejemplo siguiente, `appManifest.yml` es el nombre del archivo:

```
cf push -f appManifest.yml
```

| Opciones | Descripción | Uso o ejemplo |
|:----------|:--------------|:---------------|
| **buildpack** | El URL o el nombre del paquete de compilación. | `buildpack: ` *URL_paquete_compilación* |
| **disk_quota** | La cuota de disco que se debe asignar a la aplicación. El valor predeterminado es 1 G. | `disk_quota: 500M` |
| **domain** | El nombre de dominio de la aplicación en {{site.data.keyword.Bluemix_notm}}. | `domain:` ng.bluemix.net |
| **host** | El nombre de host de la aplicación en {{site.data.keyword.Bluemix_notm}}. Este valor debe ser exclusivo en el entorno de {{site.data.keyword.Bluemix_notm}}. | `host:` *nombre_host* |
| **name** | El nombre de la aplicación en {{site.data.keyword.Bluemix_notm}}. Este valor debe ser exclusivo en el entorno de {{site.data.keyword.Bluemix_notm}}. | `name:` *nombre_app* |
| **path** | La ubicación de la aplicación. Este valor puede ser una vía de acceso relativa o absoluta. | `path:` *vía_acceso_a_aplicación* |
| **command** | El mandato de inicio personalizado para la aplicación o el mandato para ejecutar archivos script. | `command:` *mandato_personalizado* `command:` *bash ./run.sh* |
| **memory** | La cantidad de memoria que se debe asignar a la aplicación. El valor predeterminado es 1 G. | `memory: 512M` |
| **instances** | El número de instancias que van a crear para la aplicación. | `instances: 2` |
| **timeout** | El intervalo máximo de tiempo, en segundos, que se utiliza para iniciar la aplicación. El valor predeterminado es de 60 segundos. | `timeout: 80` |
| **no-route** | Un valor booleano para impedir que se asigne una ruta a la aplicación si la aplicación sólo se está ejecutando como programa de fondo. El valor predeterminado es **false**. | `no-route: true` |
| **random-route** | Un valor booleano para asignar una ruta aleatoria a la aplicación. El valor predeterminado es **false**. | `random-route: true` |
| **services** | Los servicios que se van a enlazar a la aplicación. | `services: - mysql_maptest` |
| **env** | Las variables de entorno personalizadas de la aplicación. | `env: DEV_ENV: production` |
{: caption="Tabla 2. Opciones soportadas en el archivo YAML de manifiesto" caption-side="top"}

### Un archivo de ejemplo manifest.yml
{: #sample}

En el ejemplo siguiente se muestra un archivo de manifiesto para una aplicación Node.js que utiliza el paquete de compilación Node.js integrado de la comunidad en {{site.data.keyword.Bluemix_notm}}.

```
---
- name: myNodejsapp
  memory: 256M
  disk_quota: 512M
  path: /dev/myNodejsApp
  buildpack: nodejs_buildpack
  host: nodejs001
  domain: mybluemix.net
  command: node app.js
  timeout: 80
  services:
  - mongo_8917
  env:
    env_type: production
```
{: codeblock}
