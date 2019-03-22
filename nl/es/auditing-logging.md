---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-11-09"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Auditoría y registro
{: #auditing-logging}

Las funciones de auditoría y registro de {{site.data.keyword.cfee_full}} (CFEE) permiten a los administradores auditar los sucesos que tienen lugar en una instancia de CFEE y los desarrolladores realizar un seguimiento de los sucesos de registro generados a partir de sus aplicaciones Cloud Foundry.

La auditoría y el registro en CFEE reciben soporte mediante la integración con los servicios Log Analysis y Activity Tracker de IBM Cloud.

## Auditoría
{: #auditing}

La auditoría permite a los administradores de CFEE realizar un seguimiento de las actividades auditables de Cloud Foundry que tienen lugar en una instancia de CFEE.  Estas actividades incluyen inicio de sesión, creación de organizaciones y espacios, pertenencia de usuarios y asignaciones de roles, despliegues de aplicaciones, enlaces de servicio y configuración de dominios. Se da soporte a la auditoría mediante la integración con el servicio Activity Tracker en IBM Cloud. Una instancia del servicio Activity Tracker seleccionada por el administrador de CFEE se configura automáticamente para recibir sucesos que representan acciones realizadas en Cloud Foundry y en el panel de control de CFEE.  El usuario puede ver y gestionar estos sucesos en la interfaz de usuario de la instancia de servicio de Activity Tracker.

Para habilitar la auditoría para una instancia de CFEE:

1. Abra una interfaz de usuario de CFEE y vaya a la entrada **Operaciones > Auditoría** en el panel de navegación de la izquierda para abrir la página Registro.
2. Pulse **Habilitar auditoría** y seleccione una de las **instancias de Activity Tracker** disponibles en la cuenta de IBM Cloud.  Si no hay ninguna instancia disponible, el usuario verá una opción para crear una nueva instancia de Activity Tracker en el catálogo de IBM Cloud.
3.  Una vez que se ha habilitado la auditoría, los detalles de la configuración se visualizan en la página. Los detalles incluyen el estado de la configuración y un enlace con la propia instancia de servicio de Activity Tracker, donde el usuario puede acudir para ver y gestionar sucesos de auditoría.

Para inhabilitar la auditoría, pulse **Inhabilitar auditoría**, lo que eliminará la instancia de servicio de Activity Tracker que se ha añadido y configurado previamente. Esta acción no suprime la instancia del servicio Activity Tracker.

## Persistencia de registro
{: #logging}

El registro de los sucesos de Cloud Foundry recibe soporte a través de la integración con el servicio Log Analysis en IBM Cloud. Una instancia del servicio Log Analysis seleccionada por el administrador de CFEE se configura automáticamente para recibir y conservar de forma permanente los sucesos de registro de Cloud Foundry generados a partir de la instancia de CFEE.  El usuario puede ver y gestionar estos sucesos de registro en la interfaz de usuario de la instancia de servicio de Log Analysis.

Para habilitar el registro para una instancia de CFEE:

1. Asegúrese de que tiene una [política de acceso de IAM](https://console.bluemix.net/iam/#/users) que le asigna el rol de editor, operador o administrador sobre la instancia de servicio de Log Analysis en la que tiene previsto guardar de forma permanente los sucesos de registro.
2. Abra una interfaz de usuario de CFEE y vaya a la entrada **Operaciones > Registro** en el panel de navegación de la izquierda para abrir la página Registro.
3. Pulse **Habilitar persistencia** y seleccione una de las **instancias de Log Analysis** disponibles en la cuenta de IBM Cloud.  Si no hay ninguna instancia disponible, el usuario verá una opción para crear una instancia en el catálogo de IBM Cloud.
4. Una vez que se ha habilitado la persistencia de registro, los detalles de la configuración se visualizan en la página. Los detalles incluyen el estado de la configuración y un enlace con la propia instancia de servicio de Log Analysis, donde el usuario puede acudir para ver y gestionar sucesos de registro.

**Aviso:** para habilitar la persistencia de registro se requiere un reinicio disruptivo del panel de control y de las células de CFEE.  Durante el reinicio, todas las funciones de administración estarán disponibles, pero puede que algunas aplicaciones y servicios que se ejecutan en esta instancia de CFEE no lo estén.  El estado de los componentes de CFEE se reflejará en la página Comprobación de estado durante el reinicio.  El reinicio tarda 20 minutos aproximadamente.

Para inhabilitar la persistencia de registro, pulse **Inhabilitar persistencia de registro**, lo que eliminará la instancia de servicio que se ha añadido y configurado previamente. Esta acción no suprimirá la instancia del servicio Log Analysis.

**Nota:** cuando se inhabilita la persistencia de registro, se siguen generando sucesos de registro de Cloud Foundry, pero no se guardan de forma permanente fuera de la instancia de CFEE.
