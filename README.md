
# Introducción a Docker


## El Problema 1

Este es un flujo de instalación de software tradicional en cualquier computador. Es muy probable que nos haya pasado en más de alguna ocasión.

-   Partimos descargando el instalador.
    
-   Luego lo ejecutamos.
    
-   En algún momento inevitablemente tuvimos un mensaje de error durante la instalación.
    
-   Entonces buscamos soluciones en Internet.
    
-   Ejecutamos nuevamente el instalador.
    
-   y un nuevo error aparece.
    
Los inconvenientes son evidentes. El usuario debe buscar y descargar primero el instalador y, la **mayoría** de las veces, a la máquina de destino le **faltarían las dependencias necesarias** para que el software se ejecute según lo previsto.

Esto es lo que Docker intenta corregir. 

Docker quiere que sea realmente fácil y sencillo instalar y ejecutar software en cualquier equipo, en cualquier plataforma.

## El Problema 2

Supongamos que tenemos un stack que incluye varias tecnologías diferentes, como un servidor web que usa **Nodejs**, y una base de datos como **MongoDB**, un sistema de mensajería como **Redis** y una herramienta de orquestación como **Ansible**.

Surgen muchos problemas al desarrollar esta aplicación con todos estos componentes diferentes:

-   **Compatibilidad con el sistema operativo**, tenemos que asegurarnos de que todos estos diferentes servicios sean compatibles con la versión del sistema operativo que planeamos usar.
    
-   **Compatibilidad entre los servicios y las librerías y las dependencias del sistema operativo**. Surgen problemas en los que un servicio requiere una versión de una librería, mientras que otro servicio requiere otra versión.
    
-   **La arquitectura de nuestra aplicación cambia todo el tiempo**, surgen nuevas versiones de componentes, cambios en la bd, etc y cada vez que esto sucede debemos la verificar la compatibilidad entre estos componentes y la infraestructura.
    
-   Estas relaciones forman una matriz de compatibilidad, y el problema que provoca es conocida como **matrix from hell**. 

En palabras simples, es el desafío de empaquetar cualquier aplicación, independientemente del lenguaje/frameworks/dependencias, para que pueda ejecutarse sobre cualquier plataforma, independiente del sistema operativo/hardware/infraestructura.

Idealmente nos gustaría tener un método que replicase **un completo y complejo sistema** con una variedad de plataformas hardware y entornos con la posibilidad de actualizar componentes en lugar del sistema completo para cada cambio.

## La Solución

Los contenedores son una **solución al problema de cómo hacer que el software se ejecute de manera confiable** cuando se mueve de un entorno informático a otro.

Esto podría ser **desde una equipo de un desarrollador a un entorno de prueba,** desde un entorno de prueba a producción, y quizás desde una máquina física en un centro de datos a una máquina virtual en una nube pública o privada.

La matriz del infierno se convierte en matriz de contenedores. Docker nos ayuda a “**empaquetar**” cada componente de software como una imagen de contenedor estandarizada y ejecutarlo con un alto grado de **portabilidad** de una manera **repetible** y **confiable**.

## ¿Qué es Docker?

Docker es un proyecto de código abierto que permite **automatizar el despliegue de aplicaciones dentro de contenedores**.

Nos permite desarrollar, implementar y ejecutar aplicaciones dentro de contenedores ligeros y portables para que las aplicaciones de software puedan ejecutarse en cualquier máquina con Docker instalado, en resumen es una tecnología para desplegar aplicaciones y aunque los contenedores no son nuevos, su uso para implementar aplicaciones fácilmente sí lo es.

Con **Docker,** reduces el tiempo de **instalación y configuración** en los despliegues, subsanas los errores de **compatibilidad y múltiples versiones** de los sistemas, disminuyes los **tiempos de despliegue** de aplicaciones.

## ¿Qué es un contenedor?

El objetivo de Docker es permitirte **la creación paquetes estándar** pensados para despliegue llamados "**contenedores**" que incluyen **todo lo necesario para que una aplicación funcione** (dependencias, servicios...) y que se aíslan del sistema subyacente (Host) para lograr que siempre funcionen exactamente igual.

Los contenedores son muy útiles para mejorar la seguridad, la reproducibilidad y la escalabilidad en el desarrollo de software y la ciencia de datos. Su auge es una de las tendencias tecnológicas más importantes de la actualidad.

