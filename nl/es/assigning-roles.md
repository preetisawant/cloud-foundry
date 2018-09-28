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

# Asignar roles
{: #roles}

Puede otorgar varios roles a miembros del equipo en una cuenta de {{site.data.keyword.Bluemix_notm}}. Estos roles definen los permisos del usuario para gestionar los recursos de la cuenta y de la organización:
Puede otorgar [roles de usuario](/docs/iam/users_roles.html#userroles) a miembros de una organización. Estos roles definen el nivel de acceso dentro de la organización, y restringen quién puede acceder a un espacio y a sus recursos. Por ejemplo, puede otorgar a los usuarios distintos permisos en distintos espacios.

## Propietario de la cuenta
{: #accountowner}

Tanto si diseña una arquitectura con varias organizaciones como una arquitectura con una única organización, el propietario de la cuenta será el superusuario del entorno de nube.

Entre las tareas principales del propietario de la cuenta se incluyen las siguientes:

* Gestión de los recursos de la cuenta global.
* Creación de organizaciones.
* Adición de los miembros del equipo a la cuenta.

El propietario de la cuenta también puede añadir uno o varios usuarios como gestores de una organización asignando a estos usuarios el rol **Gestor**. Considere la posibilidad de añadir dos usuarios como gestores de la organización. El primer usuario actúa como el gestor principal de la organización. El segundo usuario actúa como el gestor adjunto, en caso de que el gestor principal no esté disponible.

## Roles de usuario
{: #userroles}

Los roles de usuario definen los permisos que puede asignar a un miembro del equipo en una organización y definen el nivel de acceso que tiene un miembro del equipo dentro de la organización y de cada espacio.

En una arquitectura con varias organizaciones o con una única organización, defina los miembros del equipo y los permisos que necesita cada usuario para completar su trabajo:

1. Identifique el conjunto de usuarios que necesita acceso a una organización.
2. Defina los permisos para cada miembro del equipo en la organización y en un espacio de la organización.
3. Seleccione el rol que otorga a un usuario los permisos que necesita.

   * Gestor de organización
   * Auditor de organización
   * Gestor de facturación de organización
   * Gestor de espacio
   * Desarrollador de espacio
   * Auditor de espacio

### Gestor de organización
{: #bporgmgr}

Entre las tareas de las que un gestor de la organización es responsable se incluyen la creación de espacios, la distribución de la cuota entre los espacios, la invitación de los miembros del equipo y, opcionalmente, la otorgación a los mismos de roles específicos, y la definición de dominios personalizados.

### Auditor de organización
{: #bporgauditor}

Los miembros del equipo con el rol **Auditor** de la organización pueden supervisar la cuota, el uso de recursos y los miembros del equipo para todos los espacios de una organización.
Los auditores podrán entonces informar sobre la eficiencia de la organización y resaltar cualquier problema potencial.

* Al adoptar una arquitectura con varias organizaciones, es posible que desee otorgar el rol de auditor a los mismos miembros del equipo para todas las organizaciones que formen parte de la cuenta.
A continuación, estos miembros del equipo pueden supervisar la cuota en todas las organizaciones del entorno de nube y obtener una vista global de la cuenta.
* Al adoptar una arquitectura con una única organización, otorgue el rol de auditor a los miembros del equipo con la responsabilidad para supervisar el uso de la cuota y la eficiencia global
de la organización.

### Gestor de facturación de organización
{: #bporgbillingmgr}

Los miembros del equipo con el rol **Gestor de facturación** pueden supervisar los costes de una organización.

* Al adoptar una arquitectura con varias organizaciones, es posible que desee otorgar el rol de facturación al mismo conjunto de miembros del equipo para todas las organizaciones que forman parte de la cuenta. A continuación, estos miembros del equipo podrán supervisar el coste de cada organización y obtener una vista global de la cuenta.
* En una arquitectura con una única organización, identifique los usuarios que son responsables de la supervisión del coste.

### Gestor de espacio
{: #bpspacemgr}

El **Gestor** del espacio es responsable de cualquier trabajo que se realice dentro del espacio que gestiona y controla. El gestor de espacios puede realizar las tareas siguientes:

* Supervisar la cuota asignada al espacio.
* Solicitar más recursos al gestor de la organización.
* Notificar al gestor de la organización sobre los recursos que no son necesarios.
* Añadir miembros del equipo al espacio con el rol **Desarrollador**.
* Opcionalmente, asignar el rol **Gestor** de espacio a un miembro del equipo para que actúe como gestor de espacio adjunto en su ausencia.

### Desarrollador de espacio
{: #bpspacedev}

Un desarrollador de espacio puede realizar las tareas siguientes:

* Gestionar apps de Cloud Foundry.
* Suministrar y configurar servicios de {{site.data.keyword.Bluemix_notm}}.
* Asociar dominios a apps.

### Auditor de espacio
{: #bpspaceauditor}

Para todos los espacios, es posible que desee otorgar el rol **Auditor** de espacio a los mismos miembros del equipo con el rol **Auditor** de la organización. En la empresa, este rol se podría otorgar a un conjunto de usuarios específico.

