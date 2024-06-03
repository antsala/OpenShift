# Laboratorio 85-B: ***Desplegar la aplicación de parques naturales en crc***.

La aplicación `national-parks` de OpenShift es un ejemplo de aplicación diseñada para demostrar las capacidades de la plataforma OpenShift, que es una solución de Kubernetes empresarial desarrollada por Red Hat. Esta aplicación suele ser utilizada en tutoriales, demostraciones y talleres para mostrar cómo desplegar, gestionar y escalar aplicaciones en un entorno OpenShift. 

La aplicación "national-parks" tiene como objetivo demostrar el uso de OpenShift. A través de esta aplicación, los usuarios pueden aprender sobre el despliegue de contenedores, la configuración de pipelines CI/CD, el escalado automático, la gestión de recursos y otros aspectos de OpenShift.

Las tecnologías involucradas son: 
   - **Contenedores Docker**: La aplicación está empaquetada en contenedores Docker, lo que permite una fácil implementación y escalabilidad en OpenShift.
   - **OpenShift Templates y Operators**: Utiliza plantillas y operadores de OpenShift para facilitar el despliegue y la gestión de la aplicación.
   - **CI/CD**: Puede incluir pipelines de CI/CD (Integración Continua / Despliegue Continuo) para demostrar cómo automatizar la construcción, prueba y despliegue de la aplicación.


Requisitos:

Una instancia en ejecución de local.


## Ejercicio 1: Conectar a la consola web.

Iniciamos sesión en la consola web de OpenShift Container Platform con nuestras credenciales de inicio de sesión. Conectamos a la siguiente URL, e iniciamos sesión con las credenciales de administrador.
```
https://console-openshift-console.apps-crc.testing
```

Nos redirigirá a la página Proyectos. Para los usuarios no administradores, la vista predeterminada es la `perspectiva del desarrollador`. Para los administradores de clústeres, la vista predeterminada es la `perspectiva Administrador`. Si no tenemos privilegios en el cluster, no veremos la perspectiva de administrador en la consola web.

![Perspectiva administrador](../img/202406030924.png)


La consola web proporciona dos perspectivas: la perspectiva del administrador y la perspectiva del desarrollador. La perspectiva del desarrollador proporciona flujos de trabajo específicos para los casos de uso del desarrollador. La perpectiva de administrador permite desplegar aplicaciones y administrar el cluster.


## Ejercicio 2: Creación de un proyecto.

Los `proyectos` son extensiones de OpenShift Container Platform a los `espacios de nombres` de Kubernetes. 

Los usuarios ***deben recibir acceso a los proyectos*** por parte de los administradores. Los administradores de clústeres pueden permitir que los desarrolladores creen sus propios proyectos. En la mayoría de los casos, los usuarios tienen acceso automáticamente a sus propios proyectos.

Cada proyecto tiene su propio conjunto de `objetos`, `políticas`, `restricciones` y `cuentas de servicio`.

En la consola web de OpenShift Container Platform, elegimos la `perspectiva del desarrollador`.

![Perspectiva desarrollador](../img/202406030934.png)

Tiene las funciones y los permisos adecuados en un proyecto para crear aplicaciones y otras cargas de trabajo en OpenShift Container Platform.