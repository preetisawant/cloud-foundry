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

Antes de que los usuarios empiecen a crear y trabajar con las instancias del servicio de {{site.data.keyword.cfee_full}}, el administrador de la cuenta donde se ha creado la instancia deberá establecer correctamente sus permisos. 

## Permisos necesarios para crear un nuevo entorno
{: #perm-creating}

Para crear nuevas instancias del servicio CFEE, es necesario que el administrador de la cuenta otorgue políticas de acceso a los usuarios, no solo al servicio CFEE, sino también a los servicios de soporte que también se crean automáticamente cuando se crea el servicio CFEE.

Las siguientes políticas de acceso de Identity & Access Management (IAM) son necesarias para que los usuarios puedan crear una instancia de {{site.data.keyword.cfee_full_notm}}:

* Acceso de _Visor_ (o superior) al **Grupo de recursos** **_predeterminado_** en la cuenta de {{site.data.keyword.Bluemix}}. Los grupos de recursos permiten la organización de recursos en grupos personalizados para facilitar el control de acceso a dichos recursos. Cuando crea la nueva instancia del entorno, se le solicita un grupo de recursos. El acceso al grupo de recursos de _Valor predeterminado _ es necesario porque siempre es el grupo de recursos en el que se necesita el clúster de Kubernetes.  Los usuarios pueden suministrar la instancia CFEE en un grupo de recursos diferente, pero el clúster de Kuberetes se seguirá suministrando en el grupo de recursos de _Valor predeterminado_.  Si un usuario suministra el servicio CFEE en un grupo de usuarios diferente, los usuarios necesitarán el acceso de visor en dicho grupo de recursos.

* Rol de editor o administrador para los recursos de **servicio {{site.data.keyword.cfee_full_notm}}** en el grupo de recursos en el que se asigna un entorno. Los usuarios con los roles de administrador o editor en el servicio de {{site.data.keyword.cfee_full_notm}} pueden crear y suprimir entornos. Pero únicamente los usuarios con un rol de administración pueden asignar usuarios a una instancia de {{site.data.keyword.cfee_full_notm}} o cambiar los roles que se asignan a los usuarios de dicha instancia.
   
* Rol de administrador para los recursos de **Servicio Kubernetes**.  Las instancias de {{site.data.keyword.cfee_full_notm}} se despliegan en la infraestructura de clúster del contenedor, proporcionada por el servicio Kubernetes. Cuando crea una instancia de servicio de {{site.data.keyword.cfee_full_notm}}, el servicio crea automáticamente un clúster de Kubernetes. El acceso al servicio Kubernetes es necesario para la infraestructura de clúster. Puede ampliar el acceso a la política de servicio Kubernetes a la región específica en la que pretende aprovisionar la instancia de CFEE, o ampliar el acceso a todas las regiones.

* Rol de administrador o editor en el servicio de **IBM Cloud Object Storage**, que es una dependencia necesaria del servicio CFEE.  Se utiliza una instancia del servicio de IBM Cloud Object Storage para almacenar datos generados durante la creación de los contenedores de su aplicación ICFEE (p. ej. paquetes de aplicación cargados, paquetes de compilación y ejecutables compilados).

* Una instancia del servicio Compose for PostgreSQL es una dependencia necesaria del servicio CFEE.  Compose for PostgreSQL se utiliza para almacenar los datos de Cloud Foundry en su instancia de CFEE (p. ej. la auditoría del despliegue de aplicación, inicio y detención de sucesos; y el mantenimiento de registros de la pertenencia de usuarios de CFEE, organizaciones, espacios, aplicaciones y conexiones de servicio).  La instancia del **servicio de Compose for PostgreSQL** se despliega en un espacio dentro de una organización de Cloud Foundry pública (no está relacionada con las organizaciones de CFEE) que selecciona al crear una instancia de {{site.data.keyword.cfee_full_notm}}.  Esto significa que cuando crea una instancia de {{site.data.keyword.cfee_full_notm}} debe tener acceso de gestor como mínimo a una organización en la ubicación en la que tiene previsto suministrar la instancia de CFEE.  También necesitará acceso de desarrollador a, al menos, un espacio en dicha organización. 

  Si no es miembro de al menos una organización pública en la ubicación en la que pretende crear una instancia de CFEE, solicite a un administrador de IBM Cloud que le invite a una. Si tiene un rol de administrador en la cuenta, podrá añadir usuarios a organizaciones y espacios públicos de la cuenta realizando lo siguiente:

     * Vaya a [**Gestionar > Cuenta > Organizaciones de Cloud Foundry**](https://console.bluemix.net/account/organizations) y pulse **Añadir una organización** o seleccione una organización existente.
     * Vaya al separador **Usuarios** en la parte superior de la página de la organización.
     * Busque el usuario que necesita crear instancias de CFEE. Si el usuario con el que desea crear instancias de CFEE no está en la lista, pulse **Añadir o invitar usuario** sobre la tabla para añadir o invitar usuarios a la organización.
     * Vaya al separador **Espacios** en la parte superior de la página de la organización.
     * Busque el espacio en el que se suministrará la instancia del servicio de Compose for PostgreSQL y marque el recuadro de selección el rol **Desarrollador**.

La pantalla siguiente muestra las políticas de acceso tal y como aparecerían en la página Identidad y acceso de {{site.data.keyword.Bluemix_notm}} que permiten a un usuario crear una instancia de {{site.data.keyword.cfee_full_notm}}.

![Políticas de acceso](img/AccessPolicies_Creator.png)

Para confirmar que dispone de las políticas de acceso necesarias para crear una instancia de {{site.data.keyword.cfee_full_notm}}:
1. Vaya al menú [**Gestionar > Cuenta > Usuarios**](https://console.bluemix.net/iam/#/users) en la cabecera de {{site.data.keyword.Bluemix_notm}} para abrir la página **Identidad y acceso**.
2. En el separador Políticas de acceso, pulse el usuario que está creando el entorno para asignar y ver las políticas de acceso de ese usuario.

## Permisos necesarios para trabajar con un entorno
{: #perm-working}

Para trabajar con una instancia de {{site.data.keyword.cfee_full_notm}}, los usuarios deben ser:
1. Miembros de la cuenta de {{site.data.keyword.Bluemix_notm}} en la que se creó la instancia de {{site.data.keyword.cfee_full_notm}}.
2. El administrador de la cuenta otorgó las siguientes _Políticas de acceso_ de IAM (consulte la página _Identidad y acceso_ en el menú [**Gestionar > Cuenta > Usuarios**](https://console.bluemix.net/iam/#/users) en la cabecera de {{site.data.keyword.Bluemix_notm}} para verificar las políticas de acceso de cuenta actuales):

  - Acceso al servicio de {{site.data.keyword.cfee_full_notm}} en el grupo de recursos bajo el que se ha creado la instancia de entorno. El nivel de acceso y control que los usuarios tienen en una instancia de {{site.data.keyword.cfee_full_notm}} depende del rol que se ha otorgado en la política de acceso:
     - Los usuarios con los roles de administrador o editor pueden crear organizaciones, asignar gestores a organizaciones y espacios, tener permisos a todas las organizaciones y espacios del entorno y realizar acciones operativas utilizando la API del controlador de nube. Estos usuarios automáticamente tienen el _ámbito cloud_controller.admin_ en el _ámbito Cuenta de usuario y autenticación_ de Cloud Foundry.
     - Los usuarios con el rol de visor pueden ver el entorno en el panel de control de {{site.data.keyword.Bluemix_notm}} principal y pueden abrir la interfaz de usuario. El acceso de los usuarios a organizaciones y espacios específicos en un entorno lo controlan los roles de dichos espacios y organizaciones, que están asignados por los gestores de los mismos. Para obtener más información, consulte [Adición de usuarios a organizaciones](add-users.html).

La imagen muestra las políticas de acceso mínimas (tal y como aparecerían en la página {{site.data.keyword.Bluemix_notm}} _Identidad y acceso_) necesarias para acceder a un {{site.data.keyword.cfee_full_notm}}.

![Políticas de acceso](img/AccessPolicies_User.png)

