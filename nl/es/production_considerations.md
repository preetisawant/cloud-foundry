---

copyright:
  years: 2016, 2017, 2018
lastupdated: "2018-01-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Mejores prácticas para ejecutar apps en producción
{: #production}

Cloud Foundry es una plataforma excelente para ejecutar aplicaciones listas para la nube en producción. Estas mejores prácticas pueden ayudar a ejecutar apps de Cloud Foundry de producción con {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## Varias instancias
{: #multiple_instances}

Las apps listas para Cloud son escalables horizontalmente, y por lo tanto se pueden añadir o eliminar dinámicamente instancias de aplicación. Ejecute al menos tres instancias de cada aplicación para evitar tiempo de inactividad inesperado en el caso de incidentes aislados o mantenimiento de la plataforma.

## Opciones de supervisión
{: #monitoring}

{{site.data.keyword.Bluemix_notm}} facilita la supervisión de la aplicación con servicios como [Monitoring and Analytics](/docs/services/monana/index.html) y [New Relic ![Icono de enlace externo](../icons/launch-glyph.svg)](http://newrelic.com/){: new_window}. Consulte [Capacidades de registro integradas](../monitor_log/logging.html#logging_for_bluemix_apps) para obtener más información.

## Opciones de soporte
{: #support}

El plan de precios de pago de {{site.data.keyword.Bluemix_notm}} ofrece un número de tipos de cuenta distintos con soporte de pago *opcional*.  Sin importar el tipo de cuenta, si piensa en llevar una aplicación a producción en {{site.data.keyword.Bluemix_notm}}, considere la posibilidad de inscribirse en esta opción.

Con o sin soporte de pago, puede obtener ayuda como se describe en [¿Cómo obtengo el apoyo que necesito?](../get-support/howtogetsupport.html), pero pagando por el apoyo garantizará que las incidencias de soporte recibirán el nivel de atención que se merecen.
