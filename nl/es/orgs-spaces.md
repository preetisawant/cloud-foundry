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

# Creación de organizaciones y espacios
{: #create_orgs}

Las apps de {{site.data.keyword.cfee_full}} abarcan espacios específicos. A su vez, el espacio existe en una organización específica. Los miembros de una organización comparten un plan de cuotas, apps, instancias de servicio y dominios personalizados. Una vez se hayan creado espacios y organizaciones, es posible añadir a los usuarios con roles específicos que determinan el nivel de acceso y control a dichas organizaciones y espacios. Para crear organizaciones y asignar gestores a dichas organizaciones, necesita un rol de administrador para el servicio {{site.data.keyword.cfee_full_notm}} y para la instancia de entorno específica a la que se añaden los usuarios. Estos permisos se establecen en la página _Identidad y acceso_ en el menú **Gestionar > Usuarios** en la cabecera de {{site.data.keyword.Bluemix}}.
{: shortdesc}

## Creación de organizaciones
{: #create-org}

Para crear organizaciones en {{site.data.keyword.cfee_full_notm}}:

1. Vaya al [panel de control de {{site.data.keyword.Bluemix_notm}} Cloud Foundry Environments](https://cloud.ibm.com/dashboard/cloudfoundry?filter=cf_environments){: new_window} y abra el {{site.data.keyword.cfee_full_notm}} en el que desea crear organizaciones.
2. En la interfaz de usuario de {{site.data.keyword.cfee_full_notm}}, vaya a la entrada **Organizaciones** en el panel de navegación para abrir la página _Organizaciones_.
3. Pulse **Añadir nuevo**.
4. Escriba un **Nombre** para la nueva organización.
5. En **Gestores**, identifique al menos un usuario. Solo los usuarios con un rol de Gestor pueden añadir miembros a dicha organización.
6. En **Plan de cuotas**, seleccione un plan disponible. Un plan de cuotas limita la memoria disponible para las apps de la organización, el número máximo de instancias de app alojadas y el número máximo de rutas.

Además de gestionar la pertenencia a una organización, los gestores de organización pueden crear, visualizar, editar o suprimir espacios en la organización. Los gestores de organización también pueden visualizar la cuota y el uso de la organización, invitar usuarios a la organización, gestionar los roles y la pertenencia a la organización y gestionar los dominios personalizados para la organización.

Para crear espacios en la organización, en la página _Organizaciones_, vaya al separador **Espacios** y pulse **Añadir nuevo**. Los miembros de una organización también pueden crear y gestionar sus propios espacios en una organización. Para obtener más información sobre los roles de Cloud Foundry, consulte [Acceso de Cloud Foundry](https://cloud.ibm.com/docs/iam/cfaccess.html#cfroles){: new_window}.

**Nota**: El acceso a organizaciones y espacios en {{site.data.keyword.cfee_full_notm}} requiere que los usuarios tengan permiso para acceder al entorno. Sin el permiso de acceso a {{site.data.keyword.cfee_full_notm}}, los usuarios no pueden acceder a organizaciones y espacios del entorno, independientemente de su rol y pertenencia a dichas organizaciones y espacios.
