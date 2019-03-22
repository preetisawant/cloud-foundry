---

copyright:

  years: 2018
lastupdated: "2018-12-19"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Actualización y escalado
{: #update-scale}

Actualice la instancia de servicio de {{site.data.keyword.cfee_full_notm}} a la versión más recientes para obtener las últimas funciones y arreglos de CFEE. Las actualizaciones de CFEE pueden incluir nuevas versiones de Cloud Foundry y servicios de soporte de CFEE (Kubernetes, Cloud Object Storage o Compose for PostgreSQL).  Sin embargo, no todas las actualizaciones de CFEE incluirán una nueva versión de Cloud Foundry y de los servicios de soporte de CFEE.

Las actualizaciones de versión de CFEE se llevan a cabo en el panel de control que contiene los componentes de CFEE y en las células. También puede escalar la capacidad de su instancia de CFEE mediante la adición o supresión de células de aplicación.

**Nota:** durante una actualización de versión o mientras se añaden o se suprimen células, es posible que algunas métricas (por ejemplo, memoria y CPU) que se muestran en las páginas _Visión general_, _Uso de recursos_ y _Actualización y escalado_ no estén disponibles.

## Actualización de la versión de CFEE
{: #update}

Los usuarios necesitan los siguientes permisos para poder actualizar una instancia de CFEE a una nueva versión:
   * Rol de _editor_ o superior sobre una instancia de CFEE.
   * Rol de _operador_ o superior sobre el clúster de Kubernetes en el que se suministra el CFEE.

La actualización de la versión CFEE de la instancia de CFEE es un proceso de dos pasos. En primer lugar, actualice el panel de control que aloja los componentes de CFEE. A continuación, actualice las células que alojan las aplicaciones.

Se aplican las siguientes reglas y restricciones cuando se actualiza un CFEE a una nueva versión:
* El panel de control debe actualizarse primero. Una vez que actualizado el panel de control, se pueden actualizar las células.
* Las células de aplicación solo se pueden actualizar a la versión del panel de control.  Es decir, las células del panel de control pueden tener un nivel de versión de CFEE superior al de las células de aplicación, pero no viceversa.

Para actualizar la versión de CFEE de la instancia CFEE:
1. Vaya al panel de control de [{{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/dashboard/apps/) y abra el {{site.data.keyword.cfee_full_notm}} que desea actualizar.
2. En {{site.data.keyword.cfee_full_notm}}, vaya a la entrada **Células** del panel de navegación para abrir la página de células.
3. (opcional) En la tabla _Panel de control_, puede expandir la fila para ver los nodos trabajadores del panel de control.
4. Pulse **Actualizar**.
5. En el diálogo Actualizar del _Panel de control_, seleccione una de las versiones de CFEE disponibles y pulse **Actualizar**. La actualización tarda unos 45 minutos.  La descripción de la versión detalla las versiones de los componentes incluidos en el paquete de la versión de CFEE seleccionada, junto con un enlace al documento _Novedades_ en el que se describe el contenido suministrado en dicha versión.
6. La columna _Estado de nodos_ muestra el progreso de la actualización. Una vez que se haya completado la actualización, la columna _Versión_ refleja la nueva versión de CFEE.
7. Una vez que se haya completado la actualización de las células del panel de control, busque la tabla _Células_ y pulse **Actualizar**.
8. En el diálogo _Actualizar panel de control_, seleccione la versión CFEE y pulse *Actualizar*. Solo hay una versión disponible para actualizar las células porque las células solo se pueden actualizar a la versión del panel de control. Una sola acción de actualización actualiza todas las células.
9. Las células se actualizan secuencialmente. La columna _Estado de nodos_ muestra el progreso de la actualización de cada célula. A medida que se actualizan las células, su versión nueva se refleja en la columna _Versión_.

## Interrupciones durante la actualización de versión
{: #update-disruption}

La actualización del panel de control de Cloud Foundry no es un proceso disruptivo.  Sin embargo, la actualización de las células de Cloud Foundry a una nueva versión de CFEE puede interrumpir el funcionamiento del entorno CFEE.  La actualización de las células se realiza de una en una, de modo que las instancias de aplicación que se ejecutan en una célula se vuelvan a activar una vez que se ha completado la actualización, mientras que las otras células están fuera de servicio durante su actualización. Sin embargo, algunas aplicaciones y servicios que se ejecutan en el CFEE pueden no estar disponibles bajo ciertas circunstancias. Por ejemplo, si el CFEE tiene dos células de Cloud Foundry a capacidad completa, una aplicación con una sola instancia estará fuera de servicio durante la actualización de la versión porque la instancia de la aplicación no se puede mover a otra célula mientras se actualiza la célula y, por consiguiente, la aplicación no estará disponible.  Incluso con tres células y tres instancias por aplicación, puede haber una interrupción transitoria en la disponibilidad de las aplicaciones durante una actualización de versión.

Durante la actualización de la versión, puede haber una discrepancia en las métricas de memoria y de CPU mostradas en los indicadores de Nodos de célula de la página _Visión general_ de CFEE (que genera el clúster Kubernetes) y las mismas métricas que se muestran en el panel de control _Nodos_ en Grafana (que se generan a nivel de sistema operativo).

El estado de los componentes de CFEE mientras la actualización está en curso se reflejará en la página Comprobación de estado.  El reinicio tarda 45 minutos aproximadamente.

## Ciclo de versión y política de soporte
{: #version-cycle}

El servicio Cloud Foundry Enterprise Environment suele lanzar una nueva versión de forma regular. La versión del servicio sigue el formato semántico de versiones _**Principal.Menor.Parche**_ (https://semver.org/)

La versión _menor_ se incrementa de forma regular (generalmente, una vez al mes). La versión _principal_ también se incrementa, pero con menor frecuencia; generalmente cuando hay un cambio significativo.  La actualización a una versión _principal_ puede dar lugar a algunas interrupciones durante la actualización. Los _parches_ proporcionan un arreglo y se aplican a la última versión disponible. 

Para evitar que el sistema deje de estar inactivo, solo se permite actualizar las instancias de CFEE hasta un máximo de 2 versiones _principales_ por delante de su versión actual. Continuando con el ejemplo anterior, si la versión actual de la instancia de CFEE es la 3.1.2, y la versión de destino es la 7.0.0, la instancia de CFEE se deberá actualizar primero a la versión 5.x.x y luego a la versión de destino 7.0.0.

Las nuevas funciones y las mejoras de las funciones existentes que se proporcionan regularmente pasan a estar disponibles solo en la última versión. Los arreglos críticos se distribuyen en el último release dentro de las últimas 3 versiones _principales_ únicamente (la versión más reciente y las dos versiones anteriores). Por ejemplo, si están disponibles las versiones 4.x.x, 3.x.x y 2.x.x, las versiones 1.x.x no recibirán soporte (es decir, no se suministrarán parches con arreglos para las versiones 1.x.x).  

Los parches se suministran en la última versión disponible de una determinada versión _principal_. Por ejemplo, si una instancia de CFEE está ejecutando la versión 3.1.2 pero la versión más reciente disponible de la versión _principal_ 3.x.x es la versión 3.3.4, los parches se suministrarán en la base de código de la versión 3.3.x, lo que significa que el parche se suministrará en una (nueva) versión 3.3.5. La instancia de CFEE con la versión 3.1.2 debería actualizarse a la versión 3.3.5 para poder recibir el nuevo parche (es decir, el hecho de actualizar solo a la versión 3.3.4 no resolverá el problema solucionado en el parche, que se suministra solo en la versión 3.3.5).

## Escalado de la infraestructura CFEE
{: #scale}

Los usuarios necesitan los siguientes permisos para poder añadir o eliminar células de Cloud Foundry a una instancia CFEE:
* Rol de _administrador_ o superior sobre una instancia de CFEE.
* Rol de _operador_ o superior sobre el clúster de Kubernetes en el que se suministra el CFEE.

Para añadir células de aplicación a la instancia de CFEE:
1. Vaya al [panel de control de {{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/dashboard/apps/) y abra el {{site.data.keyword.cfee_full_notm}} al que desea añadir células.
2. Pulse **Añadir célula** junto a la tabla _Células_, lo que abre la página _Añadir células de Cloud Foundry_.
3. En la página _Añadir células de Cloud Foundry_, seleccione el número de células que desea añadir. La página también muestra la geografía y la ubicación de la instancia de CFEE en la que se añadirán las células. También muestra el número actual de células y la capacidad de las células que se van a añadir (lo que equivale a la capacidad de las células actuales). El panel derecho de la página muestra el coste estimado de las células añadidas junto con el nuevo coste total estimado del entorno.
4. Pulse **Añadir célula**.  
5. Vaya a la página _Nodos_. Se añade una nueva fila a la tabla _Células_ para cada nodo nuevo. La columna _Estado de nodo_ indica el progreso de la adición y el despliegue de la célula en el entorno CFEE.
