---

copyright:
  years: 2018
lastupdated: "2018-08-07"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Supervisión
{: #monitoring}

La supervisión de una instancia de {{site.data.keyword.cfee_full}} y de su infraestructura soportada están soportados por un conjunto de herramientas de código abierto formado por Prometheus y Grafana.  La solución le permite analizar, visualizar y gestionar alertas para métricas en el entorno de Cloud Foundry.  Hay tres consolas web desde las que se lleva a cabo la supervisión: Una consola de Grafana, una consola de Prometheus y una consola del Alert Manager de Prometheus.

**Nota:** El acceso a la función de supervisión en una instancia de {{site.data.keyword.cfee_full}} requiere un rol de _Administrador_ o _Editor_ en el clúster de Kubernetes que ofrece soporte a la instancia de CFEE.  El nombre predeterminado del clúster de Kubernetes que ofrece soporte a la instancia de CFEE es _`<CFEEname>`-cluster_.

## Prometheus
{: #prometheus}

Prometheus es un kit de herramientas de alerta y supervisión de sistema de código abierto. Desde su creación en 2012, muchas empresas y organizaciones han adoptado Prometheus y el proyecto tiene una comunidad de usuarios y desarrolladores muy activa.
Es un proyecto autónomo de código abierto que se mantiene de forma totalmente independiente a cualquier empresa. Para enfatizarlo y aclarar la estructura de gobernanza del proyecto, Prometheus se unió a Cloud Native Computing Foundation en 2016 como el segundo proyecto alojado, después de Kubernetes. Consulte la [documentación de Prometheus](https://prometheus.io/docs/introduction/overview/) para obtener más información.

El ecosistema de Prometheus consiste en varios componentes, de los cuales muchos son opcionales:

* El servidor de Prometheus principal que extrae y almacena datos de series temporales.</li>
* [Alertmanager](https://prometheus.io/docs/alerting/alertmanager/) para gestionar alertas.</li>
* Varios exportadores con un propósito específico como el exportador de nodos, el exportador de caja negra, etc.</li>
* Una puerta de enlace push para ofrecer soporte a los trabajos efímeros.</li>

Prometheus reúne las métricas de trabajos instrumentados, ya sea directamente o a través de una puerta de enlace push intermediaria para trabajos efímeros. Almacena todas las muestras reunidas localmente y ejecuta reglas en los datos para agregar o registrar nuevas series temporales a partir de datos existentes, o para generar alertas.

## Grafana
{: #grafana}

Grafana es una plataforma de análisis de código abierto para todas las métricas recopiladas por Prometheus. La versión de Grafana desplegada en su clúster ya está configurada para utilizar la base de datos de Prometheus subyacente. También contiene paneles de control de Grafana valiosos.  Consulte la [documentación de Grafana ](http://docs.grafana.org/guides/getting_started/) para obtener más información.

## Iniciación a la supervisión
{: #gettingStarted_monitor}

Los componentes de Grafana y Prometheus que componen la solución de supervisión están preinstalados en la infraestructura de Kubernetes que ofrece soporte a la instancia de CFEE.  Para acceder a las herramientas de supervisión es necesario reenviar los puertos de los servidores de Prometheus, Prometheus AlertManager y Grafana.  Esto se hace mediante la CLI de Kubernetes.
A continuación, se le guiará por los pasos para instalar las CLI necesarias, reenviar los puertos de servidor e iniciar las consolas.

**Nota:** Las siguientes instrucciones también están disponibles en la interfaz de usuario de {{site.data.keyword.cfee_full}}.  Abra la interfaz de usuario de la instancia de CFEE y pulse **Supervisión** en el panel de navegación de la izquierda para ver las instrucciones que se visualizan.

### Requisitos previos

1. Compruebe sus [Políticas de acceso](https://console.bluemix.net/iam/#/users) para asegurarse de que tenga como mínimo un rol de administrador sobre el clúster de Kubernetes que da soporte al entorno.
2. Instale la [CLI de IBM Cloud](https://console.bluemix.net/docs/cli/reference/ibmcloud/download_cli.html#install_use).
3. Instale la [CLI de Kubernetes](https://kubernetes.io/docs/tasks/tools/install-kubectl/).  Si ya tiene una CLI de Kubernetes, le recomendamos que instale la versión más reciente.
4. Instale el plugin del servicio de contenedor:
```
    ibmcloud plugin install container-service -r Bluemix
```

### Acceder al clúster de Kubernetes

1. Inicie sesión en su cuenta de IBM Cloud:

  ```
  ibmcloud login -a https://api.ng.bluemix.net
  ```
  {: pre}

  Si tiene un ID federado, utilice __ibmcloud login -sso__ para iniciar sesión en la CLI de IBM Cloud.

2. Establezca como destino la región de IBM Cloud Container Service en la que desea trabajar (por ejemplo, us-south):

  ```
  ibmcloud cs region-set us-south
  ```
  {: pre}

3. Establezca el contexto del clúster en su cli:

  a. Obtenga el mandato para establecer la variable de entorno y descargue los archivos de configuración de Kubernetes:

  ```
  ibmcloud cs cluster-config <CFEE_instance_name>-cluster
  ```
  {: pre}

  b. Establezca la variable de entorno KUBECONFIG. Copie la salida desde el mandato anterior y péguela en el terminal. La salida del mandato debe ser parecida a la siguiente:
  __export KUBECONFIG=/Users/$USER/.bluemix/plugins/container-service/clusters/cf-admin-0703-cluster/kube-config-dal10-cf-admin-0703-cluster.yml__

### Reenvío de los puertos de servidor
4. Configure el reenvío de puerto en el clúster de Kubernetes para los pods que ejecutan Prometheus, AlertManager y Grafana. Esto le permitirá alojar las métricas de supervisión según el proxy en su máquina local (sistema principal local):

  ```
  sh -c 'kubectl -n monitoring port-forward deployment/prometheus-server 9090 & kubectl -n monitoring port-forward deployment/prometheus-alertmanager 9093 & kubectl -n monitoring port-forward deployment/grafana 3000'
  ```
  {: pre}

### Inicie las consolas de supervisión en su proxy web local

5. Inicie la consola de Grafana para ver análisis sobre las métricas seleccionadas.  Hay paneles de control de Grafana predeterminados incluidos en la instancia de CFEE. Estos paneles de control predeterminados son interactivos y le proporcionan una vista de la infraestructura utilizada para alojar su instancia de CFEE. (clúster de Kubernetes). Cuando haya iniciado la consola de Grafana, haga clic en el botón **Inicio** en la parte superior de la consola de Grafana para seleccionar uno de los paneles de control desplegados previamente (vea la lista siguiente) que graficará las métricas correspondientes:

   Hay un usuario `admin` predeterminado en Grafana, con la contraseña predeterminada `admin`. Recomendamos iniciar sesión con el Usuario/Contraseña `admin/admin` y que los cambie por nuevas credenciales:

     [Iniciar la consola de Grafana](https://localhost:3000)

   Los paneles de control por defecto se proporcionan con la instancia de CFEE y están disponibles desde el desplegable _Inicio_.

   Paneles de control para la infraestructura de Kubernetes que ofrecen soporte a su entorno de CFEE:
   - Panel de control _Planificación de capacidad de Kubernetes_
        - Muestra la capacidad de la infraestructura de Kubernetes.
   - Panel de control _Estado del clúster de Kubernetes_
        - Muestra el estado del clúster de Kubernetes.
   - Panel de control _Estado del clúster de Kubernetes_
        - Muestra el estado del clúster de Kubernetes.
   - Panel de control _Solicitudes de recurso de Kubernetes_
        - Muestra la CPU utilizada, la memoria y otros parámetros del clúster de Kubernetes.
   - Panel de control _Nodos_
        - Muestra los detalles de cada nodo de trabajador del clúster de Kubernetes.
   - Panel de control _Pods_
        - Muestra los detalles de cada pod en ejecución del clúster de Kubernetes.
   - Panel de control _Conjunto de réplicas_
        - Muestra el estado de los conjuntos de réplicas de Kubernetes.
   - Panel de control _Despliegue_
        - Muestra el estado de los despliegues de Kubernetes.

   Paneles de control de Cloud Foundry:
   - Panel de control _CF: Capacidad de células_
        - Muestra el estado general de las células de Cloud Foundry en las que se despliegan las aplicaciones de Cloud Foundry.
   - Panel de control _CF: Direccionador_
        - Muestra el estado del direccionador de Cloud Foundry que se está ejecutando en su entorno de CFEE.
   - Panel de control _CF: Célula_Diego_
        - Muestra el estado de las células de Cloud Foundry y los componentes Diego.

6. Opcionalmente, también puede iniciar la consola de Prometheus para ver los datos en bruto recopilados por el servidor de Prometheus y el Alertmanager de Prometheus para gestionar las alertas enviadas por el servidor de Prometheus:

     [Iniciar el servidor de Prometheus](https://localhost:9090)

     [Iniciar el servidor Alertmanager de Prometheus](https://localhost:9093)
