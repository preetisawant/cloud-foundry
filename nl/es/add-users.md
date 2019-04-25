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

# Adición de usuarios a organizaciones y espacios
{: #adding_users}

Los miembros de una organización con el rol de gestor pueden añadir miembros a dicha organización. Para poder añadir usuarios a una organización, deben tener el rol de visor en el servicio {{site.data.keyword.cfee_full}} y en el grupo de recursos al que pertenece la instancia de {{site.data.keyword.cfee_full_notm}}. Estos permisos se establecen en la página _Identidad y acceso_ en **Gestionar > Usuarios** en la cabecera de {{site.data.keyword.Bluemix}}.

Para añadir usuarios como miembros de una organización en una instancia de {{site.data.keyword.cfee_full_notm}}:

1. Vaya a la entrada **Organizaciones** en el panel de navegación. Localice la organización en la que desea añadir un miembro. Vaya al menú _Acciones_ en la fila de tabla y seleccione **Añadir miembro**. De forma alternativa, puede pulsar en la organización para abrir la página de la organización, ir al separador **Miembros** y pulsar en **Añadir miembro**.
2. En la ventana _Añadir miembro_, busque el usuario, seleccione un **Rol de organización** y pulse **Añadir**.

**Nota:** Si desea añadir un usuario al que se ha invitado a la cuenta de {{site.data.keyword.Bluemix_notm}} recientemente, es posible que el proceso de reconocimiento del usuario en la ventana en la que añade usuarios a una organización o espacio tarde varios minutos. Si el usuario no se reconoce cuando introduce el nombre de usuario, especifique la dirección de correo electrónico del mismo y pulse el icono más (+) para añadirlo.

Únicamente los gestores de espacio (o los gestores de la organización padre) pueden añadir miembros a un espacio. Para añadir miembros de un espacio a una organización de la instancia de {{site.data.keyword.cfee_full_notm}}:

1. Vaya a la entrada **Organizaciones** en el panel de navegación, localice la organización en la que se ubica el espacio de destino y púlsela para abrir la página de la organización.
2. En la página de la organización, vaya al separador **Espacios**.
3. Localice el espacio de destino en la tabla de espacios, vaya al menú _Acciones_ en la fila de tabla y seleccione **Añadir miembro**. De forma alternativa, puede pulsar en el espacio de destino para abrir la página del espacio y seleccionar **Añadir miembro**.
4. En la ventana _Añadir miembro_, busque el usuario, seleccione **Rol de espacio** y pulse **Añadir**.

**Nota**: Los gestores de la organización pueden añadir miembros directamente a un espacio sin añadirlos primero a la organización padre. Cuando un gestor de organización añade miembros a un espacio, dichos miembros también se convierten en miembros de la organización padre.
