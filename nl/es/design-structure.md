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

# Diseño de la estructura del entorno de {{site.data.keyword.Bluemix_notm}}
{: #bpimplementation}

En lugar de la metodología tradicional y estrictamente definida de desarrollo, prueba y producción, puede implementar un entorno donde los desarrolladores y los probadores puedan colaborar junto a otros miembros del equipo. Si diseña la forma en la que desea desarrollar y entregar sus apps, cree espacios de {{site.data.keyword.Bluemix}} para satisfacer dicha metodología. En lugar de diseñar el entorno desde el nivel inferior de la organización, considere la posibilidad de diseñar el entorno de {{site.data.keyword.Bluemix_notm}} desde el nivel superior del espacio.

Tenga en cuenta la escala y el ámbito de las apps que tiene intención de desarrollar y de desplegar. Se puede utilizar un espacio de {{site.data.keyword.Bluemix_notm}} como un entorno de desarrollo para una o varias apps que están estrechamente conectadas o definidas. Además de un espacio de desarrollo, por ejemplo, puede crear espacios para las pruebas de unidad, las pruebas de rendimiento y las pruebas de integración. Los espacios también pueden estar definidos para la compilación, la transferencia y la producción. Cada uno de los espacios que cree se pueden compartir con distintos miembros del equipo dentro de la misma organización.

Cree organizaciones de Cloud Foundry independientes cuando haya personas trabajando en distintas áreas empresariales y donde sus actividades no se solapen. Si hay dos grupos independientes, la creación de una organización para cada uno de ellos define los límites claros para la entrega y la gestión de los profesionales y los recursos del equipo. Puede definir una API para la comunicación entre las organizaciones.

Las organizaciones de Cloud Foundry pueden crearse para que coincidan con el modo en que desea trabajar en lugar de con la estructura de una empresa. Normalmente, las organizaciones de la empresa pueden cambiar, pero el desarrollo y el mantenimiento de una aplicación continúa independientemente. Diseñe el entorno de {{site.data.keyword.Bluemix_notm}} durante el tiempo de vida de las apps y no en la estructura de organización de la empresa.

El desarrollo y el despliegue iterativos pueden dar lugar a que las apps se expandan rápidamente. El diseño del proceso de entrega debe ser capaz de aumentar de forma rápida y sencilla. Desea un desarrollo continuo con una tasa de despliegue rápida. Tener los espacios de desarrollo y de producción en la misma organización de {{site.data.keyword.Bluemix_notm}} proporciona acceso a los mismos recursos. La gestión de distintos espacios dentro de una sola organización reduce la carga de trabajo administrativa. El personal de desarrollo, de prueba y de operaciones puede colaborar fácilmente si está trabajando dentro de la misma organización de {{site.data.keyword.Bluemix_notm}}.

Implemente un estándar de denominación para identificar claramente el uso de la organización y del espacio. Por ejemplo, puede incluir el tipo de nube, la región geográfica, el tipo de uso (por ejemplo, dev, test, prod), el nombre de aplicación, y el número de versión o de revisión. Las organizaciones y los espacios se podrán identificar fácilmente para fines de administración y de acceso.  

El número de espacios se puede multiplicar rápidamente debido al desarrollo iterativo. Puede definir tantos espacios como necesite dentro de una organización. Si tiene previsto definir muchos espacios, es posible que desee crear una aplicación para ayudar a gestionar los espacios. Cuando el número de espacios supere los sesenta, es posible que desee definir otra organización.

Haga que una persona cree y gestione una organización, defina los espacios y otorgue acceso a los miembros del equipo. Se puede otorgar el mismo acceso a una segunda persona para mantener el entorno cuando el gestor de la organización esté inhabilitado.  

Identifique todas las personas que necesitan acceso a cada espacio y organización. Determine su rol. El rol de trabajo de un miembro del equipo determina su autoridad. Por ejemplo, un desarrollador sénior necesita la autorización para ver y actualizar todo el entorno de desarrollo de {{site.data.keyword.Bluemix_notm}}. Sin embargo, un desarrollador junior está limitado en lo que pueda ver y actualizar.
