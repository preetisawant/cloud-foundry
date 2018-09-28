---

copyright:

  years: 2018
lastupdated: "2018-04-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Determinar sus espacios
{: #determinespaces}

Dentro de una organización, los espacios proporcionan un nivel adicional de cumplimiento y abstracción de los límites.

Un espacio es un área reservada de la organización donde los usuarios pueden desarrollar y ejecutar apps y servicios. En una organización podrá crear tantos espacios como desee y controlar los usuarios que tendrán acceso a dichos espacios. Consulte [Espacios](/docs/account/orgs_spaces.html#orgsspacesusers) para obtener más detalles.

Si tiene previsto definir muchos espacios, es posible que desee crear una aplicación para ayudar a gestionar los espacios. Cuando el número de espacios supere los sesenta, es posible que desee definir otra organización.

## Espacios para una única organización en comparación con varias organizaciones
{: #spaceconsiderations}

Cuando se adopta una arquitectura de organización única, el nivel de segregación y de abstracción se proporciona mediante los espacios que define en la organización. Tenga en cuenta lo siguiente al definir espacios:

* Defina un espacio para alojar un servicio que necesite suministro y configuración sólo una vez en la organización.
* Defina espacios basados en el ciclo de vida de entrega.
  Por ejemplo, puede definir uno o varios espacios para apps que se están desarrollando, uno o varios espacios para apps que se encuentran en fase de prueba, y una o varios espacios para apps que están en producción.
* Si el límite del ciclo de vida de entrega no es suficiente, puede conseguir más segregación definiendo uno o varios espacios por LOB y fase de entrega.
* Identifique si necesita imponer límites para distintos grupos de usuarios.
  Por ejemplo, sus desarrolladores no pueden desarrollar la aplicación ni probarla. Necesita un conjunto distinto de usuarios para probar la aplicación. En este caso de ejemplo, cree dos espacios, uno para los desarrolladores de la aplicación y otro para sus probadores. A continuación, otorgue cada conjunto de acceso de usuarios al espacio correcto.

Al implementar una arquitectura con varias organizaciones, puede segregar cada organización mediante el LOB, el ciclo de vida de entrega, o ambos. A continuación, puede definir
varios espacios, que se basan en el número de apps o proyectos que entrega el mismo departamento de la empresa. Tenga en cuenta lo siguiente como guía cuando se planifican los espacios de una organización:

* Defina un espacio para alojar un servicio que necesite suministro y configuración sólo una vez en la organización.
* Defina un espacio por aplicación, por grupo de apps relacionadas, o por proyecto específico.
* Si necesita imponer límites para distintos usuarios, defina un espacio para cada conjunto de usuarios. Cuando a un usuario se le otorga un rol de desarrollador en un espacio, dicho usuario tendrá acceso completo a todos los recursos y servicios de {{site.data.keyword.Bluemix_notm}} suministrados y en ejecución en dicho espacio. Cuando necesite imponer una seguridad más estricta para impedir que los usuarios controlen todos los recursos, tenga en cuenta la posibilidad de definir distintos espacios. Dentro de cualquiera de estos espacios, puede suministrar servicios de {{site.data.keyword.Bluemix_notm}} que utilizarán las apps que se ejecutan en dicho espacio.

## Denominación, restricciones y gestión del espacio
{: #spaceadmin}

Para definir los distintos espacios para la organización de la nube, tenga en cuenta las siguientes instrucciones:

* Defina y aplique un convenio de denominación. Por ejemplo, defina un convenio de denominación donde el nombre de espacio incluya información sobre el lugar donde está ubicada la organización y el tipo de nube. Puede cambiar el nombre de un espacio una vez que se haya creado. Si se altera un nombre de espacio, notifique a todos los miembros del equipo del espacio sobre el cambio.
* Defina las restricciones que se aplican al espacio. Por ejemplo, defina el tipo de apps que se pueden desarrollar, gestionar y desplegar en cada espacio.
* Identifique al gestor del espacio. Es posible que desee delegar la administración del espacio a más de una persona.
