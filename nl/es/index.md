---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-12-07"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Acerca de {{site.data.keyword.cfee_full_notm}}
{: #about}

Bienvenido al servicio {{site.data.keyword.cfee_full}}.

Con {{site.data.keyword.cfee_full}} (CFEE), puede crear instancias de varias plataformas de Cloud Foundry aisladas y de nivel empresarial a petición. Instancias de la ejecución de servicio de {{site.data.keyword.Bluemix_notm}} Foundry Enterprise en su cuenta de {{site.data.keyword.Bluemix_notm}}. El entorno se despliega en hardware aislado (clústeres de Kubernetes). Tiene un control completo sobre el entorno, que incluye el control de accesos, la capacidad, las actualizaciones de versiones, el uso de recursos y la supervisión. Además, la integración de CFEE en {{site.data.keyword.Bluemix_notm}} permite a los desarrolladores aprovechar los servicios disponibles en su cuenta de {{site.data.keyword.Bluemix_notm}}.  Los usuarios pueden añadir estos servicios a un CFEE y enlazarlos a las aplicaciones desplegadas en espacios de CFEE.

Descubra cómo puede [**comenzar**](https://cloud.ibm.com/docs/cloud-foundry/getting-started.html#getting-started) a crear y a utilizar una instancia de CFEE.

{:shortdesc}

## Principales elementos de CFEE
{: #key-elements}

En la tabla siguiente se muestra un resumen de los principales elementos del servicio {{site.data.keyword.cfee_full}}:

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
|América del Norte | Dallas (dal10) | us-geo | us-south |
|América del Norte | Dallas (dal12) | us-geo | us-south |
|América del Norte | Dallas (dal13) | us-geo |us-south |
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
|Europa | Milán (mil01) |  eu-geo | eu-de |
|Asia Pacífico | Melbourne (mel01) | ap-geo | au-syd |
|Asia Pacífico | Sídney (syd01) | ap-geo | au-syd |
|Asia Pacífico | Sídney (syd04) | ap-geo | au-syd | 
|Asia Pacífico | Hong Kong (hkg02) | ap-geo | au-syd |
|Asia Pacífico | Hong Kong (seo01) | ap-geo | au-syd |
|Asia Pacífico | Singapur (sng01) | ap-geo | au-syd |
|Asia Pacífico | Tokio (tok02) | ap-geo | au-syd |
|Asia Pacífico | Tokio (tok04) | ap-geo | au-syd |
|Asia Pacífico | Tokio (tok05) | ap-geo | au-syd |
|Asia Pacífico | Chennai (che01) | ap-geo | au-syd |
{: caption="Tabla 2. Destinos de suministro para los servicios de soporte y CFEE" caption-side="top"}

Por **ejemplo**, el servicio CFEE puede suministrarse en tres centros de datos en Europa: Amsterdam (1 centro de datos), Frankfurt (3 centros de datos), Londres (3 centros de datos), Oslo (1 centro de datos) y París (1 centro de datos). Si se suministra CFEE en Frankfurt, la instancia de servicio de Cloud Object Store se desplegará en la región _eu-geo_ y la instancia de servicio de Compose for PostgreSQL se desplegará en la región de Cloud Foundry pública de _eu-de_.

Encontrará vídeos con información detallada y demostraciones sobre cómo trabajar con los servicios de CFEE en la [lista de reproducciones de vídeos de CFEE](https://ibm.biz/CFEE_Playlist){: new_window} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo").
{:tip}