Los contenedores no son algo nuevo, es una tecnología que usa Linux. Existen diferentes tipos de contenedores como LXC, LXD , LXCFS etc.

Docker se basa en los contenedores LXC.

## Características de un contenedor

- **Liviano**: El peso de este sistema no tiene comparación con cualquier otro sistema de virtualización más convencional que estemos acostumbrados a usar.

- **Portable**: Los contenedores de Docker se pueden ejecutar en cualquier lugar, localmente en el centro de recursos de cliente, en un proveedor de servicios externo o en la nube.

- **Bajo Acoplamiento**: cada programa funciona independientemente de otros contenedores, de forma que aplicaciones con requerimientos opuestos pueden funcionar en paralelo en el mismo sistema.

- **Seguro**: Aplicaciones aisladas. Cada contenedor dispone de sus propios recursos. Ningún contenedor ve los procesos de otro contenedor.

- **Escalable**: Fácilmente escalable.

## Contenedores

Esta sería la solución al problema de matrix from hell vista anteriormente mediante el uso de contenedores.

Con Docker podemos ejecutar cada componente con sus propias librerías y dependencias, en contenedores separados.

Con esto surge el concepto de Contenerizar (Dockerizar) aplicaciones.

## Diferencia entre VM y Contenedores

### Virtualización

Es la **abstracción de los recursos de un servidor** de forma que se **crea una capa entre el hardware** de la máquina física (host o hypervisor) y **el sistema operativo** de la maquina virtual (guest).

### Máquinas Virtuales (VM).

La idea de una VM es la de **emular** un entorno como si fuera un servidor físico completo, y de esta forma proporcionar un entorno de ejecución independiente.

La virtualización convencional con VM se apoya en una pieza de software llamado Hypervisor, que **distribuye** los recursos de hardware del sistema de Host (**anfitrion**) entre los sistemas operativos Guest (**invitado**).

Cada VM es cargada con un sistema operativo completo, cuyo tamaño puede alcanzar varios GB.

Cada VM tiene su propio Kernel, no usa o comparte el Kernel del host. Mayor aislamiento.

En cada VM podemos ejecutar sistemas operativos diferentes.

### Contenedores.

La virtualización mediante contenedores, por el contrario, **no inicia ningún sistema operativo adicional**. 

Los contenedores **comparten el Kernel del SO** que es el responsable de interactuar con el hardware. El software sobre el Kernel de Linux hace que los SO sean diferentes (Ubuntu, Fedora, Debian, etc…)

Se quita la capa del SO que tienen las VM, de esta forma los contenedores corren **solo nuestra aplicación** junto a las librerias/dependencias incluidas.

Debido a que las diferentes distribuciones del SO Linux (Ubuntu, Fedora, Debian, etc) comparten el mismo Kernel, Docker es capaz de ejecutar sobre ellos contenedores con otras distribuciones de Linux.

Los contenedores son **pequeños** en tamaño y uso de recursos, además inician más **rápidos** en comparación con las máquinas virtuales.

Distinguimos 2 tipos de contenedores:

 - Basados en el kernel de Linux (solo pueden correr en un servidor (Host) Linux)
 - Basados en el kernel de Windows (solo puede correr en un servidor (Host) Windows)

**¿ Como ejecutamos contenedores linux en Windows/Mac ?**

En este caso el Docker Desktop con el que se instala Docker en Windows y Mac, Docker funciona utilizando una pequeña maquina virtual.

En el caso de contenedores basados en el kernel de Windows, estos solo funcionan con las versiones de Windows 10 y Windows Server 2016, siendo bastantes más pesados con respecto a los basados en Linux.



## Arquitectura

La arquitectura Docker es una **arquitectura cliente-servidor**, donde el **cliente habla con el servidor** (que es un proceso daemon) **mediante un API** para poder gestionar el ciclo de vida de los contenedores y así poder construir, ejecutar y distribuir los contenedores.

El hecho de que el cliente se comunique con el servidor mediante el API hace que el cliente y servidor puedan estar en la misma máquina comunicándose mediante sockets de UNIX o bien en máquinas diferentes comunicándose mediante un end-point en la red.

**Docker Host** es la máquina (Servidor) donde se ejecutando el Deamon (dockerd) de Docker.

