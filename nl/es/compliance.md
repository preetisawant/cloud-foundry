---

copyright:
  years: 2018
lastupdated: "2018-10-19"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}


# Cumplimiento y regulación
{: #compliance}

{{site.data.keyword.cfee_full}} (CFEE) es una plataforma como un servicio. Como tal, el cliente es libre de utilizar la instancia de servicio para cualquier cosa a la que de soporte. El CFEE y los servicios dependientes tienen acceso a la menor cantidad de datos personales posible.

Sin embargo, debe quedar claro que, aunque el panel de control de CFEE (mediante IU/API/CLI) no procesa datos confidenciales (por ejemplo, datos HIPAA), es responsabilidad del cliente asegurarse de que utilizan su CFEE de forma responsable, ya que todas las dependencias son gestionadas por los clientes y son propiedad de los mismos en su cuenta de {{site.data.keyword.Bluemix_notm}}. 

Recomendamos seguir las siguientes prácticas recomendadas:
*  No modifique los servicios dependientes creados con un CFEE (Kubernetes, Cloud Object Storage y Compose for PostgreSQL).
*  Actualice y gestione el CFEE a través del propio servicio CFEE (interfaz de usuario o interfaz de línea de mandatos), en lugar de hacerlo a través del servicio Kubernetes.

El clúster Kubernetes se utiliza para mantener la mayor parte de la infraestructura CFEE, así como todas las aplicaciones que se ejecutan en el CFEE, ya que las células de Cloud Foundry se despliegan en la parte superior de los nodos Kubernetes. Este clúster es propiedad y está gestionado por la cuenta de SoftLayer del cliente.

CFEE utiliza la base de datos Compose for PostgreSQL para albergar metadatos sobre organizaciones, espacios, usuarios y roles. Si se utiliza la instancia de CFEE tal como se recomienda, no se expondrá ningún dato confidencial. Sin embargo, si un cliente decide dar un nombre a sus organizaciones y espacios con información personal o confidencial sobre sus clientes, la base de datos PostgreSQL podría contener información HIPAA u otro tipo de información confidencial.

CFEE utiliza la instancia de Cloud Object Storage para albergar droplets de una aplicación, de modo que se puedan desplegar, detener, iniciar, etc. Esto significa que la instancia de Cloud Object Storage no está ejecutando la aplicación, solo alojando su imagen. Por lo tanto, si la instancia de Cloud Object Storage se utiliza siguiendo las prácticas recomendadas, no contendrá ninguna información confidencial de HIPAA. El cliente es el responsable de garantizar que no haya datos personales codificados en ninguna de sus aplicaciones (datos de prueba, etc.).
