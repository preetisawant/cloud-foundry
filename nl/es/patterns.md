---

copyright:

  years: 2015, 2018
lastupdated: "2018-04-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Visión general estructural
{: #patterns}

Para un proyecto satisfactorio, tómese tiempo para planificar y diseñar qué recursos necesita y cuáles son sus requisitos empresariales. Para ayudarle a empezar, tenga en cuenta las preguntas siguientes:
{:shortdesc}

* ¿Cuántas apps está desarrollando, y de qué tipo?
* ¿A qué servicios deben acceder las apps?
* ¿Quién colabora en el proceso de desarrollo y qué rol desempeña?
* ¿Qué grado de aislamiento es necesario para cada fase del proyecto?
* ¿Proporciona su empresa los recursos de la infraestructura?
* ¿Cómo se comunica su empresa?
* ¿Existe un estándar de denominación que pueda implementar para identificar claramente la organización y el uso de espacio?

Como parte de la decisión de qué tipo de entorno de nube necesita, planifique la estructura de su cuenta, de las organizaciones, de los espacios, de los recursos y de los miembros del equipo.

Para la mayoría de las empresas, es suficiente con una sola cuenta de {{site.data.keyword.Bluemix_notm}}. Para empresas más grandes, donde hay más de un área empresarial, es posible que desee
una cuenta independiente de {{site.data.keyword.Bluemix_notm}} para cada dominio empresarial. Por ejemplo, dentro de una entidad bancaria de gran tamaño, puede que haya cuentas independientes para los sectores de venta al pormenor y comerciales.

En la tabla siguiente se proporciona un resumen de algunos de los elementos clave.

| Elemento   | Descripción |
|-----------|---------------|
|| Contiene una o más organizaciones. Debe tener una cuenta Pago según uso para crear más de una organización. |
|| Solo puede tener una cuenta. |
|| Puede añadir uno o varios gestores de la organización para delegar la gestión de la organización, lo que incluye los permisos de lectura y escritura en las organizaciones. |
|| Puede ser un miembro del equipo en organizaciones y espacios de otras cuentas de {{site.data.keyword.Bluemix_notm}}. |
| Organización   | Contiene uno o varios espacios. |
|| Contiene uno o varios gestores de la organización. |
|| Contiene uno o varios miembros del equipo. A cada miembro del equipo se le puede otorgar uno o varios roles. |
|| Los cargos de uso, generados por una aplicación desplegada dentro de un espacio, se notifican al nivel de organización. |
| Espacio   | Contiene uno o varios recursos. |
|| Contiene una o varias apps. |
|| Contiene uno o varios gestores de espacios. |
|| Contiene uno o varios miembros del equipo. Cada usuario ya debe ser un miembro del equipo en la organización de su propiedad. A cada miembro del equipo se le puede otorgar uno o varios roles. |
| Miembro de equipo   | Puede añadirse a una o varias organizaciones y espacios en distintas cuentas. |
|| Se le puede dar más de un rol en la misma organización, espacio, o ambos. |
{:caption="Tabla 1. Descripción de elementos clave" caption-side="top"}