**Docker Daemon** es un servicio en segundo plano de Linux que se ejecuta en la máquina host de Docker y administra el ciclo de vida de los contenedores de Docker (creación, ejecución, eliminación, etc.). En terminología de Linux, el demonio es un proceso que se ejecuta en el sistema operativo generalmente como un servicio.

**Docker Client** es la interfaz de línea de comandos (CLI)  y facilita la comunicación entre el usuario y el demonio de Docker mediante llamadas a la API REST. Docker CLI no es el único cliente, hay muchas implementaciones de UI como Kitematic o Portainer.

Otras aplicaciones en Docker pueden comunicarse directamente con el API REST. Con ésto tenemos todo lo necesario para manejar elementos de Docker como imágenes, contenedores, networks y volúmenes.

El **Docker Registry** es el lugar donde se almacenan las imágenes de que creamos, o donde podemos descargar una imagen base para contenerizar nuestra aplicación. El registry puede ser público (Docker Hub) o privado alojado en una nube pública o privada.

**Nota**: Docker está escrito en GO (inicialmente en Python), aunque también se aprovecha de muchas de las capacidades del kernel Linux, como namespaces, cgroups, y el sistema de ficheros UnionFS (capas).

## Imágenes vs Contenedores

### Imágenes

Una imagen de Docker es un archivo o **plantilla** de solo-lectura, **inmutable** (una vez que se crea no cambia), que contiene el código fuente, librerías, dependencias y todo lo necesario para que se ejecute una aplicación. 

Debido a su calidad de solo-lectura, estas imágenes son denominadas **snapshots**.

Cada archivo de imagen de Docker **se compone de una serie de capas**. Estas capas se combinan en una sola imagen. Una capa se crea cuando la imagen cambia.

### Contenedores

Un contenedor es una entidad lógica, una **agrupación de procesos que se ejecutan de forma nativa** como cualquier otra aplicación en la máquina host. Los procesos no tienen acceso a nada que se encuentre fuera del contenedor, y no sólo eso, no tienen forma de consumir más recursos que los que el contenedor les permite.

Los contenedores se crean a partir de imágenes y representan la instancia real de una aplicación / servicio / etc. Si viene con experiencia en programación OOP, puede pensar en los contenedores como instancias de clases e imágenes como clases en sí mismas.

## Capas

Cada archivo de imagen de Docker **se compone de una serie de capas** cada una con id único. Cada capa agrega cambios incrementales que son guardados sobre las capas existentes. Cada vez que un usuario especifica un comando, como ejecutar o copiar, se crea una nueva capa.

-   Una imagen es construida a partir de múltiples capas, donde en el nivel más bajo tenemos la capa base correspondiente al SO.
    
-   Las capas superiores podrían tener software o librerías personalizados, por ejemplo Apache, Python, Java, etc.
 
Docker **reutiliza estas capas para construir nuevos contenedores**, lo cual hace mucho más rápido el proceso de construcción. Los cambios intermedios se comparten entre imágenes, mejorando aún más la velocidad, el tamaño y la eficiencia.

Tomemos por ejemplo el caso de dos contenedores con capas de imagen 1, 2, 3 y otro 1, 2, 4, entonces Docker solo tiene que almacenar una copia de cada capa de la imagen, tanto a nivel local como en el repositorio.

Esto gracias a un servicio de Linux llamado **Unionfs** Union Files System.

## Dockerfile

Docker **construye** imágenes automáticamente **leyendo las instrucciones de un Dockerfile**, un archivo de texto que contiene todos los comandos, en orden, necesarios para crear una imagen determinada. Este fichero sigue un formato específico y conjunto de instrucciones que podemos encontrar en la documentación de Docker.

Mediante este fichero podemos generar una nueva imagen personalizada.

Básicamente lo que el Dockerfile contiene es un conjunto de comandos que podríamos ejecutar directamente desde el CLI de Docker, pero que como siempre suelen ser los mismos para una aplicación se genera este fichero con toda la lista de comandos a ejecutar en orden, y con esto Docker es capaz de generar automáticamente una imagen de nuestra aplicación.

Estructura Instrucciones:

-   Fundamentales: FROM, ARG
    
-   Configuración: RUN, ADD | COPY, ENV
    
-   Ejecución: CMD, ENTRYPOINT, EXPOSE
 
### Listado de comandos más utilizados

**FROM** — Especifica la base para la imagen.

**ENV** — Establece una variable de entorno persistente.

**ARG** — Permite definir una variable usable en el resto del Dockerfile con la sintaxis ${NOMBRE_DEL_ARG}

