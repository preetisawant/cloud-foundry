---

copyright:
  years: 2018
lastupdated: "2019-01-15"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Uso de recursos

Los administradores y desarrolladores pueden ver cómo utilizan las aplicaciones y las células la capacidad de recursos (memoria y CPU) de un CFEE. Para supervisar el uso de recursos en una instancia de CFEE:

1. Vaya al [panel de control de {{site.data.keyword.Bluemix_notm}} Cloud Foundry](https://cloud.ibm.com/dashboard/cloudfoundry?filter=cf_environments) y abra el {{site.data.keyword.cfee_full_notm}} en el que desea gestionar la utilización de recursos.
2. En la interfaz de usuario de {{site.data.keyword.cfee_full_notm}}, vaya a la entrada **Uso de recursos** en la parte izquierda del panel de navegación y abra la página _Uso de recursos_. En la página _Uso de recursos_ puede ir a _Aplicaciones_ o a las subentradas _Células_ para abrir las páginas correspondientes.  La información que se muestra en las páginas _Aplicaciones_ y _Células_ puede considerarse dos formas de desglosar el uso de recursos:
   * La página **Aplicaciones** analiza el uso de recursos según las aplicaciones agregadas entre instancias.
   * La página **Células** muestra el uso de recursos de las instancias de aplicación que se ejecutan en células específicas. El patrón de uso de recursos entre células puede proporcionar conocimientos en la distribución de carga y capacidad.  Por ejemplo, puede ayudar a identificar problemas con el equilibrio de carga de aplicaciones (p. ej., diferencias importantes en los recursos utilizados por una aplicación entre células) o el uso de recursos que se acerca a la capacidad total (p. ej., porcentajes altos del uso de recursos en todas las células).

**Nota:** Los datos de uso del recurso representan el uso de los recursos durante el ciclo de recopilación de los últimos 5 minutos. Los datos de uso del recurso pueden actualizarse pulsando **Actualizar datos** en la parte superior de la página.

## Aplicaciones
{: #usage_apps}

La página Aplicaciones tiene dos secciones:
1. Gráficos de barras horizontales que muestran el uso de memoria física y reservada.
   * La memoria física y reservada utilizadas por las **apps seleccionadas** en la tabla siguiente.
   * La memoria física y reservada utilizada por **todas las apps** en la instancia de CFEE.
   * La memoria física utilizada por el **sistema**, que incluye memoria utilizada por el panel de control de Cloud Foundry, y la memoria de la aplicación almacenada en memoria caché por el panel de control de Cloud Foundry.
   * Memoria física y reservada **total disponible** en la instancia de CFEE.
   
   **Nota:** Cuando las aplicaciones reservan más memoria de la que físicamente hay disponible, se muestra un esquema rojo punteado en el gráfico de barras de la memoria reservada para representar la representar la cantidad de memoria reservada por las aplicaciones seleccionadas.

   Para mostrar el número que representa el porcentaje de memoria utilizada por todas las aplicaciones o las aplicaciones seleccionadas en la tabla, pase el cursor por la parte correspondiente del gráfico.  Al pasar el cursor por la parte *todas las apps* del gráfico, se muestra el porcentaje de memoria utilizada por todas las aplicaciones de CFEE en relación con el total disponible. Al pasar el cursor por la parte *apps seleccionadas* del gráfico, se muestra el porcentaje de memoria utilizada por todas las aplicaciones seleccionadas en la tabla, en relación con la memoria total disponible.

2. Una tabla con todas las aplicaciones.  Cada fila de la tabla muestra información de recursos de la aplicación.  Al expandir una fila se muestra la información de uso de recursos de varias instancias de la aplicación.

  La primera columna de la tabla es un recuadro de selección que determina si la aplicación correspondiente debe incluirse en el conjunto de *Apps seleccionadas* que debe incluirse en el gráfico de la parte superior de la página. Para incluir (o excluir) una aplicación en el conjunto seleccionado, pulse el recuadro de selección correspondiente.  Cuando se selecciona o se desmarca una aplicación para su incorporación en el conjunto, el gráfico se actualiza.  La descripción _Apps seleccionadas_ en la parte derecha del gráfico de barras indica (en paréntesis) el número de aplicaciones seleccionadas actualmente para su incorporación en el gráfico.

  La información siguiente se muestra en forma de columnas en la tabla de aplicaciones:
   * **Nombre de aplicación**: el nombre de la aplicación o la instancia de aplicación. Si el usuario no tiene permiso para acceder a la aplicación, en su lugar, se mostrará el GUID de aplicación.
   * **Instancias**: Representa el número de instancias en ejecución de una aplicación.  Para una instancia de aplicación (que se muestra debajo del nombre de aplicación cuando la fila de aplicación se expande) representa el nombre de la célula en la que se ejecuta la instancia de aplicación.
   * **Memoria física total**: MB de la memoria física utilizada por todas las instancias de una aplicación.  La memoria física utilizada por una aplicación es igual al total de la memoria física utilizada por todas las instancias de la aplicación.
   * **Memoria reservada total**: MB de la memoria reservada por todas las instancias de una aplicación.  La memoria reservada por una aplicación es igual al total de memoria reservada por todas las instancias de la aplicación.
   * **Promedio de CPU (% de la célula)**: Para las instancias de aplicación, la métrica representa el promedio de CPU **en la célula en la que se ejecuta**.  Para una aplicación, representa el promedio de uso de CPU en todos los promedios de instancia.
   * **Máximo de CPU (% de células)**: Para instancias de aplicación, la métrica representa el máximo de CPU utilizado por la instancia **en la célula en la que se ejecuta**.  Para una aplicación, representa el máximo del uso de CPU máximo de las instancias.
   * **CPU (% del sistema)**: El porcentaje de CPU total disponible en el CFEE utilizado por una aplicación y sus instancias.  La CPU utilizada por una aplicación es igual al total de porcentajes de CPU utilizados por todas las instancias de la aplicación.
   * **Solicitudes**: El número de solicitudes a una aplicación durante el último ciclo de recopilación de datos (cinco minutos).
   * **Organización**: La organización en la que se despliega la aplicación. Si el usuario no es un miembro de la organización, en su lugar, se mostrará el GUID de la organización.

Expanda una fila de aplicación en la tabla para ver la lista de instancias de aplicación y las métricas de uso de recursos correspondientes.

### Filtrado de aplicaciones
Puede filtrar el contenido de la tabla mediante los desplegables de filtro **Aplicaciones** y **Organizaciones** ubicados sobre la tabla.

Asimismo, puede utilizar el campo de entrada de filtro sobre la tabla para mostrar únicamente las aplicaciones que coinciden con la serie que ha introducido en el campo de filtro.  El filtro se refleja en la tabla y en el gráfico sobre la misma.

**Nota:** Los filtros funcionan de forma independiente a las filas de la tabla seleccionadas (mediante el recuadro de selección de la primera tabla de columnas) para la incorporación en el conjunto de _Apps seleccionadas_ incluidas en el gráfico anterior. Por ejemplo, si hay un total de diez aplicaciones en el entorno de CFEE y cinco de ellas se han seleccionado para su incorporación en el gráfico, cuando aplique el filtro que coincide únicamente con una instancia de aplicación, solo esta aparecerá en la tabla.  Además, el conjunto de _Apps seleccionadas_ solo incluirá la aplicación coincidente y el gráfico se actualizará en consecuencia.  Cuando elimine el filtro, las diez aplicaciones se mostrarán de nuevo en la tabla y el conjunto de _Apps seleccionadas_ se restablecerá para incluir todas las apps.


## Células
{: #usage_cells}

La página Células tiene dos secciones:
1. Gráficos de barras verticales que muestran:
   * La memoria y CPU *total disponible*, disponibles en la instancia de CFEE.
   * La memoria y la CPU utilizadas por las **Instancias de la app seleccionadas** de la instancia de CFEE.
   * La memoria y la CPU utilizadas por **Todas las instancias de la app** de la instancia de CFEE.
   * La memoria y la CPU utilizadas por el **Sistema** en la tabla siguiente.  El uso del sistema representa el recurso utilizado por los componentes del servicio de CFEE más la memoria caché de aplicaciones.
   * La memoria total y CPU disponible en la célula. El **total de células** es igual al total (memoria o CPU) disponible en el nodo de trabajador de Kubernetes (donde la célula es suministrada) menos lo que es utilizado por el sistema.

   Para mostrar el porcentaje de memoria o CPU utilizado por todas las instancias de app o por las instancias de app seleccionadas en la tabla, pase el cursor por la parte del gráfico correspondiente.  Al pasar el curso por la barra del gráfico se muestra la memoria o CPU absoluta disponible, la memoria o CPU utilizas por todas las apps y la memoria o CPU utilizada por el sistema + memoria caché.  También muestra el porcentaje de memoria o CPU utilizado por todas las apps y por el sistema + memoria caché relativos al total disponible.

2. Una tabla que lista todas las células y las instancias de aplicación que se ejecutan en las mismas.  Cada fila de la tabla muestra información de recursos para dicha célula e instancia de aplicación.

  La primera columna de la tabla es un recuadro de selección que determina si la instancia aplicación correspondiente debe incluirse en el conjunto de *Instancias de la app seleccionadas* para incluirla en el gráfico de la parte superior de la página. Para incluir (o excluir) una instancia de una aplicación en el conjunto seleccionado, pulse el recuadro de selección correspondiente.  Cuando se selecciona o se desmarca una instancia de aplicación para su incorporación en el conjunto, el gráfico se actualiza.

  La información siguiente se muestra como columnas en la tabla:
   * **Nombre de célula**: El nombre de la célula.
   * **Nombre de aplicación**: El nombre de la aplicación que se ejecuta en la célula. Si el usuario no tiene permiso para acceder a la aplicación, en su lugar, se mostrará el GUID de aplicación.
   * **Instancias**: El número de instancias de aplicación que se ejecutan en la célula.
   * **Memoria física**: MB de la memoria física utilizados por la instancia de aplicación que se ejecuta en la célula.
   * **Memoria reservada**: MB de la memoria reservada por la instancia de aplicación que se ejecuta en la célula.
   * **CPU (% de célula)**: El porcentaje de CPU total disponible en el CFEE utilizado por la instancia de aplicación que se ejecuta en la célula.

### Filtración de células e instancias de app
Puede filtrar el contenido de la tabla mediante el desplegable del filtro **Células** ubicado sobre la tabla y seleccionando las células que se deben mostrar en la tabla.

Asimismo, puede utilizar el campo de entrada de filtro sobre la tabla para mostrar únicamente las instancias de aplicación que coinciden con la serie que ha introducido en el campo de filtro.  El filtro se refleja en la tabla y en el gráfico sobre la misma.

**Nota:** Los filtros funcionan de forma independiente a las filas de la tabla seleccionadas (mediante el recuadro de selección de la primera tabla de columnas) para la incorporación en el conjunto de _Instancias de la app seleccionadas_ incluidas en el gráfico anterior. Por ejemplo, si hay un total de diez instancias de aplicación en el entorno de CFEE y cinco de ellas se han seleccionado para su incorporación en el gráfico, cuando aplique el filtro que coincide únicamente con una instancia de aplicación, solo esta aparecerá en la tabla.  Además, el conjunto de _Instancias de la app seleccionadas_ ahora solo incluirá la instancia de la app, y el gráfico se actualizará en consecuencia.  Cuando elimine el filtro, las diez instancias de aplicación se mostrarán de nuevo en la tabla y el conjunto de _Instancias de la app seleccionadas_ se restablecerá para incluir todas las instancias de app.

## Métricas de memoria
{: #memory_metrics}

Hay varias métricas de memoria disponibles en CFEE.  Esta diversidad de métricas de memoria responde a las diversas perspectivas desde las que se puede analizar la utilización de memoria. La utilización de memoria se puede medir en relación con la capacidad disponible en la célula o células de Cloud Foundry o en relación con la capacidad física total del nodo trabajador Kubernetes en el que se suministran las células (que puede incluir otra utilización de memoria no relacionada con Cloud Foundry). La capacidad de memoria también se puede ver desde la perspectiva de la memoria reservada (asignada) por las aplicaciones o desde la perspectiva de la memoria realmente utilizada por dichas aplicaciones.  

Estas son las métricas de memoria disponibles para los usuarios de una instancia de CFEE:

* Memoria total utilizada por los nodos trabajadores Kubernetes que dan soporte a las células de Cloud Foundry en relación con la capacidad total de memoria de dichos nodos.  Esto refleja la memoria de nodo trabajador utilizada no solo por las células de Cloud Foundry, sino también por el sistema o sobrecarga de memoria caché no relacionada con Cloud Foundry.  Esto se muestra en el indicador **Uso global** de la página **Visión general**.
* Memoria asignada a aplicaciones en relación con la memoria de célula disponible, independientemente de que dicha memoria se utilice realmente o no. Esto se muestra en el indicador **Asignada** de la página **Visión general**.
* Memoria física utilizada por las aplicaciones en relación con la memoria de célula disponible. La memoria de aplicación global utilizada se muestra en el indicador **Uso de app** de la página **Visión general**. La memoria utilizada por aplicaciones específicas se muestra en la página **Uso de recursos - Aplicaciones**.
* Memoria utilizada por las células de Cloud Foundry en relación con la capacidad de memoria del nodo trabajador.  Esto se muestra en la página **Uso de recursos - Células**.
* Memoria total utilizada por los nodos trabajadores (relacionada o no con Cloud Foundry). Esto se muestra en la página **Actualizaciones  y escalado**, tanto para los nodos que dan soporte a las células de CFEE como para los nodos que dan soporte  al plano de control de CFEE.
* Se muestran métricas adicionales en los paneles de control de Grafana, que se pueden iniciar desde la página **Supervisión**.  Estas métricas muestran capacidad y uso de memoria detallados para las células de Cloud Foundry y el clúster y los nodos trabajadores de Kubernetes.
