---

copyright:
  years: 2018
lastupdated: "2018-11-08"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}


# Gestión de dominios
{: #domains}

Hay dos tipos de dominios de Cloud Foundry:
* Los dominios compartidos están disponibles para cualquier aplicación en cualquier espacio dentro de {{site.data.keyword.cfee_full_notm}}.  Para acceder a los dominios compartidos, vaya a la página **Dominios** en el panel de navegación izquierdo de la IU (en *Operaciones*).
* Los dominios privados solo están disponibles para aplicaciones y espacios dentro de una organización específica.  Para acceder a los dominios dentro de una organización, vaya a la página **Organizaciones** en el panel de navegación izquierdo de la interfaz de usuario, abra la organización y vaya al separador **Dominios**.

## Creación y supresión de dominios
{: #create-domains}

Para crear un dominio compartido, vaya a **Dominios** en el panel de navegación izquierdo de {{site.data.keyword.cfee_full_notm}}.  

Para crear un dominio privado, vaya a la página **Organizaciones** en el panel de navegación izquierdo de la IU, abra la organización y vaya al separador **Dominios**.

Cuando esté en la página _Dominios_ (para dominios compartidos) o en el separador _Dominios_ de una organización específica (para dominios privados), pulse **Crear dominio** para crear un dominio y especifique un nombre exclusivo.

**Nota:** los nombres de dominio deben ser exclusivos en todo el ámbito de {{site.data.keyword.cfee_full_notm}}.  Es decir, un dominio privado no puede tomar el nombre de un dominio compartido o privado dentro de un determinado {{site.data.keyword.cfee_full_notm}}

También puede crear un dominio compartido desde la CLI de Cloud Foundry con el mandato siguiente:
  ```
  cf create-shared-domain <domain name>
  ```
  {: pre}
  
Puede crear un dominio privado desde la CLI de Cloud Foundry con el mandato siguiente:
  ```
  cf create-domain my-org <domain name>
  ```
  {: pre}
  
**Nota:** los dominios creados desde la CLI de Cloud Foundry se reflejarán en la interfaz de usuario inmediatamente, pero pueden tardar hasta 1 hora en entrar en vigor.

Para suprimir un dominio, vaya al menú situado más a la parte derecha de la fila de la tabla correspondiente al dominio que desea suprimir y seleccione **Suprimir dominio**.
  
También puede suprimir un dominio compartido desde la CLI de Cloud Foundry con el mandato siguiente:
  ```
  cf delete-shared-domain <domain name>
  ```
  {: pre}  
  
  ```
  cf delete-domain my-org <domain name>
  ```
  {: pre}
  
 
 ## Carga de certificados SSL
 {: #upload-certificates}
 
Puede cargar un certificado SSL para un dominio (compartido o privado). Pulse **Cargar** en la fila de la tabla correspondiente al dominio al que se va a añadir el certificado, seleccione el archivo que contiene el certificado y el archivo que contiene la clave privada.
  
