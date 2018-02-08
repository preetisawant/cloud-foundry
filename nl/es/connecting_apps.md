---

copyright:
  years: 2017, 2018
lastupdated: "2018-01-18"

---

{:shortdesc: .shortdesc}

# Gestión de conexiones
{: #connect_app}

Puede conectar un servicio a una aplicación {{site.data.keyword.Bluemix}} nueva o existente desde el separador **Conexiones** en el panel de control de su servicio. Conectar un servicio de Cloud Foundry a una aplicación de Cloud Foundry crea un enlace entre ellos y puede desenlazar, añadir conexiones adicionales o suprimir conexiones desde el separador **Conexiones**.

Sin embargo, cuando conecta una instancia de servicio gestionada por {{site.data.keyword.Bluemix_notm}} IAM con una aplicación de Cloud Foundry, IAM crea automáticamente un alias para el servicio gestionado en el espacio de Cloud Foundry correspondiente con la información de enlace que ha especificado. Este alias está representado como una instancia de servicio de Cloud Foundry de su servicio gestionado por IAM.
{:shortdesc}

## ¿Qué es un alias?
{: #what_is_alias}

Un alias es una conexión entre su servicio gestionado por IAM dentro de un grupo de recursos y una aplicación de Cloud Foundry dentro de una organización o un espacio. En la consola de {{site.data.keyword.Bluemix_notm}}, la conexión (alias) está representada como una instancia de servicio de Cloud Foundry. Puede gestionar sus alias modificando la instancia de servicio que representa su conexión.

Los alias son como enlaces simbólicos que mantienen referencias con recursos remotos para habilitar la interoperatividad y la reutilización de una instancia en toda la plataforma. Por ejemplo, puede crear una instancia de un servicio en un grupo de recursos y luego reutilizarla desde cualquier región de Cloud Foundry disponible creando un alias en una organización o espacio en esas regiones.

Se aplican las siguientes reglas a los alias:

* No hay ningún cargo adicional para un alias, pero cada alias se tiene en cuenta en su cuota en su organización de Cloud Foundry.
* Solo puede crear un alias por espacio de Cloud Foundry en la consola de {{site.data.keyword.Bluemix_notm}}. Sin embargo, se puede crear más de un alias por espacio utilizando la CLI de {{site.data.keyword.Bluemix_notm}}. Para obtener más información, consulte [Mandatos para gestionar grupos de recursos y recursos](/docs/cli/reference/bluemix_cli/bx_cli.html#commands-for-managing-resource-groups-and-resources).
* Puede crear varias conexiones entre su servicio gestionado por IAM y cualquier aplicación de Cloud Foundry en cualquier espacio, organización y región en la misma cuenta si tiene permisos.
* Varias conexiones realizadas en el mismo espacio con apps de Cloud Foundry diferentes desde una instancia de servicio gestionada por IAM utilizarán el mismo alias.
* Desenlazar una instancia de servicio gestionada por IAM *no* suprimirá la instancia de servicio de Cloud Foundry que representa el alias.
* Suprimir la aplicación de Cloud Foundry a la que está conectada su instancia de servicio gestionada por IAM *no* suprimirá la instancia de Cloud Foundry que representa el alias.
* Suprimir una instancia de servicio gestionada por IAM *suprimirá* la instancia de servicio de Cloud Foundry que representa el alias.

## Creación de una conexión (alias) entre un servicio gestionado por IAM y una app de Cloud Foundry
{: #creating_alias}

Para conectar su instancia de servicio gestionada por IAM con una aplicación de Cloud Foundry:

1. Vaya a su panel de control.

2. Pulse el nombre de su app para abrir la vista de detalles de la app.

3. Pulse **Conectar existente** y elija su app de Cloud Foundry existente. O pulse **Crear conexión** para crear una app de Cloud Foundry a la que conectarse.

4. Especifique el **Rol de acceso de conexión**. Este valor define el rol de acceso de servicio de IAM. Para obtener más información, consulte [Acceso de IAM](/docs/iam/users_roles.html#userroles).

5. Opcionalmente, puede proporcionar un **ID de servicio para conexión** permitiendo a IAM generar un valor exclusivo para usted o proporcionando un ID de servicio existente. Para obtener más información, consulte [Creación y gestión de ID de servicio](https://console.stage1.bluemix.net/docs/iam/serviceid.html#serviceids).

6. Pulse **Crear**.

## Visualización de un alias

Después de crear una conexión entre un servicio gestionado por IAM y una app de Cloud Foundry, se muestra el alias en el separador **Conexiones** de la app de Cloud Foundry conectada. Además, el alias se muestra como una instancia de servicio de Cloud Foundry en ejecución en su panel de control y solo contiene un separador **Conexiones** cuando la abre.

1. Vaya a su panel de control.
2. En la tabla **Servicios de Cloud Foundry**, pulse el nombre de la instancia de servicio para abrir la vista de detalles de servicio. Si solo tiene un separador **Conexiones**, es un alias.

## Supresión de un alias

La forma más fácil de suprimir el alias es suprimir la instancia de servicio gestionada por IAM. Sin embargo, puede mantener su instancia de servicio gestionada por IAM y en su lugar suprimir el alias directamente.

1. Vaya a su panel de control.
2. En la tabla **Servicios de Cloud Foundry**, pulse el nombre de la instancia de servicio para abrir la vista de detalles de servicio. Si solo tiene un separador **Conexiones**, es un alias.
3. Suprima la instancia.

## Creación de una conexión entre varios servicios de Cloud Foundry
{: #cf}

Para obtener más información sobre cómo enlazar un servicio de Cloud Foundry con otro servicio de Cloud Foundry, consulte [Utilización de servicios en otro servicio](../apps/reqnsi.html#add_service).
