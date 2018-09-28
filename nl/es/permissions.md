---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-04-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Permisos
{: #permissions}

Antes de empezar a crear y a trabajar con instancias de servicio de {{site.data.keyword.cfee_full}}, deben establecerse correctamente los permisos del administrador y del resto del equipo.

## Permisos necesarios para crear un nuevo entorno
{: #perm-creating}

Para crear nuevas instancias de servicio de {{site.data.keyword.cfee_full_notm}}, es necesario que el administrador de la cuenta en la que se debe crear la instancia otorgue políticas de acceso a los usuarios:

* Acceso, como mínimo, a un grupo de recursos en la cuenta de {{site.data.keyword.Bluemix}}. Los grupos de recursos permiten la organización de recursos en grupos personalizados para facilitar el control de acceso a dichos recursos. Cuando crea la nueva instancia del entorno, se le solicita un grupo de recursos.

* Rol de administrador o editar para el servicio de {{site.data.keyword.cfee_full_notm}} en el grupo de recursos en el que se asigna el entorno. Los usuarios con los roles de administrador o editor en el servicio de {{site.data.keyword.cfee_full_notm}} pueden crear y suprimir entornos. Pero únicamente los usuarios con un rol de administración pueden asignar usuarios a una instancia de {{site.data.keyword.cfee_full_notm}} o cambiar los roles que se asignan a los usuarios de dicha instancia.

* Rol de administrador o editor en el servicio de IBM Cloud Object Storage, que es una dependencia necesaria del servicio CFEE.  Se utiliza una instancia del servicio de IBM Cloud Object Storage para almacenar datos generados durante la creación de los contenedores de su aplicación ICFEE (p. ej. paquetes de aplicación cargados, paquetes de compilación y ejecutables compilados).

* Una instancia del servicio Compose for PostgreSQL es una dependencia necesaria del servicio CFEE.  Compose for PostgreSQL se utiliza para almacenar los datos de Cloud Foundry en su instancia de CFEE (p. ej. la auditoría del despliegue de aplicación, inicio y detención de sucesos; y el mantenimiento de registros de la pertenencia de usuarios de CFEE, organizaciones, espacios, aplicaciones y conexiones de servicio).  La instancia de un servicio Compose for PostgreSQL se despliega en una organización de Cloud Foundry pública (no relacionada a organizaciones de CFEE). La organización pública de Cloud Foundry en la que se despliega la instancia de Compose for PostgreSQL tiene un nombre específico: **_cfee-`<accountId>`_**, donde "accountID" es el ID de la cuenta de IBM Cloud en la que se debe proporcionar el CFEE (junto con la instancia de servicio de Compose for PostgreSQL).  La organización de Cloud Foundry pública se crea automáticamente cuando el propietario de la cuenta crea una instancia de CFEE.  La organización no se crea automáticamente cuando un usuario que no es el propietario de la cuenta intenta crear la instancia de CFEE (por lo tanto, el intento de creación del CFEE fallará).  Por consiguiente, cualquier usuario de la cuenta de IBM Cloud que cree instancias de CFEE, pero que no sea el propietario de la cuenta, se debe añadir en la organización de Cloud Foundry pública de **_cfee-`<accountId>`_** mediante un **rol de gestor**.   

   Para añadir un usuario de la cuenta de IBM Cloud a la organización pública de _cfee-`<accountId>`_:
    * Vaya a [**Gestionar > Cuenta > Organizaciones de Cloud Foundry**](https://console.bluemix.net/account/organizations).
    * Pulse la organización **_cfee-`<accountId>`_**.
    * Vaya al separador **Usuarios** en la parte superior de la página.
    * Busque el usuario que necesita crear instancias de CFEE y pulse el recuadro de selección **Gestor** para dicho usuario. Si el usuario con el que desea poder crear instancias de CFEE no está en la lista, pulse **Añadir o invitar usuario** en la parte superior de la tabla para añadir o invitar usuarios a la organización **_cfee-`<accountId>`_**.

   **Nota**: Aunque la organización pública **_cfee-`<accountId>`_** se crea de forma automática e implícita cuando el propietario de la cuenta de IBM Cloud crea una instancia de CFEE, el propietario de la cuenta (y únicamente el propietario de la cuenta) puede crear, en su lugar, la organización de Cloud Foundry pública de forma manual, sin la necesidad de crear una instancia de CFEE. El propietario de la cuenta de IBM Cloud puede crear la organización _cfee-`<accountId>`_ pública de forma manual en la página **Gestionar > Cuenta > Organizaciones de Cloud Foundry**. Si es el propietario de la cuenta y crea la organización _cfee-`<accountId>`_ pública, asegúrese de que el nombre es exactamente _cfee-`<accountId>`_. Para buscar el ID de cuenta de IBM Cloud, vaya a la página [**Gestionar > Cuenta > Organizaciones de Cloud Foundry**](https://console.bluemix.net/account/organizations) y busque el URL disponible en el navegador.  El ID de cuenta de IBM Cloud es el conjunto de valores alfanuméricos que siguen al signo `=` en el URL de la página. De forma alternativa, puede ir a __Gestionar > Cuenta > Usuarios__ y pasar el cursor sobre la ayuda contextual en la parte izquierda del nombre _Cuenta_ ubicado en la esquina superior derecha de la página.
   
* Rol de administrador o editar para el servicio de contenedor de {{site.data.keyword.Bluemix_notm}} en el grupo de recursos en el que se asigna el entorno. Las instancias de {{site.data.keyword.cfee_full_notm}} se despliegan en la infraestructura de clúster del contenedor, proporcionada por el servicio de contenedor de {{site.data.keyword.Bluemix_notm}}. Cuando crea una instancia de servicio de {{site.data.keyword.cfee_full_notm}}, el servicio crea automáticamente un clúster de Kubernetes en el que se despliega {{site.data.keyword.cfee_full_notm}}. El acceso al servicio de IBM Container, específicamente en el grupo de recursos en el que se asigna el entorno, es necesario para crear la infraestructura del clúster.

Para confirmar que dispone de las políticas de acceso necesarias para crear una instancia de {{site.data.keyword.cfee_full_notm}}:
1. Vaya al menú [**Gestionar > Cuenta > Usuarios**](https://console.bluemix.net/iam/#/users) en la cabecera de {{site.data.keyword.Bluemix_notm}} para abrir la página **Identidad y acceso**.
2. En el separador Políticas de acceso, pulse en el usuario que está creando el entorno.
3. Confirme que las políticas de acceso para el usuario que está creando el entorno son coherentes con las políticas descritas anteriormente.

La pantalla siguiente muestra las políticas de acceso tal y como aparecerían en la página Identidad y acceso de {{site.data.keyword.Bluemix_notm}} que permiten a un usuario crear una instancia de {{site.data.keyword.cfee_full_notm}}.

![Políticas de acceso](img/AccessPolicies_Creator.png)

## Permisos necesarios para trabajar con un entorno
{: #perm-working}

Para trabajar con una instancia de {{site.data.keyword.cfee_full_notm}}, los usuarios deben ser:
1. Miembros de la cuenta de {{site.data.keyword.Bluemix_notm}} en la que se creó la instancia de {{site.data.keyword.cfee_full_notm}}.
2. Usuarios con _Políticas de acceso_ otorgadas por el administrador de la cuenta (consulte la página _Identidad y acceso_ en el menú [**Gestionar > Cuenta > Usuarios**](https://console.bluemix.net/iam/#/users) en la cabecera de {{site.data.keyword.Bluemix_notm}} para verificar las políticas de acceso actuales de su cuenta):
  - Acceso, como mínimo, a un grupo de recursos en la cuenta de {{site.data.keyword.Bluemix_notm}}. Los grupos de recursos permiten la organización de recursos en grupos personalizados para facilitar el control de acceso a dichos recursos. Cuando crea la nueva instancia del entorno, se le solicita un grupo de recursos.
  - Los usuarios deben tener asignado el acceso al servicio de {{site.data.keyword.cfee_full_notm}} en el grupo de recursos en el que se ha creado la instancia del entorno. El nivel de acceso y control que los usuarios tienen en una instancia de {{site.data.keyword.cfee_full_notm}} depende del rol que se ha otorgado en la política de acceso:
     - Los usuarios con los roles de administrador o editor pueden crear organizaciones, asignar gestores a organizaciones y espacios, tener permisos a todas las organizaciones y espacios del entorno y realizar acciones operativas utilizando la API del controlador de nube. Estos usuarios automáticamente tienen el _ámbito cloud_controller.admin_ en el _ámbito Cuenta de usuario y autenticación_ de Cloud Foundry.
     - Los usuarios con el rol de visor pueden ver el entorno en el panel de control de {{site.data.keyword.Bluemix_notm}} principal y pueden abrir la interfaz de usuario. El acceso de los usuarios a organizaciones y espacios específicos en un entorno lo controlan los roles de dichos espacios y organizaciones, que están asignados por los gestores de los mismos. Para obtener más información, consulte [Adición de usuarios a organizaciones](add-users.html).

La imagen muestra las políticas de acceso mínimas (tal y como aparecerían en la página {{site.data.keyword.Bluemix_notm}} _Identidad y acceso_) necesarias para acceder a un {{site.data.keyword.cfee_full_notm}}.

![Políticas de acceso](img/AccessPolicies_User.png)

