# Laboratorio 85-C: ***Uso de la cli de OpenShift***.

## La CLI de OpenShift: Control total de tu clúster desde la terminal

La `Interfaz de línea de comandos de OpenShift (CLI)`, también conocida como `oc`, es una herramienta fundamental para la gestión y administración de clústeres de OpenShift Container Platform (OCP). Esta  herramienta nos permite interactuar directamente con el cluster desde la terminal, permitiéndonos un control preciso sobre diversos aspectos, desde la creación y configuración de proyectos hasta el despliegue y administración de aplicaciones.

**Funcionalidades clave:**

* **Manejo de proyectos y aplicaciones:** Crea, elimina, modifica y visualiza proyectos dentro de tu clúster. Despliega, escala, monitoriza y elimina aplicaciones de forma sencilla.
* **Gestión de recursos:** Administra recursos como pods, imágenes, servicios, rutas y volúmenes en el clúster.
* **Automatización de tareas:** Automatiza tareas repetitivas y complejos flujos de trabajo mediante scripts y plantillas YAML.
* **Interacción con APIs:** Interactúa con las APIs de OpenShift para realizar tareas avanzadas.

Requisitos:

Una instancia en ejecución de OpenShift.


## Ejercicio 1: Instalación de la cli en la máquina del desarrollador.

Podemos instalar la `cli` de OpenShift (oc = OpenShift Cli) en `Linux`, `Windows` o `MacOS`.

Nota: Como OpenShift se actualiza automáticamente cada cierto tiempo, es conveniente reinstalar la cli de la misma forma. 

Para instalar la cli, realizamos el siguiente procedimiento:

Vamos a la página de descarga de OpenShift:
```
https://access.redhat.com/downloads/content/290
```

Seleccionamos la arquitectura de la lista 

En `Product Variant` seleccionamos ***Red Hat OpenShift Container Platform***.

En `Version` elegimos la última (***latest***).

En `Architecture` debe aparecer ***x86_64***.

Ahora hacemos clic en el botón `Download Now`para el producto `OpenShift Vx.x.x Windows Client`, o el que estimes oportuno para tu sistema operativo.

![Windows Client](../img/202406040948.png)

La descarga, para cualquiera de los sistemas operativos, es un archivo zip que contiene un ejecutable, que debemos colocar en un directorio que esté en el PATH. Descomprimimos en zip en la carpeta de descargas.

Para Windows, con el `Explorador de archivos`, creamos la siguiente carpeta: `C:\Archivos de programa\oc`

A continuación, movemos a dicha carpeta, el ejecutable `oc.exe` que debe estar en la carpeta de descargas.

Modifica la variable de entornos `PATH` para que contenga la nueva ruta.

![Path](../img/202406040959.png)

Abrimos una terminal de `cmd`. Probamos que todo ha ido correctamente. En la terminal, escribimos.
Nota: El mensaje de error que indica que no puede conectar con el servidor en perfectamente normal, ya que aun no hemos indicado donde se encuentra el Control Plane de OpenShift.
```
oc version
```

![oc version](../img/202406041012.png)

Como alternativa, podemos descargar la cli desde la consola web de administración de OpenShift. 

![cli](../img/202406041022.png)

La consola muestra enlaces para poder descargar la versión que más nos interese.

![URLs descarga cli](../img/202406041024.png)

## Ejercicio 2: Conexión al Control Plane desde la cli.

Para poder conectar la cli debemos conocer la URL de la API Server. Para ello, desde la consola web, hacemos clic en el icono de la interrogación y seleccionamos `Command Line Tools`. Se mostrará un enlace con eñ comando de `login`.

![URL login](../img/202406041033.png)

Hacemos clic en él y nos logamos en el Servidor. Aparecerá una nueva pantalla que nos permite visualizar el token de conexión. 

![oc login](../img/202406041038.png)

Copia el comando de login y ejecútalo en tu terminal.




