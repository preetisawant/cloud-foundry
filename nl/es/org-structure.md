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

# Determinación de la arquitectura de la organización
{: #orgstructure}

Para diseñar un entorno que utilice {{site.data.keyword.Bluemix_notm}} Público, {{site.data.keyword.Bluemix_dedicated_notm}}, {{site.data.keyword.Bluemix_local_notm}} o cualquier combinación, puede utilizar las siguientes arquitecturas de organización:

* Organización única: Considere la posibilidad de utilizar esta arquitectura si necesita el mismo conjunto de usuarios para acceder a los recursos disponibles en cualquier lugar de la organización.
* Organización múltiple: Considere la posibilidad de utilizar esta arquitectura si necesita aislamiento entre distintos entornos.

## Una única organización en comparación con varias organizaciones
{: #singleormulti}

En un entorno de organización única, los recursos de infraestructura los comparten distintas áreas de
la empresa. Sin embargo, en un entorno de organización múltiple, los recursos de infraestructura no se comparten.

Las dos arquitecturas de organización dan soporte a los siguientes principios:

* Imposición de límites para apps, proyectos, o ambos.
* Autorización para gestionar recursos otorgados por el rol de usuario.

A continuación, puede definir varios espacios que se basan en distintas líneas de negocio (LOB),
las fases de entrega, proyectos específicos, apps, permisos de usuarios, o una combinación de estos componentes.

Para implementar una arquitectura de varias organizaciones, puede definir las organizaciones que se corresponden con distintas LOB, fases de entrega, proyectos específicos, permisos de usuarios, o una combinación de estos componentes. A continuación, puede definir diversos espacios que se basan en apps o proyectos entregados por el mismo departamento de la empresa.

{: tip}

## Consideraciones sobre la organización
{: #orgconsiderations}

Al implementar una arquitectura de organización única, la organización incluirá todos los recursos de nube, los servicios y las apps que puede utilizar para desarrollar, gestionar y desplegar apps de nube. En {{site.data.keyword.Bluemix_notm}} Público, la organización proporciona segregación entre cuentas y está disponible en todas las regiones.

 ![Figura que muestra la arquitectura de organización única](img/singleorg_example.svg "Figura que muestra la arquitectura de organización única en {{site.data.keyword.Bluemix_notm}}")

 Figura 1. Ejemplo de una arquitectura de organización única.
{: #bpfigure1}

Al implementar una arquitectura de organización múltiple, las organizaciones proporcionarán el primer nivel de imposición de límites y de abstracción, que puede utilizar para controlar y definir qué se puede hacer y quién lo puede hacer. Diseñe cada organización en torno a las distintas LOB, las fases de entrega, los roles de los usuarios, los proyectos específicos, o una combinación de estos componentes.  

El número de organizaciones que necesita depende de varios factores:

* El nivel de granularidad que necesita dentro de su organización para gestionar cuotas y costes de control.
* El nivel de seguridad que debe imponer en los distintos entornos. Por ejemplo, si está utilizando contenedores, es posible que desee segregar imágenes de contenedor que se utilizan para el desarrollo a partir de imágenes del contenedor que se utilizan para la producción.
* La ubicación de las organizaciones debido a requisitos corporativos, del país y del sector. Por ejemplo, puede que desee ejecutar todas las apps en un entorno ubicado en una región específica de su geografía (geo).

Cuando está definiendo las distintas organizaciones para la estructura de nube, tenga en cuenta la orientación siguiente:

* Defina y, a continuación, aplique un convenio de denominación. Por ejemplo, defina un convenio de denominación donde el nombre de la organización incluya información sobre el área de negocio, el tipo de nube y la fase del proceso (desarrollo, pruebas o producción). Para las organizaciones que se encuentran en {{site.data.keyword.Bluemix_notm}} Público, es posible que desee añadir también información sobre la región.
* Defina las restricciones que se aplican a la organización. Por ejemplo, defina el rol de los miembros del equipo que van a trabajar en dicha organización.
* Identifique al gestor de la organización.
* Identifique el área de la empresa que se asigna a esta organización.

Los casos de ejemplo siguientes muestran distintos enfoques que puede adoptar al definir el número de organizaciones de Cloud Foundry en un entorno:

### Caso de ejemplo 1: Segregación de los grupos de usuarios por entrega de aplicación empresarial

 Descripción: Las reglas empresariales requieren que las apps de cada LOB deban estar desarrolladas, gestionadas y desplegadas por los usuarios de cada LOB. Se debe imponer seguridad para que los usuarios sólo puedan acceder a las apps que sean relevantes para su parte del negocio. Por lo tanto, los usuarios trabajan en distintas áreas de negocio, las apps en las que están trabajando necesitan acceso a distintos recursos de {{site.data.keyword.Bluemix_notm}}, y no hay solapamiento de actividades.

  Solución: Puede crear una organización para cada proceso de entrega de aplicación empresarial. Por ejemplo, una organización para banca comercial, y otra para banca de inversión.

  ![Figura que muestra la segregación de usuarios por entrega de aplicación empresarial](img/bank_example.svg "Figura que muestra la segregación de usuarios por entrega de aplicación empresarial")

  Figura 2. Ejemplo de una arquitectura de varias organizaciones alineada con la entrega de LOB
{: #bpfigure2}

### Caso de ejemplo 2: Segregación basada en el tipo de usuarios (usuarios internos, usuarios externos)

  Descripción: Su empresa trabaja con distintos socios y necesita límites claros entre los usuarios internos y externos.

  Solución: Puede crear una organización para entregar apps que se utilizan internamente. Además, puede crear una organización para cada socio externo.

### Caso de ejemplo 3: Aislamiento por proyecto

  Descripción: Su empresa ejecuta hackathons para identificar servicios nuevos.  

  Solución: Puede definir una organización por hackathon y utilizar la organización como un recinto de pruebas. Después del hackathon, puede promover la organización del recinto de pruebas en una organización adicional de su cuenta.

### Caso de ejemplo 4: Aislamiento de usuarios por fase de entrega

  Descripción: Una empresa desea usuarios de desarrollo, de prueba y de producción para que colaboren en una entrega, pero su acceso está controlado por el rol del usuario y la experiencia laboral.

  Solución: Puede crear una única organización y definir un espacio para cada fase de entrega. A continuación, en función del rol de usuario y de la experiencia laboral, otorgue el acceso de lectura y de escritura que necesiten para finalizar su trabajo y colaborar también dentro de la organización.

  ![Figura que muestra el aislamiento de usuarios por fase de entrega](img/user_groups_example.svg "Figura que muestra el aislamiento de usuarios por fase de entrega")

   Figura 3. Ejemplo de una arquitectura de organización única alineada por fase de entrega
{: #bpfigure3}

## Denominación, restricciones y gestión de la organización
{: #orgadmin}   

Tenga en cuenta la siguiente orientación de organización:

* Defina y aplique un convenio de denominación. Por ejemplo, defina un convenio de denominación donde el nombre de la organización incluya información sobre el área de negocio, el tipo de nube y el rol de TI (desarrollo, pruebas o producción). Para las organizaciones que se encuentran en {{site.data.keyword.Bluemix_notm}} Público, es posible que desee añadir también información sobre la región. Puede cambiar el nombre de una organización una vez que esté creada. Si el nombre de una organización se altera, notifique a todos los miembros del equipo de la organización sobre el cambio.
* Defina las restricciones que se aplican a la organización. Por ejemplo, defina el rol de cada uno de los miembros del equipo y los permisos que necesitan para trabajar en dicha organización.
* Identifique al gestor de la organización. Es posible que desee delegar la administración de la organización a más de una persona.
* Identifique el área de la empresa que se asigna a esta organización. El uso de la aplicación que se genera en cada uno de los espacios, dentro de la organización, se acumula y se notifica a nivel de organización.
