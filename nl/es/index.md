---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-07-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Acerca de {{site.data.keyword.cfee_full_notm}}
{: #about}

Con {{site.data.keyword.cfee_full}} (CFEE), puede crear una instancia de varias plataformas de Cloud Foundry aisladas y de nivel empresarial a petición. Instancias de la ejecución de servicio de {{site.data.keyword.Bluemix_notm}} Foundry Enterprise en su cuenta de {{site.data.keyword.Bluemix_notm}}. El entorno se despliega en un hardware aislado (clústeres de Kubernetes). Tiene el control completo del entorno, incluido el control de acceso, la gestión de la capacidad, la gestión de cambios, la supervisión y los servicios.
{:shortdesc}

{{site.data.keyword.cfee_full}} se encuentra actualmente en la fase beta y nos gustaría recibir comentarios al respecto. Para empezar, cree su propia instancia de {{site.data.keyword.cfee_full}} en [https://console.bluemix.net/cfadmin/create](https://console.bluemix.net/cfadmin/create) y [solicite acceso](http://ibm.biz/cfee-forum-signup) al [foro de Slack de IBM CFEE](https://ibm-cfee.slack.com) para escribir comentarios, hacer preguntas y conectar con el equipo del producto.
{:tip}

Para un proyecto satisfactorio, tómese tiempo para planificar y diseñar qué recursos necesita y cuáles son sus requisitos empresariales. Para ayudarle a empezar, tenga en cuenta las preguntas siguientes:

* ¿Cuántas apps está desarrollando, y de qué tipo?
* ¿A qué servicios deben acceder las apps?
* ¿Quién colabora en el proceso de desarrollo y qué rol desempeña?
* ¿Qué grado de aislamiento es necesario para cada fase del proyecto?
* ¿Proporciona su empresa los recursos de la infraestructura?
* ¿Cómo se comunica su empresa?
* ¿Existe un estándar de denominación que pueda implementar para identificar claramente la organización y el uso de espacio?

Como parte de la decisión de qué tipo de entorno de nube necesita, planifique la estructura de su cuenta, de las organizaciones, de los espacios, de los recursos y de los miembros del equipo.

Una única cuenta de {{site.data.keyword.Bluemix_notm}} es suficiente para la mayoría de las organizaciones. Si su organización tiene más de un área empresarial, puede crear una cuenta de {{site.data.keyword.Bluemix_notm}} independiente para cada dominio empresarial; por ejemplo, una gran entidad bancaria puede crear cuentas independientes para los sectores de venta al pormenor y comerciales.

En la tabla siguiente se proporciona un resumen de algunos de los elementos clave.

| Elemento   | Descripción |
|-----------|---------------|
| Cuenta de IBM Cloud | Las instancias de CFEE se crean en una cuenta de IBM Cloud específica, lo que hace que estén disponibles para los usuarios de la cuenta en función de los roles y las políticas de acceso definidas para dichos usuarios. |
|| La cuenta en la que se crean las instancias de CFEE debe ser del tipo Pago según uso o suscripción (no pueden ser cuentas de prueba).  |
| CFEE | El servicio de IBM Cloud Foundry Enterprise Environment para alojar aplicaciones. |
|| Está disponible en el catálogo de IBM Cloud. |
| Instancia de CFEE | Una instancia del servicio de IBM Cloud Foundry Enterprise Environment creada en una cuenta de IBM Cloud por un usuario con el rol de administrador o de editor en la cuenta. |
|| Puede haber varias instancias de CFEE en una cuenta de IBM Cloud. |
|| Puede contener una o más organizaciones. |
| Organización | Incluye uno o varios espacios. |
|| Incluye uno o varios gestores de la organización. |
|| Incluye uno o varios miembros del equipo. A cada miembro del equipo se le puede otorgar uno o varios roles. |
|| Los cargos de uso, generados por una aplicación desplegada dentro de un espacio, se notifican al nivel de organización. |
| Espacio | Incluye uno o varios recursos. |
|| Incluye una o varias apps. |
|| Incluye uno o varios gestores de espacios. |
|| Incluye uno o varios miembros del equipo. Cada usuario ya debe ser un miembro del equipo en la organización de su propiedad. A cada miembro del equipo se le puede otorgar uno o varios roles. |
| Miembro de equipo | Puede añadirse a una o varias organizaciones y espacios en distintas cuentas. |
|| Se le puede dar más de un rol en la misma organización, espacio, o ambos. |
| Alias de servicio | Un alias de la instancia de servicio en IBM Cloud. |
|| Permite a los desarrolladores enlazar instancias de servicio existentes disponibles en su cuenta de IBM Cloud a las aplicaciones desplegadas en un espacio de un CFEE.|
{:caption="Tabla 1. Descripción de elementos clave" caption-side="top"}

## Suministro de destinos para CFEE y servicios de soporte
{: #provisioning-targets}

A continuación se muestran las geografías, ubicaciones y centros de datos donde el servicio CFEE y los servicios dependientes (servicio de Kubernetes, Compose for PostgreSQL y servicios de Cloud Object Storage) están disponibles para el suministro:

|  **Geografía** &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;| **Instancia de CFEE y clúster de Kubernetes** | **Cloud Object Storage** | **Compose for PostgreSQL (CF Region)** |
|----------------------------------------|-------------------|-------------------|-------------------|
|América del Norte | Montreal (mon01) | us-geo | us-east |
|América del Norte | Toronto (tor01) | us-geo| us-east |
|América del Norte | Washington DC (wdc04) | us-geo | us-east |
|América del Norte | Washington DC (wdc06) | us-geo | us-east | 
|América del Norte | Washington DC (wdc07) | us-geo | us-east |
|América del Norte | Dallas (das10) | us-geo | us-south |
|América del Norte | Dallas (das12) | us-geo | us-south |
|América del Norte | Dallas (das13) | us-geo |us-south |
|América del Norte | San José (sjc03) | us-geo | us-south |
|América del Norte | San José (sjc04) | us-geo | us-south |
|América del Sur &nbsp; &nbsp;| Sao Paolo (sao01) |  us-geo | us-south |
|Europa | Londres (lon02) | eu-geo | eu-gb |
|Europa | Londres (lon04) | eu-geo | eu-gb |
|Europa | Londres (lon06) | eu-geo | eu-gb | 
|Europa | Amsterdam (ams03) | eu-geo | eu-de |
|Europa | Oslo (osl01) |eu-geo | eu-de | 
|Europa | París (par01) | eu-geo | eu-de |
|Europa | Frankfurt (fra02) | eu-geo | eu-de |
|Europa | Frankfurt (fra04) | eu-geo | eu-de | 
|Europa | Frankfurt (fra05) |  eu-geo | eu-de |
|Asia Pacífico | Melbourne (mel01) | ap-geo | au-syd |
|Asia Pacífico | Sídney (syd01) | ap-geo | au-syd |
|Asia Pacífico | Sídney (syd04) | ap-geo | au-syd | 
|Asia Pacífico | Hong Kong (hkg02) | ap-geo | au-syd |
|Asia Pacífico | Hong Kong (seo01) | ap-geo | au-syd |
|Asia Pacífico | Singapur (sng01) | ap-geo | au-syd |
|Asia Pacífico | Tokio (gok02) | ap-geo | au-syd |
|Asia Pacífico | Tokio (gok04) | ap-geo | au-syd |
|Asia Pacífico | Tokio (gok05) | ap-geo | au-syd |

{: caption="Tabla 2. Destinos de suministro para los servicios de soporte y CFEE" caption-side="top"}



Por **ejemplo**, el servicio CFEE puede suministrarse en tres centros de datos en Europa: Amsterdam (1 centro de datos), Frankfurt (3 centros de datos), Londres (3 centros de datos), Oslo (1 centro de datos) y París (1 centro de datos). Si se suministra CFEE en Frankfurt, la instancia de servicio de Cloud Object Store se desplegará en la región _ eu-geo _ y la instancia de servicio de Compose for PostgreSQL se desplegará en la región de Cloud Foundry pública de _eu-de_.

