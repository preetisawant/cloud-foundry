---

copyright:
  years: 2018
lastupdated: "2018-09-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Cómo trabajar con servicios
{: #workingwith-services}

Las aplicaciones desplegadas en {{site.data.keyword.cfee_full_notm}} pueden enlazarse a dos tipos de instancias de servicio:
1. Instancias de servicio públicas creadas a partir del catálogo de {{site.data.keyword.Bluemix}} y disponibles en la cuenta de {{site.data.keyword.Bluemix}}.  
Las instancias de servicio públicas disponibles en la cuenta de {{site.data.keyword.Bluemix}} no pueden estar disponibles por sí mismas en entornos de CFEE.  Para que una instancia de servicio pública (disponible en la cuenta de {{site.data.keyword.Bluemix}}) esté disponible para espacios en un entorno de CFEE, se deben añadir específicamente al espacio CFEE de destino. Cuando se haya añadido la instancia de servicio de {{site.data.keyword.Bluemix}} al espacio de CFEE, puede enlazarse a las aplicaciones de dicho espacio CFEE.  Esto permite a los desarrolladores optimizar el amplio catálogo de servicios de {{site.data.keyword.Bluemix}} en las aplicaciones desplegadas en entornos CFEE, al tiempo que permite el control de accesos a dichos servicios de {{site.data.keyword.Bluemix}}.

   Además de añadir instancias de servicio de {{site.data.keyword.Bluemix}} existentes a un espacio CFEE, puede crear una nueva instancia de servicio de {{site.data.keyword.Bluemix}} desde un espacio CFEE, que también lo añade automáticamente a dicho espacio CFEE.

2. Las instancias de servicio gestionadas por un intermediario de servicio de Cloud Foundry local (local en el CFEE). Estas, a su vez, también pueden ser de dos tipos:
   *  2a. Una instancia de una oferta de servicios creada desde el mercado de Cloud Foundry de la instancia de {{site.data.keyword.cfee_full_notm}} actual. Este tipo de instancia de servicio requiere un intermediario de servicio registrado disponible en el entorno. Un intermediario de servicio muestra un catálogo de ofertas de servicio y planes y, además, permite la creación, la eliminación, el enlace y la desvinculación de instancias desde dichas ofertas de servicio. Consulte [Gestión de intermediarios de servicio](https://docs.cloudfoundry.org/services/managing-service-brokers.html) en la documentación de Cloud Foundry para obtener más información.
   * 2b. Una instancia de servicio proporcionada por el usuario. La creación de este tipo se admite mediante la CLI, pero no mediante la interfaz de usuario. Sin embargo, las instancias de servicio proporcionadas por el usuario se listarán en la interfaz de usuario.
   

## Visualización de las instancias de servicios de {{site.data.keyword.Bluemix_notm}} en todos los entornos de CFEE
{: #viewing-services_across}

Vaya al [panel de control de servicios de Cloud Foundry](https://console.bluemix.net/dashboard/cloudfoundry/services) para obtener una vista consolidada de todas las instancias de servicio de {{site.data.keyword.Bluemix_notm}} (a las que tiene acceso) en la cuenta de {{site.data.keyword.Bluemix_notm}} y ver cuáles se han añadido a los espacios CFEE.

Esta vista muestra todos los {{site.data.keyword.Bluemix_notm}} disponibles en la cuenta e indica los que se han añadido (alias) a los espacios de CFEE. Expanda una instancia de servicio para mostrar los espacios de CFEE en los que se ha añadido.  Puede expandirlos para ver las aplicaciones en dichos espacios de CFEE a los que se han enlazado las instancias de servicio.  

Desde esta vista también puede enlazar las aplicaciones desplegadas en los espacios de CFEE a los que se han añadido dichas instancias de servicio. Vaya al menú situado en el extremo derecho de la fila de la tabla del servicio correspondiente (disponible para un espacio de CFEE específico) y seleccione **Enlazar a aplicaciones **.

## Adición de instancias de servicio de {{site.data.keyword.Bluemix_notm}} existentes a un espacio de CFEE
{: #adding-services_inspace}

Puede enlazar una instancia de servicio de {{site.data.keyword.Bluemix_notm}} a las aplicaciones desplegadas en un espacio de CFEE.  Antes de que una instancia de servicio de IBM Cloud pueda enlazarse a la aplicación desplegada en CFEE, debe añadirse al espacio de CFEE en el que se despliega la aplicación. Lo siguiente es necesario antes de poder añadir una instancia de servicio de {{site.data.keyword.Bluemix_notm}} a un espacio de CFEE:
* El servicio de {{site.data.keyword.Bluemix_notm}} deberá estar disponible en la misma cuenta de {{site.data.keyword.Bluemix_notm}} en la que reside la instancia CFEE.
* Debe tener acceso a la propia instancia de servicio de {{site.data.keyword.Bluemix_notm}}. Para obtener más información, consulte la página Identidad y acceso en el menú **Gestionar > Usuarios** en la cabecera de {{site.data.keyword.Bluemix_notm}} para verificar las políticas de acceso de la cuenta actuales.

Para añadir una instancia de servicio de {{site.data.keyword.Bluemix_notm}} existente a un espacio de CFEE:
1. Vaya al [panel de control de servicios de Cloud Foundry](https://console.bluemix.net/dashboard/cloudfoundry/services).  
2. Localice la instancia de servicio de {{site.data.keyword.Bluemix_notm}} en la lista e invoque el menú situado en el extremo derecho de la fila de la tabla correspondiente.
3. Seleccione **Añadir servicio**.
4. En el diálogo _Añadir servicio_, seleccione CFEE, la organización y el espacio en el que desea añadir el servicio y pulse **Añadir**.
5. Expanda el servicio de {{site.data.keyword.Bluemix_notm}} de destino para encontrar la nueva CFEE en la que se ha añadido el servicio.


Como alternativa, puede añadir una instancia de servicio de {{site.data.keyword.Bluemix_notm}} desde el espacio de CFEE donde desee añadirla:
1. En el [panel de control](https://console.bluemix.net/dashboard) de {{site.data.keyword.Bluemix_notm}} o [panel de control de los servicios de Cloud Foundry](https://console.bluemix.net/dashboard/cloudfoundry/services), busque el entorno de Cloud Foundry Enterprise que aloja su aplicación.
2. Vaya a **Organizaciones** en el panel de navegación y abra la organización y espacio en los que se ubica la aplicación.
3. Vaya al separador **Espacios** y ubique el espacio que contiene la aplicación.
4. En la página de espacio de destino, vaya al separador **Servicios** y pulse **Añadir servicios**.  Esto abrirá el diálogo __Añadir servicio__.  La página enumera las instancias de servicio disponibles en la cuenta de {{site.data.keyword.Bluemix_notm}}.
5. Busque y seleccione una instancia de servicio disponible que desee añadir al espacio CFEE. 
6. La instancia de servicio se añadirá a la lista de servicios disponible en el espacio de CFEE.

   **Nota:** Al añadir un servicio de {{site.data.keyword.Bluemix_notm}} a un espacio de CFEE, se crea un alias para dicha instancia de servicio en dicho espacio. Al **Eliminar** la instancia de servicio del espacio de CFEE (en el menú ubicado en el extremo derecho de la correspondiente fila de la instancia de servicio de la tabla), el servicio no se suprime de la cuenta pública.  La acción simplemente la elimina de la cuenta CFEE específica y ya no estará disponible para enlazarla a aplicaciones en ese espacio de CFEE.  Además, cuando suprime la propia instancia de servicio de la cuenta de {{site.data.keyword.Bluemix_notm}}, el servicio deja de estar disponible para cualquier espacio de CFEE. 

## Creación de instancias de servicio de {{site.data.keyword.Bluemix_notm}} desde una interfaz de usuario del espacio de CFEE
{: #creating-services_inspace}
Puede crear las instancias de servicio de {{site.data.keyword.Bluemix_notm}} desde un espacio de CFEE.  La creación de una instancia de servicio de {{site.data.keyword.Bluemix_notm}} da como resultado lo siguiente:
* La instancia de servicio de {{site.data.keyword.Bluemix_notm}} se crea en IBM Cloud.  Esto equivale a crear la instancia de servicio desde el [catálogo](https://console.bluemix.net/catalog) de {{site.data.keyword.Bluemix_notm}}.
* Se añade (alias) la instancia de servicio de {{site.data.keyword.Bluemix_notm}} en el espacio de CFEE desde el que se ha iniciado la acción de creación.


Para crear una instancia de servicio desde un espacio de CFEE:
1. En la página del espacio de destino, vaya al separador **Servicios** y pulse **Crear servicio**.  Se abrirá la vista **Marketplace** del {{site.data.keyword.cfee_full_notm}}.  La vista enumera las ofertas de servicios de dos fuentes (consulte la columna __Origen__):
   * Ofertas del catálogo de {{site.data.keyword.Bluemix_notm}}.
   * Ofertas del mercado de {{site.data.keyword.cfee_full_notm}} local.
5. Busque y seleccione una oferta de servicio disponible para la que desee crear una instancia. 
6. En función de la fuente de la oferta de servicio (catálogo de IBM Cloud o marketplace de CFEE local), continúe con una de las opciones siguientes:
   * Si la oferta de servicio seleccionado es una oferta de catálogo de {{site.data.keyword.Bluemix_notm}}, verá un botón para **Continuar** en la página de creación de la oferta de servicio de IBM Cloud.  Hay la misma página disponible en el catálogo de {{site.data.keyword.Bluemix_notm}}.  En esta página, debe proporcionar el nombre de la nueva instancia de servicio, región, plan y otras propiedades necesarias para crear el servicio en IBM Cloud.  Cuando cree la instancia de servicio, se creará en IBM Cloud y automáticamente se añadirá en el espacio de CFEE actual.
   * Si la oferta de servicios seleccionada procede del catálogo de CFEE local, verá un botón para **Crear** la instancia de servicio. Se le solicitará una organización y un espacio en el CFEE actual donde se creará la instancia de servicio.

## Creación de instancias de servicio de {{site.data.keyword.Bluemix_notm}} desde un espacio de CFEE utilizando la CLI
{: #creating-services_cli}

Puede crear una instancia de servicio desde la CLI de un espacio en un CFEE.  La creación de un servicio desde la CLI en un espacio de CFEE equivale a crearlo desde la interfaz de usuario de dicho espacio. Es decir, la creación de un servicio tiene el siguiente resultado doble:
* La instancia de servicio de {{site.data.keyword.Bluemix_notm}} se crea en IBM Cloud.  Esto equivale a crear la instancia de servicio desde el [catálogo](https://console.bluemix.net/catalog) de {{site.data.keyword.Bluemix_notm}}.
* Se añade (alias) la instancia de servicio de {{site.data.keyword.Bluemix_notm}} en el espacio de CFEE desde el que se ha iniciado la acción de creación.

La diferencia entre la creación de una instancia de servicio desde un espacio CFEE frente a la creación de la misma desde la CLI se encuentra en el ciclo de vida de la instancia de servicio creada.  Al crear la instancia de servicio en la interfaz de usuario de espacio de CFEE, el ciclo de vida de la instancia de servicio creada se controla desde la propia instancia de servicio en la cuenta de {{site.data.keyword.Bluemix_notm}}.  Esto significa que las actualizaciones del plan de servicio se controlan desde la instancia en la cuenta de {{site.data.keyword.Bluemix_notm}}, y no desde el espacio de CFEE.  De modo alternativo, si la instancia de servicio se crea desde la CLI, el ciclo de vida del servicio se controlará desde el espacio de CFEE (el servicio se actualiza desde el espacio de CFEE).

Las instancias de servicio creadas desde la CLI también se visualizarán en la interfaz de usuario, y se indican con un ` * ` junto al nombre de la instancia de servicio.

Para crear las instancias de servicio utilizando la CLI siga los pasos siguientes:

1. Descargue e instale la interfaz de línea de mandatos de {{site.data.keyword.Bluemix}} (si no la tiene [Descargar la CLI de Cloud Foundry](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html){: new_window} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo").

2. Vaya a la página Visión general de {{site.data.keyword.cfee_full}} y localice el punto final de API del entorno.

3. En la interfaz de línea de mandatos, fije el punto final de API en el punto final de su entorno de CFEE:

  ```
  cf api <api_enpoint>
  ```
  {: pre}

4. Inicie sesión en el entorno CFEE:

  ```
  cf login -u <username> -o <org_name> -s <space_name>
  ```
  {: pre}

  Si está utilizando un ID federado, utilice la opción `-sso`:

  ```
  cf login -o <org_name> -s <space_name> -sso
  ```
  {: pre}
  
5. Cree el servicio:
  
  ```
  cf create-service SERVICE PLAN SERVICE_INSTANCE -c '{"name":"value","name":"value"}'
  ```
  {: pre}

  Opcionalmente, puede proporcionar un archivo que contenga parámetros en un objeto JSON válido necesario para crear un servicio específico.
  La vía de acceso al archivo de parámetros puede ser una vía de acceso absoluta o relativa a un archivo:
  
  ```
  cf create-service SERVICE PLAN SERVICE_INSTANCE -c PATH_TO_FILE
  ```
  {: pre}
   
  A continuación se muestra un ejemplo de un objeto JSON válido:
   
  ```
   {
      "cluster_nodes": {
         "count": 5,
         "memory_mb": 1024
      }
   }
  ```
  {: pre}
  
   Para obtener ayuda para crear un servicio desde la CLI, emita lo siguiente:
  
  ```
  cf cs -help
  ```
  Consulte [Gestión de instancias de servicio con la CLI de cf](https://docs.cloudfoundry.org/devguide/services/managing-services.html){: new_window} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo") en la documentación de Cloud Foundry para obtener más información.
  
## Enlace de servicios con aplicaciones
{: #bind_services}

Puede enlazar una instancia de servicio a una aplicación desplegada en un CFEE, ya sea desde el [panel de control de servicio de Cloud Foundry](https://console.bluemix.net/dashboard/cloudfoundry/services) o desde el separador de servicios de una página de espacio de CFEE.  

Para enlazar una instancia de servicio a una aplicación desde el [panel de control de servicios de Cloud Foundry](https://console.bluemix.net/dashboard/cloudfoundry/services):
1. Vaya al [panel de control de servicios de Cloud Foundry](https://console.bluemix.net/dashboard/cloudfoundry/services) para obtener una vista consolidada de todas las instancias de servicio de {{site.data.keyword.Bluemix_notm}} disponibles en la cuenta de {{site.data.keyword.Bluemix_notm}}.  La vista también está pensada para mostrar qué instancias de servicios de {{site.data.keyword.Bluemix_notm}} están disponibles (con alias en) en qué espacios de CFEE. Puede expandir una instancia de servicio para mostrar los espacios de CFEE donde se ha añadido.  Puede expandirlos para ver las aplicaciones en dichos espacios de CFEE a los que se han enlazado las instancias de servicio. 
2. Localice la instancia de servicio de {{site.data.keyword.Bluemix_notm}} que desea enlazar.
3. Expanda la vista correspondiente para ver todos los espacios de CFEE en los que se ha añadido dicha instancia de servicio. Si dicha instancia de servicio no se ha añadido al espacio de CFEE en el que se ha desplegado la aplicación, seleccione **Añadir** en el menú que se encuentra en el extremo derecho de la fila para que la instancia de servicio esté disponible en el espacio de CFEE de destino.
4. Vaya al menú situado en el extremo derecho de la fila correspondiente al espacio/CFEE en el que está disponible la instancia de servicio, y seleccione **Enlazar aplicación**.
5. En el diálogo __Enlazar aplicación__ seleccione la aplicación que desea enlazar.
6. La aplicación ahora está enlazada a la instancia de servicio en el espacio de CFEE en el que se ha desplegado la aplicación.  Puede expandir la fila de la tabla correspondiente para ver las aplicaciones enlazadas en el espacio de CFEE.


Para enlazar una aplicación a una instancia de servicio desde la página __Servicios__ de un espacio de CFEE:

1. Abra la interfaz de usuario de CFEE donde se despliega la aplicación.
2. Vaya a **Organizaciones** en el panel de navegación de la izquierda y abra la organización y el espacio donde se ha desplegado la aplicación.
3. Vaya al separador **Espacios** y ubique el espacio que contiene la aplicación.
4. En la página del espacio de destino, vaya al separador **Servicios**.
5. En la tabla de **Instancias de servicio**, vaya al menú __Acciones__ en el extremo derecho de la fila correspondiente a la instancia de servicio que desea enlazar y seleccione **Enlazar**.
6. Seleccione la aplicación que desea enlazar a la instancia de servicio.

Para desenlazar una aplicación de la instancia de servicio:

1. En el separador **Servicios** del espacio, expanda la instancia de servicio de destino para mostrar las apps que están enlazadas al mismo.
2. Vaya al menú Acciones en la fila de la aplicación y seleccione **Desenlazar servicio**.

Consulte [Enlazar una instancia de servicio](https://docs.cloudfoundry.org/devguide/services/application-binding.html){: new_window} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo") en la documentación de Cloud Foundry para obtener más información sobre el enlace de aplicaciones utilizando la CLI.


