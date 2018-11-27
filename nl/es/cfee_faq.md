---



copyright:

  years: 2018

lastupdated: "2018-11-09"



---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:tip: .tip}

# Preguntas frecuentes
{: #cfeefaq}

## ¿Cuál es la diferencia entre IBM Cloud Foundry Enterprise Environment (CFEE) y Cloud Foundry público?
{: #cfee_diff}

Puede utilizar {{site.data.keyword.cloud}} Foundry público para ejecutar aplicaciones nativas de nube que utilizan Cloud Foundry para la configuración sencilla, el escalado potente y la gestión de tráfico. También tiene un acceso fácil a todos los servicios de {{site.data.keyword.cloud}}.

Puede utilizar {{site.data.keyword.cfee_full}} para todo lo que haría con Cloud Foundry público, y además para crear y gestionar entornos aislados para alojar aplicaciones de Cloud Foundry exclusivamente para su empresa.


## ¿En qué se diferencia la nueva oferta de las ofertas anteriores de IBM Cloud Foundry?
{: #cfOfferings_diff}

Con respecto al multiarrendatario público, la diferencia más destacada es, sin duda, las propiedades de aislamiento. Con respecto a la oferta existente de un solo arrendatario de la infraestructura de IBM Cloud, las dos principales diferencias son el menor tamaño de la infraestructura (y, por lo tanto, el menor coste), así como el modelo de integración de servicios en un entorno de un solo arrendatario.

## ¿Dónde puedo encontrar el servicio CFEE?
{: #where}

Puede encontrar y crear una instancia del servicio {{site.data.keyword.cfee_full}} en el [catálogo de {{site.data.keyword.Bluemix_notm}}](https://console.stage1.bluemix.net/catalog).

## ¿Puedo tener más de un entorno de CFEE dentro de un centro de datos regional?
{: #multiple-cfees}

Sí, puede crear instancias de CFEE a petición, tantas como desee, en [estas regiones](https://dev.console.test.cloud.ibm.com/docs/cloud-foundry/index.html#provisioning-targets){: new_window} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo").

## ¿Tengo que empezar con alguna capacidad mínima?
{: #minimum-capacity}

Sí. Para crear una instancia de CFEE se necesita como mínimo dos células de Cloud Foundry, cada una con 4 núcleos de 16 GB de RAM, un disco primario SSD de 25 GB, un disco secundario SSD de 100 GB y una velocidad de red de 1000 Mbps.

## ¿Cuál es la IaaS subyacente en el que despliega CFEE?
{: #why-kubs}

El servicio CFEE se ejecuta en contenedores de Kubernetes, lo que permite un menor coste de infraestructura y operaciones más eficientes, ya que Kubernetes es un IaaS muy inteligente que automatiza muchas actividades operativas. 

## ¿Cuáles son mis opciones de aislamiento al crear un CFEE?
{: #isolation}

Tiene dos opciones de hardware sobre el tipo de infraestructura de Kubernetes en la que se despliega la instancia de CFEE: hardware _virtual compartido_ o _virtual dedicado_. Con el hardware _virtual compartido_, los nodos trabajadores (en los que se despliega el contenedor de la plataforma Cloud Foundry) se distribuyen entre usted y otros clientes de IBM.  Con el hardware _virtual dedicado_, los nodos trabajadores están alojados en hardware que está dedicado de forma exclusiva a su cuenta.  Tenga en cuenta que en ambos casos (_virtual compartido_ y _virtual dedicado_, cada nodo trabajador es de un solo arrendatario para el cliente.  Esto significa que las células de Cloud Foundry en las que se ejecutan las aplicaciones no se comparten con otros clientes.

## ¿Puedo escalar la capacidad de un CFEE?
{: #scaling}

Sí, puede aumentar o disminuir la capacidad de su CFEE a medida que cambien sus necesidades mediante la adición o eliminación de células de Cloud Foundry.

## ¿Puedo actualizar mi CFEE a una nueva versión? ¿Cómo funciona?
{: #upgrading}
Sí. La interfaz de usuario de CFEE le notifica cuando hay nuevas versiones de CFEE.  Usted decide cuándo desea actualizar a una nueva versión. Los administradores de CFEE invocan la actualización de versión de CFEE en la interfaz de usuario. Las actualizaciones de versión de CFEE pueden contener nuevas versiones de sus componentes o de los servicios de soporte (es decir, Cloud Foundry, Kubernetes, etc).  Primero se actualiza el panel de control de CFEE y luego las células de Cloud Foundry.  El proceso de actualización se ha optimizado para minimizar el tiempo de interrupción.

## ¿Qué se necesita para crear una instancia de CFEE?
{: #create}

Encontrará el servicio CFEE en la lista del catálogo de {{site.data.keyword.Bluemix_notm}}.  Debe tener una cuenta de {{site.data.keyword.Bluemix_notm}} actualizada y permisos sobre el servicio CFEE y sus servicios soportados (Kubernetes, Cloud Object Storage y Compose for PostgreSQL).  Una vez que tenga estos permisos, simplemente especifique un nombre para el entorno y pulse _Crear_.  La creación tarda aproximadamente unos 90 minutos.

## ¿Puedo utilizar los servicios de {{site.data.keyword.Bluemix_notm}} en mi CFEE?
{: #Services-ibmcloud}

¡Por supuesto!  Al estar integrado en {{site.data.keyword.Bluemix_notm}}, los desarrolladores de un CFEE pueden crear instancias de servicio de {{site.data.keyword.Bluemix_notm}} (o utilizar instancias existentes) y enlazarlas a aplicaciones desplegadas en espacios de CFEE.

## ¿Puedo tener mis propios servicios en mi CFEE?
{: #Services-ibmcloud}

Sí.  Un administrador puede registrar un intermediario de servicios en el CFEE y poner planes de servicio personalizados a disponibilidad de los usuarios de dicho CFEE.  El marketplace de MCFEE local incluye servicios del catálogo de {{site.data.keyword.Bluemix_notm}} más cualquier servicio del cliente gestionado por el intermediario de servicios local del CFEE.

## ¿Cómo puedo controlar el acceso de los usuarios a un CFEE?
{: #Services}

Al igual que cualquier otro servicio de {{site.data.keyword.Bluemix_notm}}, el acceso a un CFEE se controla mediante _ Identity & Access Management_ (IAM). La asignación de políticas de acceso de usuario (ya sea individualmente o a través de grupos de acceso) con roles específicos les proporciona niveles específicos de acceso a un CFEE.  Además del acceso al servicio de CFEE, el acceso a las organizaciones y espacios de Cloud Foundry en CFEE se controla mediante la pertenencia de Cloud Foundry y los roles asignados a los usuarios en organizaciones y espacios específicos.

