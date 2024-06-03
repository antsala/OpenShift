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

Hacemos clic en 'Create Project'. Aparecerá el formulario de creación de proyecto. En él aportamos la siguiente información.

En ***Name*** escribimos:
```
user-getting-started
```

En ***Display name***:
```
Getting Started with OpenShift
```

***Description*** lo dejamos vacío y hacemos clic en el botón `Create`.

Con esto finaliza la creación del proyecto de OpenShift.

## Ejercicio 3: Revisión de los permisos.

OpenShift Container Platform crea automáticamente algunas `cuentas de servicio` especiales en cada proyecto.

Una `cuenta de servicio` en OpenShift es una identidad especial que se utiliza para ejecutar `pods` dentro de un proyecto (o namespace) y para otorgar permisos específicos a aplicaciones y servicios que se ejecutan en esos pods. A diferencia de las cuentas de usuario normales, las cuentas de servicio no están vinculadas a personas individuales sino a aplicaciones o componentes de la infraestructura, permitiendo un control granular sobre los permisos y roles necesarios para que estas aplicaciones accedan a recursos específicos dentro del cluster de OpenShift. Esto facilita la gestión segura y eficiente de los recursos y operaciones automatizadas en el entorno de contenedores.

La cuenta de servicio `predeterminada` asume la responsabilidad de ejecutar los pods. OpenShift Container Platform usa e inserta esta cuenta de servicio en cada pod que inicia.

La práctica que vamos a hacer crea un objeto `RoleBinding` para el objeto de cuenta de servicio predeterminado. La cuenta de servicio se comunica con la API de OpenShift Container Platform para obtener información sobre los pods, los servicios y los recursos del proyecto.

Cambiamos a la `perspectiva de administrador`.

Elegimos la opción `RoleBindings`

![Perspectiva desarrollador](../img/202406030945.png)

En la imagen puedes ver que ya existen una cantidad importante de RoleBindings en el cluster. Hacemos clic en `Create binding`.

![Create Binding](../img/202406030949.png)

Rellenamos el formulario con la siguiente formación.

En ***Name***:
```
sa-user-account
```

La denominación `sa` en `sa-user-account `proviene de la abreviatura de ***Service Account***.

En ***Namespace*** buscamos nuestro proyecto, que se llama:
```
user-getting-started
```

En ***Role name*** buscamos `view` y seleccionamos ese rol.
```
view
```

En ***Subject*** seleccionamos `ServiceAccount`.

En ***Subject namespace*** buscamos y seleccionamos:
```
user-getting-started
```

En ***Subject name*** escribimos:
```
default
```

Por último hacemos clic en `Create`.

El resultado debe ser el siguiente:

![resultado](../img/202406031003.png)

la vista `YAML` permite visualizar la definición del objeto creado en el cluster.

![resultado](../img/202406031005.png)

## Ejercicio 4: Desplegar una imagen de contenedor.

La forma más sencilla de implementar una aplicación en OpenShift Container Platform es ejecutar una imagen de contenedor existente. En la práctica siguiente, implementamos un componente ***front-end*** de una aplicación denominada `national-parks-app`. La aplicación web ofrece un mapa interactivo donde se muestra la ubicación de los principales parques nacionales del mundo.

Nos aseguramos de estar en la `perspectiva desarrollador` (Developer).

Como lo que deseamos hacer es elegir una imagen de contenedor, seleccionamos `Container images` desde la consola web.

![Container images](../img/202406031011.png)

Rellenamos el formulario con la siguiente información.

En ***Image Name***, escribimos la ruta de la siguiente imagen:
```
quay.io/openshiftroadshow/parksmap:latest
```

Se realizará una verificación. 

En el desplegable `Runtime icon` podemos elegir el icono de nuestra elección.

Comprobar que en la sección `General` aparece la siguiente información:

Nota: Es posible cambiar estos valores a los que necesitemos.

![General](../img/202406031016.png)

En la sección `Deploy` debemos comprobar que la imagen seleccionada se desplegará en un objeto `Deployment`de Kubernetes.

![Deployment](../img/202406031019.png)

Nota: En OpenShift, la principal diferencia entre `Deployment` y `DeploymentConfig` radica en cómo gestionan las actualizaciones y despliegues de las aplicaciones. `Deployment` es un objeto nativo de Kubernetes que utiliza controladores y replicasets para gestionar el ciclo de vida de las aplicaciones, proporcionando características avanzadas como despliegues automáticos, rollbacks, y actualizaciones continuas. Por otro lado, `DeploymentConfig` es específico de OpenShift y ofrece funcionalidades adicionales como hooks de despliegue personalizados y una integración más estrecha con otras características de OpenShift, como las estrategias de despliegue personalizadas y las builds automáticas. Aunque `DeploymentConfig` proporciona más opciones de personalización, `Deployment` es más estándar y portable a cualquier clúster de Kubernetes.

Para que nuestra aplicación sea accesible, debemos crear una `Ruta`. 

![Route](../img/202406031022.png)

En OpenShift, el uso de las `etiquetas` (labels) es fundamental. Para ver las etiquetas asociadas a este despliegue, hacemos clic en el enlace `Labels`, tal y como podemos apreciar en la siguiente imagen.

![Labels](../img/202406031026.png)

Añadimos las siguientes etiquetas:
```
app=national-parks-app

component=parksmap

role=frontend
```


Finalizamos la práctica haciendo clic en el botón `Create`.

La interfaz gráfica permitirá seguir configurando nuestra aplicación.

![UI](../img/202406031024.png)



