---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2019-01-15"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Permisos
{: #permissions}

Antes de que los usuarios empiecen a crear y trabajar con un servicio {{site.data.keyword.cfee_full}} (CFEE), el administrador de la cuenta donde se ha creado la instancia de CFEE deberá establecer correctamente sus permisos. 

## Visión general de los permisos
{: #perm-summary}

A continuación encontrará un resumen de las [asignaciones de roles de Cloud Foundry](https://cloud.ibm.com/account/cloud-foundry) y de [IAM](https://cloud.ibm.com/iam#/users) mínimas necesarias para realizar diversas tareas en una instancia de CFEE. En el resto de la sección se describen estos permisos con más detalle.

|  **Tarea** &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;|  **Roles de acceso de IAM** &nbsp; &nbsp; &nbsp; |**Roles de Cloud Foundry** &nbsp; &nbsp; &nbsp; |
|----------------------------------------|-------------------|-------------------|
|Crear un CFEE |  <ul><li>Rol de visor en el grupo de recursos en el que se va a crear CFEE.</li> <li>Rol de editor en el servicio CFEE.</li> <li>Rol de administrador en el servicio Kubernetes.</li> <li>Rol de editor en el servicio Cloud Object Storage.</li> </ul> | <ul><li>Rol de usuario en una organización pública.</li> <li>Rol de desarrollador en un espacio de dicha organización pública. </li></ul>|
|Actualizar la versión de CFEE |  <ul><li>Rol de visor en el grupo de recursos de CFEE.</li> <li>Rol de editor en el servicio CFEE.</li></li> <li>Rol de operador en el servicio Kubernetes.</li> <li>Rol de editor en el servicio Cloud Object Storage.</li> </ul> | <ul><li>Rol de usuario en una organización pública.</li> <li>Rol de desarrollador en un espacio de dicha organización pública. </li></ul>|
|Escalar la capacidad de CFEE (añadir/eliminar células)|  <ul><li>Rol de visor en el grupo de recursos de la instancia de CFEE.</li> <li>Rol de administrador en la instancia de CFEE.</li> <li>Rol de operador en el servicio Kubernetes.</li> <li>Rol de editor en el servicio Cloud Object Storage.</li> </ul> | |
|Supervisar CFEE |  <ul><li>Rol de visor en el grupo de recursos de la instancia de CFEE</li> <li>Rol de editor en la instancia de CFEE.</li></ul> |  |
|Ver el uso de recursos de CFEE |  <ul><li>Rol de visor en el grupo de recursos de la instancia de CFEE.</li> <li>Rol de visor en la instancia de CFEE.</li></ul> |  |
|Habilitar la auditoría de CFEE| <ul><li>Rol de visor en el grupo de recursos de la instancia de CFEE.</li> <li>Rol de editor en la instancia de CFEE.</li></ul> | <ul><li>Rol de auditor en el espacio público de Cloud Foundry en el que se ha desplegado la instancia del servicio Activity Tracker.</li></ul>  |
|Ver sucesos de auditoría de CFEE| <ul><li>Rol de visor en el grupo de recursos de la instancia de CFEE.</li> <li>Rol de editor en la instancia de CFEE.</li></ul> | <ul><li>Rol de auditor en el espacio público de Cloud Foundry en el que se ha desplegado la instancia del servicio Activity Tracker.</li></ul>  |
|Habilitar la persistencia de registro de CFEE| <ul><li>Rol de visor en el grupo de recursos de la instancia de CFEE</li> <li>Rol de editor en la instancia de CFEE.</li></ul> |<ul><li>Rol de auditor en el espacio público de Cloud Foundry en el que se ha desplegado la instancia del servicio Log Analysis.</li></ul>  |
|Ver registros permanentes de CFEE| <ul><li>Rol de visor en el grupo de recursos de la instancia de CFEE</li> <li>Rol de editor en la instancia de CFEE.</li></ul> | <ul><li>Rol de auditor en el espacio público de Cloud Foundry en el que se ha desplegado la instancia del servicio Log Analysis.</li></ul> |
|Crear organizaciones de CFEE| <ul><li>Rol de visor en el grupo de recursos de la instancia de CFEE</li> <li>Rol de editor en la instancia de CFEE.</li></ul> |  |
|Crear espacios de CFEE| <ul><li>Rol de visor en el grupo de recursos de la instancia de CFEE</li> <li>Rol de visor en la instancia de CFEE.</li></ul> | <ul><li>Gestor en la organización en la que se va a crear el espacio.</li></ul> |
|Gestionar dominios compartidos|<ul><li>Visor en el grupo de recursos de la instancia de CFEE. </li><li>Rol de editor en la instancia de CFEE. </li></ul>|  |
|Ver dominios compartidos|<ul><li>Visor en el grupo de recursos de la instancia de CFEE. </li><li>Rol de visor en la instancia de CFEE. </li></ul>|  |
|Gestionar dominios privados|<ul> <li>Visor en el grupo de recursos de la instancia de CFEE. </li><li>Rol de visor en la instancia de CFEE. </li></ul>| <ul><li>Rol de gestor en la organización propietaria del dominio. </li></ul>|
|Ver dominios privados|<ul> <li>Visor en el grupo de recursos de la instancia de CFEE </li><li>Rol de visor en la instancia de CFEE. </li></ul>|<ul><li>Rol de visor en la organización propietaria del dominio. </li></ul>|
|Crear/suprimir una instancia de servicio de IBM Cloud en un espacio de CFEE| <ul><li>Rol de visor en el grupo de recursos en el que se va a crear CFEE.</li> <li>Rol de visor en la instancia de CFEE.</li> <li>Editor en el grupo de recursos en el que se va a crear la instancia de servicio o en el servicio gestionado por IAM del que se va a crear una instancia.</li> </ul>| <ul><li>Rol de desarrollador en el espacio de CFEE desde donde se crea la instancia de servicio (y donde se añadirá/se creará alias automáticamente).</li></ul> |
|Añadir/eliminar una instancia de servicio de IBM Cloud a/de un espacio de CFEE (es decir, crear/suprimir un alias para un servicio de IBM Cloud en un espacio CFEE)| <ul><li>Rol de visor en el grupo de recursos de la instancia de CFEE.</li><li>Rol de visor en la instancia de CFEE. </li><li>Rol de plataforma de operador y rol de servicio de lector en la instancia de servicio que se va a añadir. </li></ul>|<ul><li>Rol de desarrollador en el espacio CFEE en el que se va a añadir la instancia de servicio (alias).</li></ul> |
|Enlazar o desenlazar una instancia de servicio de IBM Cloud en un espacio CFEE|<ul> <li>Editor en el grupo de recursos de la instancia de servicio que se va a enlazar o desenlazar.</li><li>Rol de visor en la instancia de CFEE. </li><li>Rol de plataforma de operador y rol de servicio de escritor en la instancia de servicio que se va a enlazar.</li></ul> | <ul><li>Rol de desarrollador en el espacio de CFEE donde se enlazan la instancia de servicio.</li></ul> |
|Emitir mandatos de cli `cf`|<ul> <li>Rol de visor en el grupo de recursos de la instancia de CFEE. </li><li>Rol de visor en la instancia de CFEE.</li></ul> | <ul><li>Los roles de Cloud Foundry en la organización/espacio necesarios para ejecutar el mandato.</li></ul> |
{: caption="Tabla 1. Permisos necesarios para realizar tareas en un CFEE" caption-side="top"}

## Permisos necesarios para crear un nuevo entorno
{: #perm-creating}

Para crear nuevas instancias del servicio CFEE, es necesario que el administrador de la cuenta otorgue políticas de acceso a los usuarios, no solo al servicio CFEE, sino también a los servicios de soporte que también se crean automáticamente cuando se crea el servicio CFEE.

Las siguientes políticas de acceso de Identity & Access Management (IAM) son necesarias para que los usuarios puedan crear una instancia de {{site.data.keyword.cfee_full_notm}}:

* Acceso de _Visor_ (o superior) al **Grupo de recursos** **_predeterminado_** en la cuenta de {{site.data.keyword.Bluemix}}. Los grupos de recursos permiten la organización de recursos en grupos personalizados para facilitar el control de acceso a dichos recursos. Cuando crea la nueva instancia del entorno, se le solicita un grupo de recursos. El acceso al grupo de recursos de _Valor predeterminado_ es necesario porque siempre es el grupo de recursos en el que se necesita el clúster de Kubernetes.  Los usuarios pueden suministrar la instancia CFEE en un grupo de recursos diferente, pero el clúster de Kubernetes se seguirá suministrando en el grupo de recursos de _Valor predeterminado_.  Si un usuario suministra el servicio CFEE en un grupo de usuarios diferente, los usuarios necesitarán el acceso de visor en dicho grupo de recursos.

* Rol de _administrador_ o _editor_ sobre los recursos del **servicio {{site.data.keyword.cfee_full_notm}}**. En el grupo de recursos al que se asigna el entorno. Los usuarios con los roles de administrador o editor en el servicio de {{site.data.keyword.cfee_full_notm}} pueden crear y suprimir entornos. Pero únicamente los usuarios con un rol de administración pueden asignar usuarios a una instancia de {{site.data.keyword.cfee_full_notm}} o cambiar los roles que se asignan a los usuarios de dicha instancia.
   
* Rol de _administrador_ sobre los recursos del **servicio Kubernetes**.  Las instancias de {{site.data.keyword.cfee_full_notm}} se despliegan en la infraestructura de clúster del contenedor, proporcionada por el servicio Kubernetes. Cuando crea una instancia de servicio de {{site.data.keyword.cfee_full_notm}}, el servicio crea automáticamente un clúster de Kubernetes. El acceso al servicio Kubernetes es necesario para la infraestructura de clúster. Puede ampliar el acceso a la política de servicio Kubernetes a la región específica en la que pretende aprovisionar la instancia de CFEE, o ampliar el acceso a todas las regiones.

* Rol de _administrador_ o _editor_ y rol de gestor de acceso a servicios sobre el servicio **IBM Cloud Object Storage**, que es una dependencia necesaria del servicio CFEE.  Se utiliza una instancia del servicio de IBM Cloud Object Storage para almacenar datos generados durante la creación de los contenedores de su aplicación ICFEE (p. ej. paquetes de aplicación cargados, paquetes de compilación y ejecutables compilados).

* Una instancia del servicio Compose for PostgreSQL es una dependencia necesaria del servicio CFEE.  Compose for PostgreSQL se utiliza para almacenar los datos de Cloud Foundry en su instancia de CFEE (p. ej. la auditoría del despliegue de aplicación, inicio y detención de sucesos; y el mantenimiento de registros de la pertenencia de usuarios de CFEE, organizaciones, espacios, aplicaciones y conexiones de servicio).  La instancia del **servicio de Compose for PostgreSQL** se despliega en un espacio dentro de una organización de Cloud Foundry pública (no está relacionada con las organizaciones de CFEE) que selecciona al crear una instancia de {{site.data.keyword.cfee_full_notm}}.  Esto significa que cuando crea una instancia de {{site.data.keyword.cfee_full_notm}} debe tener acceso de _gestor_ como mínimo a una organización en la ubicación en la que tiene previsto suministrar la instancia de CFEE.  También necesitará acceso de _desarrollador_ a, al menos, un espacio en dicha organización. 

  Si no es miembro de al menos una organización pública en la ubicación en la que pretende crear una instancia de CFEE, solicite a un administrador de IBM Cloud que le invite a una. Si tiene un rol de administrador en la cuenta, podrá añadir usuarios a organizaciones y espacios públicos de la cuenta realizando lo siguiente:

     * Vaya a [**Gestionar > Cuenta > Organizaciones de Cloud Foundry**](https://console.bluemix.net/account/organizations) y pulse **Añadir una organización** o seleccione una organización existente.
     * Vaya al separador **Usuarios** en la parte superior de la página de la organización.
     * Busque el usuario que necesita crear instancias de CFEE. Si el usuario con el que desea crear instancias de CFEE no está en la lista, pulse **Añadir o invitar usuario** sobre la tabla para añadir o invitar usuarios a la organización.
     * Vaya al separador **Espacios** en la parte superior de la página de la organización.
     * Busque el espacio en el que se suministrará la instancia del servicio de Compose for PostgreSQL y marque el recuadro de selección el rol **Desarrollador**.

La pantalla siguiente muestra las políticas de acceso tal y como aparecerían en la página Identidad y acceso de {{site.data.keyword.Bluemix_notm}} que permiten a un usuario crear una instancia de {{site.data.keyword.cfee_full_notm}}.

![Políticas de acceso](img/AccessPolicies_Creator.png)

Puede otorgar permisos de usuario utilizando la línea de mandatos de {{site.data.keyword.Bluemix}}.  También puede definir una política de acceso para un usuario especificando los parámetros de la política (es decir, servicios, roles, regiones, etc) en un archivo con formato JSON que se invoca mediante el mandato que crea la política.  Consulte [Asignación de una política de IAM mediante la línea de mandatos](https://console.bluemix.net/docs/services/cloud-monitoring/security/assign_policy.html#assign_policy_commandline) para obtener más información o bien emita el mandato `ibmcloud iam -help` en la línea de mandatos. Tenga en cuenta que esto requiere que se instale la [CLI de IBM Cloud](https://console.bluemix.net/docs/cli/reference/ibmcloud/download_cli.html#install_use).
{:tip}

Para confirmar que dispone de las políticas de acceso necesarias para crear una instancia de {{site.data.keyword.cfee_full_notm}}:
1. Vaya al menú [**Gestionar > Acceso (IAM) > Usuarios**](https://console.bluemix.net/iam/#/users) en la cabecera de {{site.data.keyword.Bluemix_notm}} para abrir la página **Identidad y acceso**.
2. En el separador Políticas de acceso, pulse el usuario que está creando el entorno para asignar y ver las políticas de acceso de ese usuario.

Para obtener más información sobre la gestión de usuarios y de acceso en {{site.data.keyword.Bluemix}}, incluido cómo organizar un conjunto de usuarios e ID de servicio para facilitar la asignación de acceso a varios usuarios a la vez, consulte [Gestión de usuarios y de acceso](https://console.bluemix.net/docs/iam/iamusermanage.html#iamusermanage).

### Aceleración del establecimiento de permisos para crear un entorno utilizando la CLI
{: #permcli-creating}

Puede acelerar el establecimiento de permisos para crear instancias de CFEE con `ibmcloud cfee create-permission-set`.  El mandato permite a un administrador de CFEE configurar en un solo mandato las políticas de acceso necesarias para crear una instancia de CFEE y todos sus servicios auxiliares. 

El mandato establece los permisos a un _Grupo de acceso_ de IAM y añade un usuario a dicho _Grupo de acceso_.  El administrador que emite el mandato puede incluir en el mandato un _Grupo de acceso_ existente.  Si no se especifica ningún _Grupo de acceso_, se crea automáticamente un _cfee-provision-access-group_ predeterminado.

```
ibmcloud cfee create-permission-set USER_NAME [-ag, --access-group GROUP_NAME] [--output TYPE]
```
{: pre}

El mandato establece las siguientes políticas de acceso para el usuario de destino:

*  Roles de editor para los servicios de Cloud Object Storage y CFEE en la cuenta actual de IBM Cloud.
*  Rol de administrador para el servicio Kubernetes en la cuenta de IBM Cloud actual.
*  Rol de desarrollador para el espacio actual en la organización actual para el suministro de Compose for PostgreSQL.

Para obtener más detalles sobre el mandato, emita lo siguiente:

```
cfee create-permission-set -help
```
{: pre}

Puede utilizar `ibmcloud cfee create-permission-get` para averiguar o validar las políticas de acceso en vigor para un usuario:

```
ibmcloud cfee provision-permission-get USER_NAME [-ag, --access-group GROUP_NAME] [--output TYPE]
```
{: pre}

## Permisos necesarios para trabajar con un entorno
{: #perm-working}

Para trabajar con una instancia de {{site.data.keyword.cfee_full_notm}}, los usuarios deben ser:
1. Miembros de la cuenta de {{site.data.keyword.Bluemix_notm}} en la que se creó la instancia de {{site.data.keyword.cfee_full_notm}}.
2. El administrador de la cuenta otorgó las siguientes _Políticas de acceso_ de IAM (consulte la página _Identidad y acceso_ en el menú [**Gestionar > Acceso (IAM) > Usuarios**](https://console.bluemix.net/iam/#/users) en la cabecera de {{site.data.keyword.Bluemix_notm}} para verificar las políticas de acceso de cuenta actuales):

    Cualquier usuario que trabaje en una instancia de CFEE necesita un rol de plataforma de _visor_ (o superior) en:
  - El grupo de recursos bajo el que se ha creado la instancia de CFEE.
  - La propia instancia de CFEE. 
  
   El nivel de acceso y control que los usuarios tienen en una instancia de CFEE depende del rol que se otorgue en las políticas de acceso:

  - Los usuarios con el rol de _visor_ sobre una instancia de CFEE pueden verla en la lista del panel de control principal de {{site.data.keyword.Bluemix_notm}} y abrir su interfaz de usuario. El acceso de los usuarios a organizaciones y espacios específicos en un entorno lo controlan los roles de dichos espacios y organizaciones, que están asignados por los gestores de los mismos. Para obtener más información, consulte [Adición de usuarios a organizaciones](add-users.html).
  
  - Los usuarios con los roles de _administrador_ o de _editor_ sobre una instancia de CFEE pueden crear organizaciones, asignar gestores a organizaciones y espacios, tener permisos a todas las organizaciones y espacios del entorno y realizar acciones operativas mediante la API del controlador de nube. Estos usuarios automáticamente tienen el _ámbito cloud_controller.admin_ en el _ámbito Cuenta de usuario y autenticación_ de Cloud Foundry.

  - Los usuarios necesitan el rol de plataforma de _editor_ o superior sobre una instancia CFEE y el rol de _operador_ o superior sobre el clúster Kubernetes en el que se aprovisiona el CFEE para poder **actualizar el CFEE a una nueva versión**.

  - Los usuarios necesitan el rol de plataforma de _administrador_ sobre en una instancia CFEE y el rol de _operador_ o superior sobre el clúster de Kubernetes en el que se suministra CFEE para poder **cambiar la capacidad** de un cfee (añadir o eliminar células).
 
  - Los usuarios necesitan el rol de plataforma de _operador_ (o superior) sobre una instancia de servicio de IBM Cloud para poder **añadir** dicha *instancia de servicio* a un espacio CFEE (es decir, para crear un alias de una instancia de servicio en un espacio de CFEE).
 
  - Los usuarios necesitan el rol de plataforma de _operador_ (o superior) y el rol de servicio de _escritor_ (o superior) sobre una instancia de servicio de IBM Cloud para poder **enlazar** dicha instancia de servicio a una aplicación desplegada en un espacio de CFEE.


## Prácticas recomendadas: grupos de acceso
{: #access-groups}

Supongamos que se utilizan grupos de acceso para gestionar y simplificar el control de acceso para su CFEE.  Los grupos de acceso le permiten definir grupos arbitrarios a los que puede asignar políticas de acceso.  A cualquier usuario que se añada a un grupo de acceso se le asigna automáticamente la política de acceso del grupo. 

Puede crear y gestionar grupos de acceso desde la interfaz de usuario de IBM Cloud o desde la cli `ibmcloud`. 

Desde la interfaz de usuario, vaya a la barra de menús, pulse **Gestionar > Acceso (IAM)** y seleccione [Grupos de acceso](https://cloud.ibm.com/iam#/groups).

Como alternativa, puede utilizar la cli `ibmcloud`:

1. Cree un grupo de acceso:

  ```
  ibmcloud iam access-group-create GROUP_NAME [-d, --description DESCRIPTION]
```
  {: pre}

2. Cree una política de acceso para dicho grupo de acceso:

  ```
  ibmcloud iam access-group-policy-create GROUP_NAME
  ```
  {: pre}

3. Añada usuarios al grupo de acceso:

  ```
  ibmcloud iam access-group-user-add <user-name> [<user-name2...]
  ```
  {: pre}

<br>
Para obtener más información, consulte [Configuración de grupos de acceso](https://cloud.ibm.com/docs/iam/groups.html#groups).