**RUN** — Ejecuta el comando especificado. Se usa para instalar paquetes en el contenedor.

**COPY** — Copia archivos y directorios al contenedor.

**ADD** — Lo mismo que COPY pero con la funcionalidad añadida de descomprimir archivos .tar y la capacidad de añadir archivos vía URL.

**WORKDIR** — Indica el directorio sobre el que se van a aplicar las instrucciones siguientes.

**ENTRYPOINT** — Docker tiene un Entrypoint por defecto, /bin/sh -c, que se ejecuta cuando el contenedor está listo. Este comando permite sobreescribirlo.

**CMD** — Especifica el comando y argumentos que se van a pasar al contenedor. Se ejecutarán junto con lo indicado en el Entrypoint.

**EXPOSE** — Indica que puerto del contenedor se debe exponer al ejecutarlo. No lo expone directamente.

**LABEL** — Nos permite aportar meta-datos a la imagen.

**VOLUME** — Crea un directorio sobre el que se va a montar un volumen para persistir datos más allá de la vida del contenedor.

**USER** — Establece el usuario que se va a usar cuando se ejecute cualquier operación posterior con RUN, CMD y ENTRYPOINT.

## Creación de Imágenes

Esto es el concepto conocido como Contenerización o Dockerización.

- **Dockerfile**: Instrucciones para construir una imagen.
- **Imagen**: Snapshot de un contenedor.
- **Contenedor**: Instancias ejecutándose de una imagen de Docker.

## Ciclo de Vida de Contenedores

Haciendo foco particularmente en el contenedor, podemos mencionar que los diferentes estados que este puede manejar son `Created`, `Running`, `Stopped`, `Paused`, `Killed`.

Ciclo de vida básico:

-   En este ciclo de vida se crea el contenedor a partir de una imagen.
-   Se ejecuta el proceso determinado en el contenedor.
-   El proceso de finaliza y el contenedor se detiene.
-   Se destruye el contenedor.

## Comandos Básicos

**docker build**: Construye una imagen a partir de un archivo Dockerfile.

**docker pull**: Descarga una imagen desde un registry, por defecto Docker Hub.

**docker images**: Obtiene un listado de las imágenes disponibles.

**docker image**: Administra imágenes. Dentro de las opciones podemos encontramos las de listar o eliminar una imagen.

**docker run:** Ejecuta un comando en un nuevo contenedor. Es usado para iniciar un contenedor a partir de una imagen, si no está localmente es descargada de un registry, Docker Hub por defecto. Si no especificamos el tag se descargara la última versión disponible (latest).

**docker ps**: Lista los contenedores que se encuentran en ejecución. Para mostrar aquellos todos los contenedores utilizamos el indicador -a.

**docker stop**: Detiene uno o más contenedores en ejecución.

**docker start**: Inicia uno o más contenedores detenidos.

**docker rm**: Elimina uno o más contenedores detenidos. Se puede utilizar la opción -f para forzar la detención.

**docker logs**: Obtiene los logs de un contenedor.

**docker inspect**: Retorna todos los detalles de un contenedor, información de bajo nivel, en formato JSON.

**docker push**: Publica la imagen en un registry. Antes de subir la imagen debemos etiquetarla. Al hacer push las capas que ya están subidas no se vuelven a subir. Todos los registry siguen una nomenclatura a la hora de almacenar los repositorios. En el caso de Docker Hub necesitamos que nuestra imagen se llame nombre_de_usuario/nombre_del_repositorio:etiqueta.

## Ejemplo Práctico

    docker run --name my-nginx -d nginx
    docker ps
    docker exec -it my-nginx sh
    curl localhost:80
    docker run --name my-nginx-2 -p 8080:80 -d nginx
    curl localhost:8080
    docker stop my-nginx my-nginx-2
    docker rm my-nginx my-nginx-2
    docker rmi nginx
    
Dockerfile

```
FROM nginx
COPY static-html-directory /usr/share/nginx/html
```

```
echo "<html>hola mundo</html>" > index.html

echo "FROM nginx
COPY . /usr/share/nginx/html" > Dockerfile
```

```
docker build . -t my-nginx-image
docker run --name my-nginx-container -p 8080:80 -d my-nginx-image
docker stop my-nginx-container
docker rm my-nginx-container
docker rmi my-nginx-image
```
