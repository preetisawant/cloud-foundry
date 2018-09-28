---

copyright:
  years: 2018
lastupdated: "2018-04-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Creación y visualización de instancias de servicio
{: #creating-services}

Las aplicaciones desplegadas en {{site.data.keyword.cfee_full_notm}} pueden enlazarse a dos tipos de instancias de servicio:
1. Las instancias de servicio gestionadas por un intermediario de servicio de Cloud Foundry local (local en el CFEE). Estas, a su vez, también pueden ser de dos tipos:
   *  1a. Una instancia de una oferta de servicios creada desde el mercado de Cloud Foundry de la instancia de {{site.data.keyword.cfee_full_notm}} actual. Este tipo de instancia de servicio requiere un intermediario de servicio registrado disponible en el entorno. Un intermediario de servicio muestra un catálogo de ofertas de servicio y planes y, además, permite la creación, la eliminación, el enlace y la desvinculación de instancias desde dichas ofertas de servicio. Consulte [Gestión de intermediarios de servicio](https://docs.cloudfoundry.org/services/managing-service-brokers.html) en la documentación de Cloud Foundry para obtener más información.
   * 1b. Una instancia de servicio proporcionada por el usuario. La creación de este tipo se admite mediante la CLI, pero no mediante la interfaz de usuario. Sin embargo, las instancias de servicio proporcionadas por el usuario se listarán en la interfaz de usuario.
2. Instancias de servicio públicas creadas a partir del catálogo de {{site.data.keyword.Bluemix}} y disponibles en la cuenta de {{site.data.keyword.Bluemix}}.
Las instancias de servicio públicas disponibles en la cuenta de {{site.data.keyword.Bluemix}} no pueden estar disponibles por sí mismas en entornos de CFEE.  Para que una instancia de servicio pública (disponible en la cuenta de {{site.data.keyword.Bluemix}}) esté disponible en espacios en un entorno de CFEE, debe crearse un alias para la instancia de servicio en el espacio CFEE de destino. Las funciones de alias son una referencia a la instancia de servicio pública real.  Cuando se haya creado el alias de servicio en un espacio de CFEE, puede enlazarse a aplicaciones de dicho CFEE.  La asignación de alias de servicio permite a los desarrolladores optimizar el amplio catálogo de servicios de {{site.data.keyword.Bluemix}} en las aplicaciones desplegadas en entornos CFEE.


## Creación y visualización de alias de servicio en un espacio de CFEE
{: #creating-services_inspace}

Un alias para una instancia de servicio pública existente disponible en su cuenta de IBM Cloud le permite enlazar dicha instancia de servicio a aplicaciones desplegadas en un espacio de CFEE. La creación de un alias para una instancia de servicio de {{site.data.keyword.Bluemix_notm}} existente requiere el acceso de usuario a la propia instancia. Para obtener más información, consulte la página Identidad y acceso en el menú **Gestionar > Usuarios** en la cabecera de {{site.data.keyword.Bluemix_notm}} para verificar las políticas de acceso de la cuenta actuales.

Para crear un alias de instancia de servicio en un espacio en CFEE:

1. En el panel de control de {{site.data.keyword.Bluemix_notm}}, busque el entorno de Cloud Foundry Enterprise que aloja su aplicación.
2. Vaya a **Organizaciones** en el panel de navegación y abra la organización y espacio en los que se ubica la aplicación.
3. Vaya al separador **Espacios** y ubique el espacio que contiene la aplicación.
4. En la página del espacio de destino, vaya al separador **Servicios** y pulse **Crear servicio**.  Se abrirá la página **Catálogo** para {{site.data.keyword.cfee_full_notm}}.  La página lista ofertas de servicios de dos fuentes (consulte la columna _Fuente_):
   * Ofertas del catálogo de IBM Cloud.
   * Ofertas del mercado de {{site.data.keyword.cfee_full_notm}} local.
5. Busque y seleccione una oferta de servicio disponible para la que desee crear una instancia.
6. En función de la fuente de la oferta de servicio (IBM Cloud o CFEE local) haga lo siguiente:
   * **Continue** a la página de creación de la oferta de servicio de IBM Cloud para proporcionar el nombre de la nueva instancia de servicio, región, plan y otras propiedades necesarias para crear el servicio en IBM Cloud.  Cuando haga clic en *Crear*, se creará la instancia de servicio en IBM Cloud.  Además, se creará un alias de la misma instancia de servicio en {{site.data.keyword.cfee_full_notm}}.  El alias estará disponible para enlazarlo con aplicaciones de {{site.data.keyword.cfee_full_notm}}.
   **Nota:** Al crear {{site.data.keyword.Bluemix_notm}} de esta forma, además de crear una instancia pública disponible para los usuarios de la cuenta de IBM Cloud, se crea un alias para dicha instancia de servicio en el {{site.data.keyword.cfee_full_notm}} desde el que se creó.
   * **Cree** la instancia de servicio en el mercado de Cloud Foundry local. Se abrirá un diálogo en el que proporciona el nombre de la nueva instancia de servicio y del plan. Cuando haga clic en *Crear*, la instancia de servicio se creará en {{site.data.keyword.cfee_full_notm}} y estará disponible para enlazarse con aplicaciones de {{site.data.keyword.cfee_full_notm}}.

Una vez creada, la instancia de servicio (si se ha creado en el mercado de Cloud Foundry local), o el alias (si la instancia de servicio se ha creado a partir del catálogo de IBM Cloud) se listan en el separador **Servicios**.


## Creación y visualización de los alias de servicio en todos los entornos de CFEE del panel de control de Cloud Foundry global
{: #creating-services_across}

Puede ver una vista consolidada de todos los alias de la instancia de servicio (en todas las instancias de CFEE) en el panel de control de Cloud Foundry global.

1. Haga clic en el icono Menú ![Comprobación de cuenta](img/HamburgerMenu.png "Captura de pantalla que muestra el icono de menú") > **Cloud Foundry** para abrir el panel de control de Cloud Foundry.
2. Haga clic en **Empresa > Servicios** en el panel de navegación izquierdo.
La tabla de la vista muestra la información siguiente:

| Elemento   | Descripción |
|-----------|---------------|
| Alias de servicio | El nombre del alias de la instancia de servicio. |
| Instancia de servicio | La instancia de servicio de IBM Cloud pública desde la que se ha creado el alias. |
| Oferta | La oferta de servicio del catálogo de IBM Cloud desde la que se ha creado la instancia de servicio. |
| CFEE | El {{site.data.keyword.cfee_full}} en el que reside el alias. |
| Organización | La organización de la instancia del CFEE en la que reside el alias. |
| Espacio | El espacio de la organización de la instancia de CFEE en la que reside el alias. |
{:caption="Tabla 1. Descripción de elementos clave" caption-side="top"}

Puede realizar las acciones siguientes en esta vista:
* Ordenar los elementos de la tabla según las propiedades que se muestran como columnas de tabla.
* Enlazar aplicaciones a un alias específico accediendo al menú de desbordamiento de alias del alias ubicado en el extremo derecho de la fila.
* Expandir un alias (fila) para ver todas las aplicaciones enlazadas al mismo.
* Iniciar o detener aplicaciones accediendo al menú de desbordamiento de aplicación del alias ubicado en el extremo derecho de la fila.
* Ir a un CFEE, una organización de CFEE o a un espacio de CFEE haciendo clic en el enlace con el espacio, organización o CFEE correspondiente.

Para crear un alias de servicio desde el panel de control de Cloud Foundry global:
1. Haga clic en el botón **Crear alias de servicio** en la parte superior de la página. Se abrirá el diálogo _Crear alias de servicio_.  El diálogo lista todas las instancias de servicio públicas disponibles en la cuenta de IBM Cloud actual.
2. Seleccione una de las instancias de servicio públicas.
3. Pulse **Crear**. Una vez creado, el nuevo alias de la instancia de servicio se añadirá a la lista.
El alias de servicio también aparecerá en la lista de servicios del espacio CFEE, en el que se puede enlazar a aplicaciones del mismo espacio (CFEE > Organizaciones > Espacio > Servicios).


