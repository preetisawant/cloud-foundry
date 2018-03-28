---


copyright:
  years: 2016, 2018
lastupdated: "2018-01-16"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Cómo funciona Cloud Foundry con {{site.data.keyword.cloud_notm}}
{: #howwork}

Cuando despliega una app en Cloud Foundry, debe configurar {{site.data.keyword.cloud_notm}} con suficiente información para dar soporte a la app.

* En el caso de una app para móvil, {{site.data.keyword.cloud_notm}} contiene un artefacto que representa el programa de fondo de las apps para móvil, como por ejemplo los servicios que utilice la app para móvil para comunicarse con un servidor.
* En el caso de una app web, debe asegurarse de que esta información sobre el tiempo de ejecución y la infraestructura se comunique a {{site.data.keyword.cloud_notm}}, para que {{site.data.keyword.cloud_notm}} pueda configurar el entorno de ejecución apropiado para ejecutar la app.

Cada entorno de ejecución, que incluye tanto móvil como web, se aísla del entorno de ejecución de otras apps. Los entornos de ejecución se aíslan aunque estas apps estén en la misma máquina física. La figura siguiente muestra el flujo básico de cómo Cloud Foundry gestiona el despliegue de apps en {{site.data.keyword.cloud_notm}}:

![Despliegue de una app](images/deploy.png)

Figura 1. Despliegue de una app

Cuando crea una app y la despliega en Cloud Foundry, el entorno de {{site.data.keyword.cloud_notm}} determina un servidor virtual adecuado al que se envía la app, o los artefactos que representa la app. En el caso de una app para móvil, se crea una proyección de proceso en {{site.data.keyword.cloud_notm}}. Cualquier código de la app para móvil de la nube en principio se ejecuta en el entorno de {{site.data.keyword.cloud_notm}}. En el caso de una app web, el código que se ejecuta en la nube es la propia app que el desarrollador despliega en {{site.data.keyword.cloud_notm}}. La determinación del servidor virtual se basa en varios factores, que incluyen los siguientes:

* La carga que ya soporta la máquina
* Los tiempos de ejecución o infraestructuras que soporta dicho servidor virtual.

Después de seleccionar un servidor virtual, un gestor de aplicaciones de cada servidor virtual instala la infraestructura y el tiempo de ejecución apropiados para la app. A continuación, la app se puede desplegar en dicha infraestructura. Cuando se completa el despliegue, se inician los artefactos de la app.

La siguiente figura
muestra la estructura de un servidor virtual, también conocido como agente de ejecución de gotas (DEA), en el que se han desplegado varias apps:

![Diseño de un servidor virtual](images/container-diego.png)

Figura 2. Diseño de un servidor virtual

En cada servidor virtual, un gestor de apps se comunica con el resto de la infraestructura de {{site.data.keyword.cloud_notm}} y gestiona las apps que se despliegan en este servidor virtual. Cada servidor virtual dispone de contenedores para separar y proteger las apps. En cada contenedor, {{site.data.keyword.cloud_notm}} instala la infraestructura y el tiempo de ejecución adecuados que necesita cada app.

Cuando se despliega la app, si tiene una interfaz web (como por ejemplo una app web Java) y otros servicios basados en REST (como por ejemplo servicios móviles expuestos públicamente para la app para móvil), los usuarios de la app pueden comunicarse con la misma mediante solicitudes HTTP normales.

![Invocación de una app de {{site.data.keyword.cloud_notm}}](images/execute.png)

Figura 3. Invocación de una app de {{site.data.keyword.cloud_notm}}

Cada app puede tener uno o varios URL asociados, pero todos deben apuntar al punto final de {{site.data.keyword.cloud_notm}}. Cuando entra una solicitud, {{site.data.keyword.cloud_notm}} la examina, determina la app a la que va destinada y a continuación selecciona una instancia de la app para que reciba la solicitud.


## Arquitectura Cloud Foundry en {{site.data.keyword.cloud_notm}}
{: #architecture}

En general, no debe preocuparse de las capas de sistema operativo y de infraestructura cuando ejecute apps en {{site.data.keyword.cloud_notm}} en Cloud Foundry. Las capas de tipo sistemas de archivos raíz y componentes de middleware se abstraen para que se pueda centrar en el código de la app. Sin embargo, puede obtener más información sobre estas capas y necesita datos específicos sobre dónde se ejecuta la app.

Consulte [Visualización de las capas de infraestructura de {{site.data.keyword.cloud_notm}}](cf.html#infralayers) para obtener detalles.

Como desarrollador, puede interactuar con la infraestructura de {{site.data.keyword.cloud_notm}} mediante una interfaz de usuario basada en navegador. También puede utilizar una interfaz de línea de mandatos de Cloud Foundry, denominada cf, para desplegar apps web.

Los clientes, que pueden ser apps móviles, las apps que se ejecutan externamente, las apps creadas en {{site.data.keyword.cloud_notm}} o los desarrolladores que utilizan navegadores interactúan con las apps alojadas en {{site.data.keyword.cloud_notm}}. Los clientes utilizan las API REST o HTTP para dirigir las solicitudes a través de {{site.data.keyword.cloud_notm}} a una de las instancias de la app o a los servicios compuestos.

La figura siguiente muestra la arquitectura de Cloud Foundry de alto nivel en {{site.data.keyword.cloud_notm}}.

![Arquitectura de {{site.data.keyword.cloud_notm}}](images/arch.png)

Figura 4. Arquitectura de Cloud Foundry en {{site.data.keyword.cloud_notm}}

Puede desplegar sus apps en distintas regiones de {{site.data.keyword.cloud_notm}}, por motivos de latencia o de seguridad. Puede elegir desplegar en una región o a lo largo de varias regiones.


![Desarrollo de apps en varias regiones](images/multi-region.png)

Figura 5. Despliegue de apps en varias regiones

Capas de la infraestructura de {{site.data.keyword.Bluemix_notm}}
{: #infralayers}


{{site.data.keyword.Bluemix_notm}} abstrae y oculta las capas de sistema operativo y de infraestructura para que el usuario no tenga que gestionarlas. Sin embargo, es posible que en alguna ocasión desee obtener más información sobre el sistema operativo y el middleware de la app.
{:shortdesc}

### Visualización de las capas de la infraestructura de {{site.data.keyword.Bluemix_notm}}
{: #viewinfra}

Puede ejecutar el mandato **bluemix app stacks** para mostrar las pilas disponibles o los sistemas de archivo raíz en los que están desplegadas las apps. También puede especificar la pila cuando utilice el mandato **bluemix app push** con la opción *-s* y el *nombre_pila*, donde el nombre_pila es el sistema de archivos raíz, como `lucid64` o `cflinuxfs2`:

```
bluemix app push appName -s stack_name
```

Puede utilizar el mandato `cf buildpacks` para mostrar los componentes de middleware, como Perfil de WebSphere Liberty y SDK para Node.js, disponibles como tiempos de ejecución en los que se puede ejecutar la app. También puede especificar el entorno de tiempo de ejecución de la app con el siguiente mandato:

```
bluemix app push appName -b buildpackname
```
